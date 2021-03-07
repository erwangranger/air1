# air1

<!--
```bash
#!/bin/bash

function air1() {

if [ $# -eq 0 ] ; then
    printf "Thanks for using air1\nTry the following for the help menu:\n      air1 --help \n"
fi

## if you ever need to make your own copy and call it something else
## just do a straight search-and-replace
local air1="air1"

air1_header(){
    printf "
+-----------------------+
|        air1           |
+-----------------------+
"
}

```
-->

## Quickstart

### Try it

In order to try `air1`, copy-paste the following command into a Linux terminal.

```sh
br="dev/alpha"
eval "$(curl -fsSL https://raw.githubusercontent.com/erwangranger/air1/${br}/README.md \
    | awk '/^```bash/{flag=1;next}/^```/{flag=0}flag' )"
```

This will set it up temporarily in your terminal. You can then use all the commands below.

### Version information

If you want to check which version of `air1` you are using, execute:

```sh
air1 --version
```

<details><summary>code</summary>

```bash

function air1_version(){
    air1_header
    printf "You are running air1 version Alpha 0.0.1\n"
}


```

</details>

### Install it

If you want to permanently setup `air1`, you have to:

1. First, run the command to [set it up temporarily](#try-it)
2. Execute:

    ```sh
    air1 --install
    ```

If you are curious as to how it installs itself, unfold the code below:

<details><summary>code</summary>

```bash
function air1_install(){
    local github_url_base=https://raw.githubusercontent.com/erwangranger/air1
    local github_branch=dev/alpha
    local github_file=README.md
    local github_full_url=${github_url_base}/${github_branch}/${github_file}
    air1_version
    printf "Generation of file ~/.air1.sh "
    curl -fsSL ${github_full_url} \
            | awk '/^```bash/{flag=1;next}/^```/{flag=0}flag' \
            > ~/.air1.sh

    retVal=$?
    if [ $retVal -ne 0 ]; then
        printf "has failed!\n"
    else
        printf "successful!\n"
    fi


    local bashrc_loc="${HOME}/.bashrc"
    local air1_loc="${HOME}/.air1.sh"
    printf "Updating your ${bashrc_loc} file "

    ## if the line already exists, we remove it.
    local bashrc_remove_air1="sed -i.bak '/\.air1\.sh/d' ${bashrc_loc}"
    bash -c " ${bashrc_remove_air1} "

    ## if the file exists, we add a reference to in .bashrc
    echo "[[ -e \"${air1_loc}\" ]] && source \"${air1_loc}\" || { echo \"ERROR: ${air1_loc} does not exist\" 1>&2 ; exit 1; }" >>  ${bashrc_loc}

    retVal=$?
    if [ $retVal -ne 0 ]; then
        printf "has failed!\n"
    else
        printf "has worked!\n"
    fi
}
```

</details>


### Update it

### Remove it

## Principles

### Frictionlessness

### Horse first, cart second

Too often, software engineering is worried first (or only) about **what the software does** and not so much about **how does software end up in the hands of the user**. Because that has to be someone else's job, surely.

I disagree with this approach. So the first order of business in this project will be to make it extremely easy to obtain and update the software. Even before said software does anything useful.

## Documentation

### Help menu

If you call `air1` with the `--help` parameter, you will see the help menu.

If you want to look at it here, click the unfold:

<!--
```bash
function air1_help(){
    air1_version
    printf "
```
-->

<details><summary>unfold</summary>

```bash
-h  /  --help : this help screen
--version     : the version of air1 you are using
--install     : installs the latest version of air1
```

</details>

<!--
```bash
"
}
```
-->

### Locally

#### Seeing the generated code

If you want to see the entirety of the generated `air1` function, execute:

```sh
cat README.md | awk '/^```bash/{flag=1;next}/^```/{flag=0}flag'
```

#### Try it locally

Assuming that you have the README.md in the current directory.

```sh
eval "$( cat README.md | awk '/^```bash/{flag=1;next}/^```/{flag=0}flag' )"
# followed by
air --help
```

## Background

### Naming

Over the years, many english-speaking friends and colleagues have asked me how they were supposed to pronounce my first name. And I would respond that I really did not care if my name was butchered, and that I respond from anything from Erwin, to Edward and even Owen.

One colleague insisted until I told him that pronouncing it "like Air Force One minus the force" was as close as he was ever going get. He then proceed to call me "Air Force One" the whole day.

So because this is a selfish project that only serves my own needs, I decided to name it after myself.

### Needs

As more and more of my working life is spent typing increasing complex commands into a terminal window, I found myself in need of an easier way of storing and retrieving increasingly arcane incantations. The `air1` project was born out of this need.

### Rant

<!--
```bash

while [[ $# -gt 0 ]]; do
    case ${1} in
        --version)
            shift
            air1_version
            shift
            ;;
        -h|--help)
            shift
            air1_help
            shift
            ;;
        --install|--deploy)
            shift
            air1_install
            shift
            ;;
        *)
            printf "\n\nOne or more arguments were not recognized: \n$@"
            air1_help
            shift
    ;;
    esac
done


}
```
-->
