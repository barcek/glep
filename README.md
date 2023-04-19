# glep

Grep across multiple git repositories.

Returns matching commit log entries or diff lines, or a specific full diff, for all git repositories in the parent directory.

## Why?

For insight and consistency across projects more quickly and simply.

## How?

The `glep` command takes one or more arguments, the search terms:

```shell
glep <term>[ ...]
```

The default root directory is the parent - `../` - which is set close to the top of the source file. The terms are sought for each top-level git repo in the root, by default in the output of `git log` using `--branches=*` and `--oneline`, with the matching log entries printed.

One term may also be a seven-character hexadecimal commit object name, preceded by the two characters '=#':

```shell
glep =#<name>[ ...]
```

If this is the sole search term provided, the entire diff for that commit is shown, per `git show`. With additional search terms, only the matching lines of the diff are printed.

## Script

The script invokes itself and is assumed in doing so to have been made both executable, via a command like `chmod +x glep`, and available from any directory, e.g. by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of AWK, the source code that this is in fact Gawk, and the `git` command that Git itself is installed.
