
# How to Create a Git Submodule

Create a new git submodule isn't quite hard and provides us lots of benefits. We only need to use the `submodule` command from git.

### Tags

#git #permanent

---

### References

Still don't know what's a git submodule ? Check out [[25051238_git-submodules]].

## Tutorial

Lets say we have an existing git repository and we have some external utilities that comes from other git repositories (lets also assume they come from GitHub).

As mentioned before, git includes a subcommand called `submodule` which allows us to manage the git submodules of a repository.

For instance we can define a new submodule as follows:

```sh
git submodule add\

# Remote git repository
https://github.com/$GH_USER/$GH_REPO\

# The path where we want the submodule to be located inside our project
/path/to/submodule
```

> That will essentially create a submodule on the current git repository that links the remote repo with the local path.

Then we might create some bash script, CMake subdirectory or something similar to compile the source code — or if we are talking about a interpretated programming language, just import the sources from the submodule's directory.

### Sources

- `ChatGPT`