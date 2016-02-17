After heavily refactoring a Python project (or any compiled project) it helps to "clean and build".

I've done this before using IDE's for C# and Java projects, but for a Python project I've been working on recently, I haven't been using an IDE; just a text editor and the CLI for running tests. I got latest on the project and there were significant changes. As a result, I needed to clear out old files that were making a mess of things (i.e. I could't run my tests via `make test`).

To easily do clear out cached Python files from the CLI, run the following command from the root of the project:

```bash
find . -iname "*.pyc" -exec rm -f {} \;
```

Obviously, this command can be tweaked and used for any file extension.
