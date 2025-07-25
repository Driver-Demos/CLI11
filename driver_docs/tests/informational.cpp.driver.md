# Purpose
This C++ code is an executable program designed to display information about the CLI11 library, a command-line interface library for C++. It provides narrow functionality, specifically focusing on outputting details about the C++ standard being used, the availability of the `__has_include` feature, and the support for various optional libraries (such as `std::optional`, `std::experimental::optional`, and `boost::optional`). The code conditionally includes the appropriate header file based on whether `CLI11_SINGLE_FILE` is defined, indicating flexibility in how the library is integrated. This program is primarily intended for diagnostic or informational purposes, helping developers understand the configuration and capabilities of the CLI11 library in their current build environment.
# Imports and Dependencies

---
- `CLI11.hpp`
- `CLI/CLI.hpp`
- `iostream`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function outputs information about the C++ standard version, availability of the `__has_include` feature, and support for various optional libraries in the CLI11 library.
- **Inputs**: None
- **Control Flow**:
    - Prints a header 'CLI11 information:'.
    - Checks and prints the C++ standard version being used (C++20, C++17, C++14, or C++11) based on preprocessor directives.
    - Checks if the `__has_include` feature is available and prints 'yes' or 'no'.
    - Checks for the availability of optional library support in CLI11 and prints the corresponding message for CLI::optional, std::optional, std::experimental::optional, and boost::optional based on preprocessor directives.
    - Prints a newline at the end.
- **Output**: The function outputs a series of informational messages to the standard output (console) regarding the C++ standard version and optional library support.


