# Out Of Tree Subdirectories in CMake

### Tags

#programming #cmake #literatue

---

## Introduction

The compilation tool CMake, doesn't allow by default to add a compilation subdirectory that doesn't belong to the project tree. 
- We consider a CMake subdirectory to be out of the project tree when the CMake project's CMakeLists.txt file is deeper in the filesystem than the subdirectory we want to add, and
- We call a CMake compilation subdirectory a filesystem subdirectory that contains a `CMakeLists.txt` which is, in turn, referred by some project, where
- A CMake project is a filesystem directory that contains a `CMakeLists.txt` file which internally executes the `project(<name>)` CMake function to "define" a project.

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

This is the files structure of an example VNC wrapper library that suggests what files may contain, being the `vnc_server` directory a [git submodule](2505121233_quick-git-submodules-guide) — which is in charge of providing the core functionality layer.

> Since `vnc_server` is a git submodule that regards to an external tool, its CMake compilation script should be considered as a separated CMake project.

This is how `./better_vnc/sources/CMakeLists.txt` might look like — if we idealize the example:

```cmake
# The minimum cmake version required
cmake_minimum_required(VERSION 3.10)

# The project's name
project(BetterVNC)

# Variables
set(TARGET "betvnc")
set(TARGET_SRC "./sources/wrapper.cpp")
set(VNCSERV_SUB "./vnc_server/CMakeLists.txt")

# We crate the executable
add_executable(${TARGET} ${TARGET_SRC})

# And link de subdirectory
add_subdirectory(${VNCSERV_SUB}) # <- might create some target like a library to be linked to the exexuteable
```

Independently of what content does `${VNCSERV_SUB}` contain — whether it actually generates a target to be linked with `${TARGET}` or not, if CMake wouldn't prevent us to add out-of-tree subdirectories, the underlaying reasoning could even be considered as valid.

We will notice CMake applies restrictions regarding to this out-of-tree approach when running the `./compile.sh` shell script — which is ultimately in charge of running the CMake and Make compilation tools.

```sh
cd ./better_vnc
mkdir -p ./build && cd ./build
cmake ../sources
make -j
```

![cmake-out-of-tree-error](cmake-out-of-tree-error.png)

> An image of a real project with this problem.
## Quickest solution

If we are working in a testing project and we eventually need to add the subdirectory that doesn't belong to the "project tree" we can set the following two name-reserved CMake variables as follows: 

```cmake
set(CMAKE_POLICY_DEFAULT_CMP0077 NEW)
set(CMAKE_ALLOW_LOOSE_LOOP_CONSTRUCTS TRUE)
```

This method isn't recommended for real projects since it might lead to relative path references, compilation and installation errors in the future.

## Best practice

The best method we can use if we encounter in this situation would be to crate a copy of the out-of-tree subdirectory that we want to make reference to at the same level our project's `CMakeList.txt` is located.

The simples way we can do so would be through a CMake command that invokes the copy command from CMake for better portability.

In order to ease the process of coping a directory, we can create a custom CMake routine like in the following example:

```cmake
function(add_dir_copy_target TARGET_NAME SRC DST)
    add_custom_command(
        OUTPUT ${DST}
        COMMAND ${CMAKE_COMMAND} -E copy_directory ${SRC} ${DST}
        COMMENT "Coping directory '${SRC}' to '${DST}'"
        DEPENDS ${SRC}
        VERBATIM
    )

    add_custom_target(
        ${TARGET_NAME}
        DEPENDS ${DST}
        COMMENT "Target '${TARGET_NAME}' for directory copy"
    )
endfunction()
```

This routine allows to create a target that in turn depends on the execution of a CMake custom command in charge of coping the source directory.

We have to recall that CMake custom targets, unlike traditional targets, doesn't really generate files, instead we can use them as a dependency-creation tool like follows:

```cmake
add_executable(main main.cpp)

add_copy_dir_target(CopyDir ${CMAKE_SOURCE_DIR}/test_dir ${CMAKE_BINARY_DIR}/new_dir)

add_dependencies(main CopyDir)
```

