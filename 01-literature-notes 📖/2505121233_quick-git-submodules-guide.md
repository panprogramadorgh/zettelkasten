# Quick Guide of Git Submodules

### Tags

#literature #git

---
## What is a Git submodule ?

Git submodules is a handy tool provided by git to manage external project dependencies. If a project needs some dependencies which are located on remote GitHub repositories, isn't necessary to manually download and store them within the project's repo at all, we can preferably make a reference to them.

## How to create a submodule

Lets say we have an existing git repository and we have some external utilities that comes from other git repositories (lets also say that external repos comes from GitHub).

It's quite easy to create a new submodule, we only need to use the `git submodule` command as follows.

```sh
git submodule add https://github.com/<user>/<repo> /home/<user>/project/<repo>
```

> That will essentially create a submodule on the current git repository, which links the remote repo with the local location where it will stay.

Then we might create some bash script or something similar to compile the source code from the GitHub or if we are talking about something more Pythonic or JavaScripter, just import the sources as we usually do.

## How to fetch submodules

- **While cloning the repo**

	In order to clone a remote repo and fetch at the same time all Git submodules dependencies we can use the `--recurse-submodules` flag as follows.

```sh
git clone --recurse-submodules https://github.com/<user>/<repo> /home/<user>/project/<repo>
```

- **Already cloned repo**

	Lets say we already have the repository cloned on our machine; in that case we will just execute the two following commands:

```sh
git submodule init
git submodule update
```

> The first one is in charge of updating Git's configuration by reading the `.gitmodules` file; while the second one downloads the sources from the associated URLs.

## How to update submodules

Remember Git submodules are just sub repos, so — if we always want to have the latest changes on our submodules, we have to merge the newest changes against them.

```sh
git submodule update --remote --merge
```

## Lock submodules

Maybe we want the exact opposite philosophy as we did before, maybe we want our submodules to be lock at some specific, tested and trusted version of them, in whose case we would only need to `git switch` and `git commit` — the `.gitmodules` file will simply keep track of what commit were our sub repos checked-out at.

Full example below:

```sh
PRJ="~/code/testing-server"
SUBMOD="https://github.com/panprogramadorgh/serve-express"

cd $PRJ
git submodule add $SUBMOD $PRJ

# We nagivate to the submodule and lock the commit
cd "serve-xpress"
git checkout "71c82fc"
git commit -mS "Locked commit in submodule"
```

Then users that tend to:

```sh
git clone --recurse-submodules https://github.com/panpogramadorgh/serve-express
```

Will get the appropriated version of the `serve-express` Git submodule.

---
### Sources

- `ChatGPT`