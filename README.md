A setup for doing git operations across many repos using `git submodule
foreach`.

```console
$ git submodule foreach git fetch origin
$ git submodule foreach git checkout origin/master
$ sed -i s/…/…/ */*/.github/workflows/*.yml
$ git submodule foreach git commit -am "…"
$ git submodule foreach git push origin HEAD:master
```

The variables defined by git for the command are:

- `$name` &mdash; name of the submodule section in .gitmodules. Here, this is
  set to the repo name, e.g. "syn".

- `$sm_path` &mdash; path of the submodule as recorded in the superproject. This
  is the repo's user+name, e.g. "dtolnay/syn" or "serde-rs/json".

- `$displaypath` &mdash; relative path from the current working directory to the
  submodule's root directory.

- `$sha1` &mdash; commit as recorded in the superproject.

- `$toplevel` &mdash; absolute path to the top-level of the superproject:
  "/path/to/foreach".

Useful flags:

- `--quiet` &mdash; Unless given --quiet, foreach prints the name of each
  submodule before evaluating the command.

A non-zero return from the command in any submodule causes the processing to
terminate. This can be overridden by adding `|| :` to the end of the command.
