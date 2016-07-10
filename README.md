# Fuchsia Manifest

Contains the jiri manifests for Fuchsia.

## Creating a new checkout

Fuchsia uses the `jiri` tool to manage repositories
[https://github.com/vanadium/go.jiri](https://github.com/vanadium/go.jiri).
This tool manages a set of repositories specified by a manifest.  The bootstrap
procedure requires that you have Go 1.4 or newer and Git installed and on your
PATH.  To create a new Fuchsia checkout in a directory called `fuchsia` run the
following commands. The `fuchsia` directory should not exist before running
these steps.

```
curl -s https://raw.githubusercontent.com/vanadium/go.jiri/master/scripts/bootstrap_jiri | bash -s fuchsia
cd fuchsia
export PATH=`pwd`/.jiri_root/scripts:$PATH
jiri import fuchsia https://fuchsia.googlesource.com/manifest
jiri update
```

## Submitting changes

To submit a patch to Fuchsia, you may first need to generate a cookie to
authenticate you to GoogleSource (you know this is necessary if ```jiri cl mail```
prompts you for a username/password).  To generate a cookie, log into
GoogleSource and click the "Generate Password" link at the top of
https://fuchsia.googlesource.com. Then, copy the generated text and execute it
in a terminal.

Once authenticated, follow these steps to submit a patch to Fuchsia:

```
# create a new change (makes a new local branch, checks it out)
jiri cl new branch_name

# write some awesome stuff, commit to branch_name
vim some_file ...
git commit ...

# upload the patch to gerrit
jiri cl mail

# once the change is landed, clean up the branch
jiri cl cleanup branch_name
```
