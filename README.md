# git-template-test
Test repo for experiments in Git Templates

## Introduction

We would like to ensure all our repositories have certain hooks enabled
and run via `pre-commit` for every commit. This repo can be used as a
git template directory to ensure engineers only have to install the
tooling once in a central place rather than for every repo they `clone`
or `init`.

## Installation and configuration

### Installing requirements and enabling the template

Installing [pre-commit](https://pre-commit.com/) can be done in a number of ways and
is explained on the [installation page](https://pre-commit.com/#install)

These steps only need to be executed once per developer, per machine,
and should ensure all the repositories you clone benefit from the
same hooks.

Ensure you have pre-commit installed:

    brew install pre-commit
    pre-commit --version

Clone this repo to your local machine:

    mkdir -p ~/gds
    git clone https://github.com/deanwilson/git-template-test.git ~/gds/git-template

Configure `git` to use this template as the basis for all cloned repos.
You can only have one template directory specified so setting this will
remove any custom value you have already assigned:

    git config --global init.templatedir ~/gds/git-template

You can change the paths above to suit your local directory structure as
long as you do it in each command.

### Pre-commit configuration

The base expected `pre-commit` configuration will be present in every new repository created using
the GDS template TODO
[creating a template](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-template-repository).

TODO: there will need to be out of band management to ensure the pre-
commit config can be updated to suit new requirements.

TODO: merge any existing pre-commit configs with the new defaults.

### Testing the hooks

This example shows how the hooks can be invoked and their output viewed.
While it does not need any additional installation to make the
prerequisites above work it does require the repo to have a `.pre-commit-
config.yaml` file to tell `.pre-commit` what to look for.

    # Clone the repo
    cd /tmp
    git clone https://github.com/deanwilson/organisation-graph.git
    cd organisation-graph/

You can now make a `pre-commit` violating change to the code base and
hopefully cause the hook to abort the commit. First we add some trailing whitespace

    echo "   " >> bin/run-neo-docker.sh

If the hooks are working the commit should abort and display a message including:

        Trim Trailing Whitespace.....................Failed

### Warnings and downsides

Once you add `pre-commit` to your git template any repositories that do not contain
a `.pre-commit-config.yaml` file will raise a warning when you attempt to perform a commit.

    $ git commit -v README.md
    No .pre-commit-config.yaml file was found
    - To temporarily silence this, run `PRE_COMMIT_ALLOW_NO_CONFIG=1 git ...`

The willingness to accept this warning is a trade off that will have to
be discussed. On a more positive note the intrusive nature of thie
message means people will be incentivied to add `pre-commit`
configuration to their repositories quite quickly.

## Author

 * [Dean Wilson](https://www.unixdaemon.net) 
