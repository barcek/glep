# glep

Grep across multiple git repos.

Currently runs `git log`, using `--branches=*` and `--oneline`, for all git repos in the parent directory.

## Why..?

For insight and consistency and relevant commit hashes.

## How..?

The `glep` command takes one argument, the search term:

```shell
glep <term>
```

The default root directory is the parent - `../` - set close to the top of the source file. The term is sought in the output for each each top-level git repo in the root and the matching subset is printed.

## Script

The script invokes itself and is assumed in doing so to have been made both executable, via a command like `chmod +x glep`, and available from any directory, e.g. by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of AWK, the source code that this is in fact Gawk, and the `git` command that Git itself is installed.
