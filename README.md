# pdiffjson

- [`pdiffjson`](pdiffjson) is a simple bash script that’s non-obvious and useful enough more developers
  should have it at their fingertips.
  It simply combines `jq`, `diff`, `colordiff`, and `less` to normalize and then diff.
- Not a fancy web UI or a library.
  Just the simplest and fastest way to get clear, pretty-printed, colored diffs of JSON
  files on a console.
  Ignores all irrelevant whitespace and key ordering on collections objects (and ordering on
  arrays altogether, if you like) only shows you significant differences.
- Works on large files other tools barf on, thanks to `jq`’s speed.
- Shows context around each difference in a customizable way, thanks to `diff`.
- Scrollable and searchable output (use space, `/`), thanks to `less`.
- Installs quickly anywhere, thanks to `npm`.
- Extra bonus [`pjson`](pjson) command that colorizes and pretty-prints only.
- *The feature list is longer than the code!*
  🤯😀

![example usage](images/example.gif)

## Installation

```bash
$ npm install -g pdiffjson
```

Or copy `pjson` and `pdiffjson` to `/usr/local/bin` by hand!
Ensure you have `jq` and `colordiff` as well (`brew install jq colordiff` on Mac).

## Usage

    $ pdiffjson
    Usage: pdiffjson [--sort-arrays] [diff options] file1.json file2.json

    Show pretty-printed, colored diff of normalized JSON. Uses less to
    paginate the output. Allows a readable diff of any JSON, ignoring all
    non-semantic differences of whitespace and key ordering.

    Fields of each object are output with the keys in sorted order
    prior to calling diff, so insignificant differences of key order
    are ignored. The --sort-arrays option also enables recursive sorting
    of all array values, so all differences in ordering within arrays
    are ignored.

    This is a "semi-structural diff", meaning it shows only structural
    (semantic) changes but the diff is shown syntactically on JSON output,
    which actually makes it more readable and flexible than a true
    structural diff.

    Works on large files since it relies only on diff and jq.

    By default calls diff without arguments, yielding a unified diff. But
    it can be helpful to add standard diff arguments to refine the type of
    output, such as:
    -c (contextual diff),
    -C2 (contextual diff with two lines of context), or
    -U5 (unified diff with 5 lines of context).

    $

## Related Work

- [Many websites](https://www.google.com/search?q=json+diff) like
  [jsondiff](https://github.com/zgrossbart/jdd) offer JSON diff functionality but offer no
  command line, don’t work on large files, and are not good for sensitive data.
- [jsondiffpatch](https://github.com/benjamine/jsondiffpatch) is a powerful JavaScript library
  to do JSON diff and patch.
  Has a command line.
  Shows a pure structural diff.
  No semi-structured diff with context.
- [diff-json](https://github.com/andreyvit/json-diff) is another useful JavaScript library with
  a command-line interface.
  Rather slow on larger (multi-megabyte) files, with no incremental output.
- [jd](https://github.com/josephburnett/jd) is a powerful Go command line tool.
  It handles diff and patching.
  It allows more flexible diffs options on arrays (set and bag).
  No colored output or diff output options to show more context, as with diff, so the output
  seems less clear to read.
