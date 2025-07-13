---
title: A template for Bash scripts
description: I write tiny utility Bash scripts often, so it's usefult to have a template with common boilerplate.
---

<!--more-->

I like to automate easy mundane tasks using shell scripts. They can be a wrapper that launches a program with some predefined arguments, converting hexadecimal numbers to and from decimal, etc.

If I don't need to process complex arguments to these scripts[^1], I normally write them in Bash. The main reason is that they're mostly self-contained, have great portability and integrate natively with the rest of the command-line interface.

But I found myself writing more or less the same boilerplate code every time, like helper constants or log functions. So I created a [template](https://github.com/elitalon/dotfiles/blob/main/scripts/template.sh):

```bash
#!/usr/bin/env bash

# Enable shell behaviours if script is not being sourced
# Via: https://stackoverflow.com/a/28776166/8787985
if ! (return 0 2> /dev/null); then
    set -o nounset  # Treat unset variables and parameters as an error
    set -o errexit  # Exit if a pipeline returns a non-zero status
    set -o pipefail # Use last non-zero exit code in a pipeline
fi

###
# Constants
###
SCRIPT_DIRECTORY=$(cd -- "$(dirname -- "${BASH_SOURCE[0]}")" &> /dev/null && pwd)
PROGRAM_NAME="$(basename "${0:-__PROGRAM_NAME__}")"
readonly SCRIPT_DIRECTORY PROGRAM_NAME

###
# Log functions
###
function fail() {
    local message=${1:-"Error"}
    local code=${2:-1}

    if [[ $code -eq 0 ]]; then
        code=1
    fi

    warn "${message} (${code})"
    exit "$code"
}

function warn() {
    local message=${1:-}
    echo -e "\033[91m${message}\e[0m"
}

function notice() {
    local message=${1:-}
    echo -e "\033[93m${message}\e[0m"
}

function info() {
    local message=${1:-}
    echo -e "${message}"
}

###
# Whether a program exists in the search path
###
function program_exists() {
    if [[ $# -lt 1 ]]; then
        fail "Missing binary name argument in program_exists" 2
    else
        command -v "$1" 1>/dev/null 2>&1
    fi
}

###
# Write your functions here
###
function hello_world() {
    info "Hello, world!"
}

###
# Main function
###
function main() {
    # Invoke your functions here
    hello_world
}

# Invoke main with args if script is not being sourced
# Via: https://stackoverflow.com/a/28776166/8787985
if ! (return 0 2> /dev/null); then
    main "$@"
fi
```

The downside of this template is that any future changes or improvements are not applied retroactively. But it's been OK so far because once a script does what I need it to do, I normally don't change it much.

Note that I made it purposely simple to cover my needs. There are more [complete implementations](https://github.com/ralish/bash-script-template) out there with other use cases in mind that are definitely worth checking.

Of course, creating an actual script from this template is another routine task in itself, so I created [a script for that](https://github.com/elitalon/dotfiles/blob/main/scripts/mkscript.sh) too (redacted for brevity):

```bash
#!/usr/bin/env bash

set -o nounset
set -o errexit
set -o pipefail

###
# Log functions
###
function fail() {
    # …
}

function warn() {
    # …
}

function info() {
    # …
}

###
# Creates a script out of the template
###
function make_template() {
    local template_script
    template_script=template.sh
    [[ -f "${template_script}" ]] \
        || fail "Template script ${template_script} does not exist" 2

    local filename=${1:-}
    [[ -z "${filename}" ]] && fail "Missing filename" 3
    [[ -e "${filename}" ]] && fail "Script ${filename} already exists" 3

    info "Creating ${filename}"
    cat "${template_script}" > "${filename}"

    info "Making ${filename} executable"
    chmod 0755 "${filename}"

    info "Moving ${filename} to bin/ directory"
    mv "${filename}" bin/
}

###
# Main function
###
function main() {
    make_template "${1:-}"
}

main "$@"
```

And you can install any of these scripts for system-wide usage like this:

```bash
#!/usr/bin/env bash

set -o nounset
set -o errexit
set -o pipefail

function fail() {
    # …
}

function warn() {
    # …
}

function info() {
    # …
}

function install_for_all_users() {
    local path=${1:-}
    [[ -z "${path}" ]] && fail "Missing path for script"
    [[ -d "${path}" ]] && fail "${path} is a directory"
    if [[ ! -f "${path}" && ! -x "${path}" ]]; then
        fail "${path} is not a regular nor executable file"
    fi

    info "Removing extension from ${path}"
    local filename
    filename="$(basename "${path}")"
    local program_name
    program_name="${filename%.*}"

    local destination="/usr/local/bin/${program_name}"
    info "Installing ${path} to ${destination}"
    cp -f "${path}" "${destination}"

    info "Making ${destination} executable"
    chmod 0755 "${destination}"

    local user=elitalon
    local group=staff
    info "Setting user and group to ${user}:${group}"
    chown "${user}:${group}" "${destination}"

    info "Done!"
}

function main() {
    install_for_all_users "${1:-}"
}

main "$@"
```

[^1]: [`getopts`](https://en.wikipedia.org/wiki/Getopts) is not the most straightforward command for parsing arguments, so I turn to Ruby in all other cases.
