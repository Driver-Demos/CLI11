# Purpose
This C header file is part of the CLI11 library, which is a command-line interface parser for C++ applications. The file primarily defines a set of preprocessor macros that facilitate compatibility and feature detection across different C++ standards and compiler environments. It includes macros for determining the C++ standard version being used (e.g., C++14, C++17, C++20), and it sets up conditional compilation based on these standards. This allows the library to leverage newer C++ features when available, such as `[[nodiscard]]` and `[[deprecated]]` attributes, while maintaining compatibility with older standards.

Additionally, the file includes macros for detecting the availability of certain C++ standard library features, such as `<filesystem>` and `<codecvt>`, and for handling runtime type information (RTTI) support. It also provides mechanisms to suppress deprecation warnings across different compilers, ensuring that the library can be used without generating unnecessary warnings. The use of `#pragma once` indicates that this is a header file intended to be included in other source files, and the presence of the `IWYU pragma` suggests that it is designed to be used with the "Include What You Use" tool to manage dependencies efficiently. Overall, this file is crucial for ensuring that the CLI11 library can be used in a wide range of development environments with varying levels of C++ standard support.
# Imports and Dependencies

---
- `filesystem`
- `codecvt`


