## Status

This repository is not accepting new templates. See
[Stack documentation](https://docs.haskellstack.org/en/stable/GUIDE/#templates)
for instructions on providing templates to your users, for example, by
publishing them on GitHub or an arbitrary URL.

[![Build Status](https://travis-ci.org/commercialhaskell/stack-templates.svg?branch=master)](https://travis-ci.org/commercialhaskell/stack-templates)

## Project template format

Each project template is specified in an `.hsfiles` file, using the syntax of
the [Mustache](https://mustache.github.io/mustache.1.html) tool.

Each file to be generated by the project template is specified with
`START_FILE`, like this:

```
{-# START_FILE {{name}}.cabal #-}
name:                {{name}}
version:             0.1.0.0
...
```

Parameters to the template are written `{{foo}}`. They are provided by users via
their Stack `config.yaml` file, like this:

``` yaml
templates:
  params:
    author-email: chrisdone@gmail.com
    author-name: Chris Done
    copyright: 2022 Chris Done
    github-username: chrisdone
    category: Development
```

When the user runs `stack new myproject yourtemplate` and they do not have the
parameters provided in their Stack `config.yaml`, Stack will warn the user that
such parameters were missing, like this:

```
Downloading template "yourtemplate" to create project "myproject" in myproject/ ...

The following parameters were needed by the template but not provided: author-email, author-name
You can provide them in <path to config.yaml>, like this:
templates:
  params:
    author-email: value
    author-name: value
Or you can pass each one as parameters like this:
stack new myproject yourtemplate -p "author-email:value" -p "author-name:value"
```

The output of the template will yield a blank space where your parameter was. If
you want to provide default values for your template parameters, use this
Mustache syntax:

```
author:              {{author-name}}{{^author-name}}Author name here{{/author-name}}
```

## Related initiatives

The repository https://github.com/prikhi/stack-templatizer (unconnected with
this repository) provides Haskell source code to build an application that
will generate an `.hsfiles` file from the contents of a folder.

## `template-info.yaml`

When contributing a new template, please remember to add a corresponding entry
to `template-info.yaml`. Additional descriptive information for the template may
be provided, but is not required.

## Yesod templates

The Yesod templates are generated from the
[yesod-scaffold repo](https://github.com/yesodweb/yesod-scaffold). Please
send pull requests for those templates to that repository instead of this one.
