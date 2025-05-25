# How to Lock Git Submodules

Whether our project consumes an specific version of a submodule because the latest version isn't stable, contains bugs or it just introduces changes with entailments; lock them to an specific version (tag / commit) is what a wise decision!

### Tags

#git #permanent

---

### References

Articles before we saw how to keep always the latest changes of our submodules up to date ([[2505250203_update-git-submodules]]).

## Tutorial

However today we will learn how to implement the exact opposite philosophy, that is, how to lock submodules to specific and trusted versions / commits of them. 

We would only need to `git checkout` and `git commit` — the `.gitmodules` file will simply keep track of what commit were our sub repos checked-out at.

Full example below:

```sh
PRJ="~/code/testing-server"
SUBMOD="https://github.com/panprogramadorgh/serve-express"

cd $PRJ
git submodule add $SUBMOD $PRJ

# We nagivate to the submodule, checkout the exact commit we want and commit our project to ensure all contributors work with the same version of the submodule. 
cd "serve-xpress"
git checkout "71c82fc"
cd ..
git commit -S -m "Locked submodule"
```

Then users that tend to:

```sh
git clone --recurse-submodules https://github.com/panpogramadorgh/serve-express
```

Will get the appropriated version of the `serve-express` Git submodule.

> The exact same approach we did with the commits / tags is also applicable to different repository's branches.

### Sources

- `ChatGPT`