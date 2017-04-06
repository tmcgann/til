It can be bad practice to get into the habit of installing lots of development related packages globally. It's usually better practice to specify packages required by dev projects within the project itself.

One way to help you avoid installing packages globally is to require a virtual environment be active to install any package at all:

```shell
export PIP_REQUIRE_VIRTUALENV=true
```

To make it possible to install packages globally when you _really_ need to just create a separate global function:

```shell
gpip() {
    PIP_REQUIRE_VIRTUALENV="" pip "$@"
}
```

I usually put the following in my `~/.exports` dotfile:

```shell
# pip should only run if there is a virtualenv currently activated
# use gpip if you must install globally
export PIP_REQUIRE_VIRTUALENV=true
gpip() {
    PIP_REQUIRE_VIRTUALENV="" pip "$@"
}
```
