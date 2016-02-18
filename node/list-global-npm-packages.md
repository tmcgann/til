By default, `npm ls` shows the installed dependencies for your current package. If you want to see a flat tree or list of global dependencies, you need to run something like this:

```bash
npm ls -g --depth=0
```

You can include any of the config flags listed [here](https://docs.npmjs.com/cli/ls) to modify the output. `--depth=0` is an example of one of those configurations.
