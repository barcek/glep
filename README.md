# glep

Grep across multiple git repositories.

Currently runs either `git log` using `--branches=*` and `--oneline`, or `git show`, in each case for all git repositories in the parent directory.

## Why?

For insight and consistency, plus the relevant commit object names and corresponding diffs, either full or filtered.

## How?

The `glep` command takes one or more arguments, the search terms:

```shell
glep <term>[ ...]
```

The default root directory is the parent - `../` - which is set close to the top of the source file. The terms are sought in the output for each each top-level git repo in the root and the matching subset is printed.

The first search term may also be a seven-character hexadecimal commit object name, preceded by the two characters '=#':

```shell
glep =#<name>[ ...]
```

If this is the sole search term provided, the entire diff for that commit is shown. With additional search terms, only the matching subset is printed.

## Script

The script invokes itself and is assumed in doing so to have been made both executable, via a command like `chmod +x glep`, and available from any directory, e.g. by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of AWK, the source code that this is in fact Gawk, and the `git` command that Git itself is installed.
