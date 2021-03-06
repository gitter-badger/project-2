# `project` - automate initial project setup [![Circle CI](https://circleci.com/gh/nildev/project/tree/master.svg?style=svg&circle-token=5f985f466e03e2f89df778c37ff6c6ab0b370a09)](https://circleci.com/gh/nildev/project/tree/master)

## Why ?

Whenever I need to setup new *Golang* project I find myself copy/pasting from previous one. To save some time for myself
I've created this `project` cli app. 

# How it works

This cli app has one command `setup` which takes 3 arguments:

 - `destDir` specifies where new project should be created
 - `templateRepo` is git repository which hosts project template
 - `configFile` has all variable values that should be applied on template

Once you run it:

```
project setup --destDir=$GOPATH/src/github.com/nildev/my-new-app --configFile=./newapp.config.json --templateRepo="git@github.com:nildev/prj-tpl-cli-app.git"
```

`project` will clone `templateRepo` in `destDir` will remove `.git` dir and will start iterating over the files and directories
searching for {{.Variable}}'s and replacing them with values from `configFile`.

# How to use

## Prerequisites
 
Make sure `git` is installed and required private keys are added to ssh agent. To add private key:

```
# If your private key is located at ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa
```

## Install

Download binary from [here](https://github.com/nildev/project/releases) or `go get`:

```
go get github.com/nildev/project
```

## Project templates

Using Golang template [syntax](https://golang.org/pkg/text/template/) prepare your project template, for example take a look at [this one](https://github.com/nildev/prj-tpl-cli-app).
Or use one of already prepared [templates](https://github.com/nildev/project#available-templates).

Then create `project.json` file locally with values for each variable that is defined in config file. Every project template
in root directory will contain `project.sample.json` with all available variables. 

For example like this [one](https://github.com/nildev/prj-tpl-cli-app/blob/master/project.config.json):

```
{
  "GitRepoFullPath": "https://github.com/your_org/your_project_name",
  "DocsGitRepoFullPath": "https://github.com/your_org/docs",
  "OrgPath":"github.com/your_org",
  "BinaryName" : "your_project_binary_name",
  "ProjectName" : "your_project_name",
  "BinaryDescription" : "Some description of your app",
  "Org": "your_org"
}
```

## Generate new project

- replace $PATH_TO_NEW_PROJECT with path to directory where newly generated project should be created
- replace $PATH_TO_CONFIG_JSON with path to json file you have created locally
- replace $PATH_TO_TEMPLATE_REPO to project template git repository for example `git@github.com:nildev/prj-tpl-cli-app.git`

Run:
```
project setup --destDir=$GOPATH/src/github.com/nildev/newapp --configFile=./newapp.config.json --templateRepo="git@github.com:nildev/prj-tpl-cli-app.git"
```

## Template in private repository

If template is in private repository make sure that required ssh key is added to ssh agent.

# Available templates

Here is a list of available templates.
If you have created one please do a pull request with link to that repository:

 * https://github.com/nildev/prj-tpl-cli-app (`git@github.com:nildev/prj-tpl-cli-app.git`)

# Building from source

1) Get repo

```
go get github.com/nildev/project
```

2) Restore deps

```
godep restore 
```

3) Run `build`

```
./build
```

## Project Details

### Release Notes

See the [releases tab](https://github.com/nildev/project/releases) for more information on each release.

### Contributing

See [CONTRIBUTING](CONTRIBUTING.md) for details on submitting patches and contacting developers via IRC and mailing lists.

### License

project is released under the Apache 2.0 license. See the [LICENSE](LICENSE) file for details.

Specific components of project use code derivative from software distributed under other licenses; in those cases the appropriate licenses are stipulated alongside the code.