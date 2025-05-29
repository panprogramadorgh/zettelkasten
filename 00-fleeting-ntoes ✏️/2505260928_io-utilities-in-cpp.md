# Input / Output Utilities in The C++ Programming Language

Next we will be exposing the main input / output utilities that we can we in the C/C++ programming language.
### Tags

#programming #literature

---

Okay, no problem at all. Here's the same response again, but in English:

## Classification of Input/Output Utilities in C by Abstraction Level

We can classify the input/output (I/O) utilities in C into three main levels of abstraction:

**1. Low-Level (I/O via File Descriptors):**

- **Abstraction:** This level interacts directly with the operating system through file descriptors (non-negative integers that represent open files, sockets, etc.). It provides the most direct control over I/O operations.
- **Main Functions:**
    - `open()`: Opens or creates a file and returns a file descriptor.
    - `close()`: Closes a file descriptor.
    - `read()`: Reads data from a file descriptor.
    - `write()`: Writes data to a file descriptor.
    - `lseek()`: Repositions the read/write pointer within a file.
    - `fcntl()`: Performs various control operations on a file descriptor.
    - `ioctl()`: Performs device-specific operations.
- **Header:** `<fcntl.h>` (for `open`, `fcntl`), `<unistd.h>` (for `close`, `read`, `write`, `lseek`, `ioctl`).

**2. Stream Level (Buffered I/O):**

- **Abstraction:** This level provides a more abstract and convenient interface for I/O, using the concept of "streams." Streams act as intermediaries between the program and the operating system, offering buffering functionalities to improve efficiency.
- **Main Functions:**
    - `fopen()`: Opens a file and associates a stream with it.
    - `fclose()`: Closes a stream and releases the associated buffer.
    - `fread()`: Reads data from a stream (in blocks).
    - `fwrite()`: Writes data to a stream (in blocks).
    - `fgetc()`: Reads a character from a stream.
    - `fputc()`: Writes a character to a stream.
    - `fgets()`: Reads a line from a stream.
    - `fputs()`: Writes a string to a stream.
    - `fprintf()`: Writes formatted data to a stream.
    - `fscanf()`: Reads formatted data from a stream.
    - `fflush()`: Forces the flushing of a stream's buffer.
    - `fseek()`, `rewind()`, `ftell()`: Manipulate the position within a stream.
- **Header:** `<stdio.h>`

**3. High-Level Stream (Formatted I/O):**

- **Abstraction:** This level builds upon streams and adds functionalities to format input and output data according to specifications. The `printf` and `scanf` functions are the most common examples.
- **Main Functions:**
    - `printf()`: Writes formatted data to the standard output stream (`stdout`).
    - `scanf()`: Reads formatted data from the standard input stream (`stdin`).
    - `fprintf()` and `fscanf()` (already mentioned at the stream level, but with a focus on formatting).
    - `sprintf()`: Writes formatted data to a character string.
    - `sscanf()`: Reads formatted data from a character string.
    - `vprintf()`, `vfprintf()`, `vsprintf()`: Versions of the above functions that take a variable argument list (`va_list`).
- **Header:** `<stdio.h>` and `<stdarg.h>` (for functions with variable argument lists).

## File Handling Implementation in C++

Yes, **the C++ standard library provides its own implementations for file handling**, which are generally preferred over the C interfaces because they are more object-oriented and offer better type safety.

The main classes for file handling in C++ are found in the `<fstream>` header:

- `std::ofstream` (output file stream): Used for writing data to files.
- `std::ifstream` (input file stream): Used for reading data from files.
- `std::fstream` (file stream): Used for both reading and writing to files.

These classes provide methods such as:

- `open()`: Opens a file.
- `close()`: Closes a file.
- `read()`: Reads raw blocks of data.
- `write()`: Writes raw blocks of data.
- The insertion operator (`<<`) for writing formatted data.
- The extraction operator (`>>`) for reading formatted data.
- `getline()`: Reads a line from a file.
- `seekg()`: Sets the position of the read pointer in an input stream.
- `seekp()`: Sets the position of the write pointer in an output stream.
- `tellg()`: Gets the current position of the read pointer.
- `tellp()`: Gets the current position of the write pointer.

In addition to `<fstream>`, the `<iostream>` header also provides standard objects for input and output, such as `std::cin`, `std::cout`, `std::cerr`, and `std::clog`, although these are more oriented towards standard I/O (console) rather than direct file manipulation. However, the base classes of `<fstream>` (like `std::istream` and `std::ostream`) are defined in `<iostream>`.

**In summary, although C++ can use the C I/O functions (included when linking with the C standard library), the idiomatic and recommended way to handle files in C++ is through the classes provided in the `<fstream>` header.** These classes offer a safer, more object-oriented, and often more convenient interface for file management in C++.
### Sources

- `Google Gemini`