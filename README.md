# DVerse Project Documentation

View this [book](https://fuas-dverse.github.io).

To contribute to this book create a PR.

## Developers

Clone this project.

Install [babashka](https://github.com/babashka/babashka#installation).

For local development of the book install Python and Mkdocs.

``` shell
pip install -r requirements.txt
```

To see a list of avaliable tasks run `bb tasks`.

Build and serve a local site. It's better to run `bb serve` which does
not generate the full site.

``` shell
bb build
scripts/serve-site --port 1234 --dir site
```

To run the linter (`bb lint`) you must have Docker engine running.
