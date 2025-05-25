# How to Update Git Submodules

Since git submodules are separated projects, each of which has their own development line.

This means that if always want to keep the latest version of the submodules, we will need to update then from the repository source (i.e. GitHub).

### Tags

#git #permanent

---

If we encounter in the situation that we are developing a project that includes submodules as dependencies and we want to fetch and merge the updates of the submodules to work up to date, we will need to run the following command:

```sh
git submodules update --remote --merge
```

This process may not be necessary if our project locks the submodule to an specific and trusteed version / commit instead to be always interested in the latest changes. You may be interested to read how to [[2505250135_lock-git-submodules]].
### Sources

- `ChatGPT`