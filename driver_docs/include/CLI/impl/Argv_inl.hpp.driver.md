# Purpose
This C++ header file is part of a library developed by the University of Cincinnati, specifically under the CLI namespace, which is likely related to command-line interface utilities. The file is designed to be included in other parts of the library or application, as indicated by the `#pragma once` directive, which prevents multiple inclusions. The file includes several standard C++ libraries such as `<algorithm>`, `<memory>`, `<stdexcept>`, `<string>`, and `<vector>`, which suggests that it provides functionality that involves string manipulation, memory management, and exception handling. The file also includes platform-specific code for Windows, which is used to parse command-line arguments into a vector of strings. This is achieved through the [`compute_win32_argv`](#string>compute_win32_argv) function within the `detail` namespace, which utilizes Windows API functions like `CommandLineToArgvW` and `GetCommandLineW`.

The primary purpose of this file is to handle command-line argument parsing on Windows platforms, converting wide-character command-line arguments into a more manageable vector of strings. This functionality is encapsulated within the `CLI::detail` namespace, indicating that it is intended for internal use within the library rather than as a public API. The file also includes conditional compilation directives to ensure compatibility with different Windows architectures, such as AMD64, X86, ARM, and ARM64. This careful handling of platform-specific details ensures that the library can be used across various Windows environments, making it a crucial component for applications that rely on command-line input.
# Imports and Dependencies

---
- `../Argv.hpp`
- `../Encoding.hpp`
- `algorithm`
- `memory`
- `stdexcept`
- `string`
- `vector`
- `windef.h`
- `winbase.h`
- `processthreadsapi.h`
- `shellapi.h`


# Functions

---
### compute\_win32\_argv<!-- {{#callable:CLI::detail::std::vector<std::string>::compute_win32_argv}} -->
The `compute_win32_argv` function retrieves and converts the command-line arguments of a Windows application from wide-character format to a vector of standard strings.
- **Inputs**: None
- **Control Flow**:
    - Initialize an empty vector of strings named `result` to store the command-line arguments.
    - Declare an integer `argc` to hold the number of command-line arguments.
    - Define a custom deleter lambda function to free memory allocated for the wide-character argument array using `LocalFree`.
    - Use `CommandLineToArgvW` to parse the command line into an array of wide-character strings, storing the result in a unique pointer `wargv` with the custom deleter.
    - Check if `wargv` is `nullptr`, and if so, throw a runtime error with the last error code from `GetLastError`.
    - Reserve space in the `result` vector for `argc` number of elements.
    - Iterate over each wide-character argument in `wargv`, convert it to a narrow string using `narrow`, and append it to the `result` vector.
    - Return the `result` vector containing the converted command-line arguments.
- **Output**: A `std::vector<std::string>` containing the command-line arguments of the application, converted from wide-character to standard string format.


