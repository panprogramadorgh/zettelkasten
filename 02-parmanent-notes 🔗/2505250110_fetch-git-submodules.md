# How to Fetch Git Submodules

As well as git submodules allows us to easily manage dependencies for your project on other repositories, maybe the submodules' directories aren't physically in disk (we only have a reference to the external git repositories but their files aren't materialized). This is why we first need to fetch the submodules before staring consuming them.

### Tags

#git #permanent

---

## References

- [[25051238_git-submodules]]
- [[2505251245_create-git-submodules]]

## Fetching in Different Contexts

**While cloning the repo**
In order to clone a remote repo and fetch at the same time all Git submodules dependencies we can use the `--recurse-submodules` flag as follows:

```sh
git clone\

# Fetches the submodules
--recurse-submodules\

# Remote submodule's repository
https://github.com/$GH_USER/$REPO_NAME\

# Local path where the repo will be located
/path/to/my/repo
```

**After the repo was cloned**
Lets say we already have the repository cloned on our machine; in that case we will just execute the two following commands:

```sh
git submodule init
git submodule update
```

> The first one is in charge of updating Git's configuration by reading the `.gitmodules` file; while the second one downloads the sources from the associated URLs.

If you prefer both actions in one line we can execute:

```sh
git submodule update --init --recursive
```

### Sources

- `ChatGPT`