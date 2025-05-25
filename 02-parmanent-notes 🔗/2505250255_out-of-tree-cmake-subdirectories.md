# What's a Out-Of-Tree Subdirectory in CMake ?

The compilation tool CMake, doesn't allow by default to add a compilation subdirectory that doesn't belong to the project tree. 

### Tags

#cmake #permanent

---

## Concepts

We consider a CMake subdirectory to be out of the project tree when the project's and subdirectory's `CMakeLists.txt` have a non-common ancestor — parent directory. 

We call a CMake compilation subdirectory a filesystem directory that contains a `CMakeLists.txt` which is, in turn, referred by some project, where

A CMake project is a filesystem directory that contains a `CMakeLists.txt` file that internally calls the `project(<name>)` CMake command to define a new project.

## Example

Lets provide an example in sake of clarity.

```
better_vnc/
..vnc_server/
....CMakeLists.txt
....src/
......CMakeLists.txt
......vnc_core.cpp
....examples/
......CMakeLists.txt
......simples.cpp
..sources/
....CMakeLists.txt
....wrapper.cpp
..compile.sh
```

This is the files structure of an example VNC wrapper library that suggests what files may contain, being the `vnc_server` directory a [git submodule](25051238_git-submodules) — which is in charge of providing the core functionality layer.

> Since `vnc_server` is a git submodule that regards to an external tool, its CMake compilation script should be considered as a separated CMake project.

### Next Steps

- [[2505250304_how-to-handle-out-of-tree-cmake-subdirectories]]