## Project templates for Stack

From Stack 1.9.1, Stack allows any GitHub, GitLab or Bitbucket repository named
`stack-templates` to provide project templates for Stack. For example, a
template file at `username/stack-templates/my-template.hsfiles` on GitHub can be
identified as `username/my-template` when using `stack new`. For more
information see the output of the `stack templates` command and its
[documentation](https://docs.haskellstack.org/en/stable/templates_command/).

This repository provides the project template `new-template`, which is the
default template used by `stack new`. It also provides `STACK_HELP.md`, which
specifies the output of the `stack templates` command.

This repository is the default one used by Stack and it provides 24 other
project templates. Information about some of those templates is included in
`template-info.yaml` and this repository's Wiki.

Those project templates are maintained but this repository is not accepting new
templates because of the difficulties in maintaining large numbers of templates
centrally.

This repository's Wiki provides a place where the Haskell community can
announce the availability of project templates at other locations.

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

When the user runs `stack new my-project username/your-template` and they do not
have the parameters provided in their Stack `config.yaml`, Stack will warn the
user that such parameters were missing, like this:

```
Downloading template username/your-template to create project my-project in
directory my-project/ ...
Downloaded <path_to_username/your-template.hsfiles>.

Note: The following parameters were needed by the template but not provided:
      author-email, and author-name.

      You can provide them in Stack's global YAML configuration file
      (<path_to_config.yaml>) like this:

      templates:
        params:
          author-email: value
          author-name: value

      Or you can pass each one on the command line as parameters like this:

      stack new my-project username/your-template -p "author-email:value"
      -p "author-name:value"
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

## Yesod templates

The Yesod templates are generated from the
[yesod-scaffold repo](https://github.com/yesodweb/yesod-scaffold). Please
send pull requests for those templates to that repository instead of this one.
