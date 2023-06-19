# glep

Grep across multiple git repositories.

Returns matching commit log entries or diff lines, or a specific full diff, for all git repositories in the parent directory.

## Why?

For insight and consistency across projects more quickly and simply.

## How?

The `glep` command takes one or more arguments, the search terms:

```
glep <search_term>[ ...]
```

The default root directory is the parent - `../` - which is set close to the top of the source file. The terms are sought for the root directory, if a git repo, and for each top-level git repo in the root. The search is performed by default in the output of `git log` using `--branches=*` and `--oneline`, with the matching log entries printed.

### Overriding the root

One term may be an alternative root directory, preceded by the two characters '=>':

```
glep =><path_to_root>[ ...]
```

### Filtering by author

One term may also be all or part of the commit author name, preceded by the two characters '=@':

```
glep =@<author_name>[ ...]
```

This will be passed to `git log` with the `--author` flag to filter the results.

### Displaying a diff

One term may instead be a seven-character hexadecimal commit object name, preceded by the two characters '=#':

```
glep =#<object_name>[ ...]
```

If this is the sole search term provided, the entire diff for that commit is shown, per `git show`. With additional search terms, only the matching lines of the diff are printed.

## Source

The script invokes itself and is assumed in doing so to have been made both executable, via a command like `chmod +x glep`, and available from any directory, e.g. by placing it in the '/bin' or '/usr/bin' directory.

The hashbang at the top of the file assumes the presence of AWK in '/usr/bin', the source code that this is in fact Gawk and that several other utils and Git itself are installed. A list can be found close to the top of the file, as well as in the help text.

### Making changes

Running the self-test after making changes plus extending or adding test cases to cover new behaviour is recommended. The self-test is run with the `=test` or `=T` flag (see [Options](#options) below). The test cases are set in the `test_perform` function at the base of the file.

## Options

The following can be passed to `glep` as if a search term:

- `=regexp-extended` / `=e`, to use extended regular expressions in search terms
- `=preview` / `=p`, to show the command for the root directory then exit
- `=version` / `=v`, to show name and version number then exit
- `=help` / `=h`, to show usage, terms and flags then exit
- `=test` / `=T`, to perform the self-test then exit
