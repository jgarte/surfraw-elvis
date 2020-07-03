# Intro

These are some elvi for sites I find interesting and/or useful.

## Dependencies

### General

* GNU Make
* POSIX-compliant shell and utilities (e.g., `grep`, `tr`, and friends)
* surfraw-tools (from [one of my repos](https://github.com/hoboneer/surfraw-elvis-generator))
* surfraw (required for running the generated elvi, but not for building)

### Additional dependencies for more complex elvi

* GNU Bash (a few elvi use bash as the interpreter for their `.sh-in` file)
* GNU Wget
* HTML Tidy
* HTML-XML-utils

## Quickstart

Make sure `elvi/` exists before doing any of the following commands by running
`mkdir elvi`.

    $ make  # or make elvi

Generate all elvi.  Generated elvi will be placed in `elvi/`.

    $ make install  # or make uninstall

Copy (or delete) elvi to `~/.config/surfraw/elvi`.

    $ make clean

Delete all generated elvi.

    $ make clean-gen

Delete generated data files.

    $ make clean-all

An alias for `make clean clean-gen`.

## Elvi types

### Simple elvi (`.in` extension)

These elvi are generated from simple plaintext files whose contents correspond
to the arguments of `mkelvis`, with line comments.

Some elvi are simpler than others, taking ~3 lines in their `.in` file.  These
are elvi that take no options and serve a similar function as surfraw bookmarks
with embedded "%s".  The arguments usually correspond the basic form described
in the README of `surfraw-tools`, possibly with a `--description=`.

### Complex elvi (`.sh-in` extension)

These may take options, and may have more complex build requirements than other
elvi (e.g., `stack` downloads the list of stackexchange sites and uses it to
populate its enum `-site=` option).  May run arbitrary code when building.
Note: The input files for these elvi are executable, so they may be binary or
be executable scripts with a shebang.

### Extra generated elvi (`.gen-in` extension)

This is a family of elvi whose input files are simple plaintext files similar
to "simple elvi" but require further processing.  These input files are
converted to `.gen-in` files whose contents are the same as that of `.in`
files.  No arbitrary code is run (except the build scripts in `gen-scripts/`
and Makefile recipes).

#### MediaWiki elvi (`.mediawiki-in` extension)

For sites that use MediaWiki.  Provides a boolean `-direct=` option to specify
whether to go straight to a page matching the query.

### Manual elvi (under `manual-elvi/`)

These do not need building as they are written manually (hence the name).
Note: These are not installed by `make install`.
