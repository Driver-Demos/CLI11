# Purpose
This C++ source code file is an example program demonstrating the use of the CLI11 library, specifically focusing on handling retired and deprecated command-line options. The program is structured around a [`main`](#main) function, which is typical for executable files, and it utilizes the CLI11 library to define and manage command-line options. The primary technical components include the creation of a `CLI::App` object to represent the application, and the use of methods such as `add_option`, `retire_option`, and `deprecate_option` to manage the lifecycle of command-line options. The code illustrates how to mark options as retired, making them non-functional, and how to deprecate options by suggesting alternative options to users.

The file serves as a practical guide for developers on how to handle deprecated and retired options in command-line applications using CLI11. It defines a public API through the command-line interface, allowing users to interact with the application by passing arguments. The example includes options that are retired, deprecated, and active, showcasing how to transition options gracefully without breaking existing user workflows. The program also includes logic to process and display the values of non-deprecated options, providing a complete example of managing command-line inputs in a C++ application.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `utility`
- `vector`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function demonstrates the usage of retired and deprecated options in a command-line interface application using the CLI11 library.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application with the description 'example for retired/deprecated options'.
    - Declare a vector `x` to store integer values associated with options.
    - Add an option `--retired_option2` to the app, storing its values in `x`.
    - Declare a pair `y` to store two integer values associated with options.
    - Add an option `--deprecate` to the app, storing its values in `y`.
    - Add an option `--not_deprecated` to the app, storing its values in `x`.
    - Retire a non-existing option `--retired_option` using `CLI::retire_option`.
    - Retire the existing option `--retired_option2` using `CLI::retire_option`, making it non-functional.
    - Deprecate the existing option `--deprecate` and recommend `--not_deprecated` as a replacement using `CLI::deprecate_option`.
    - Parse the command-line arguments using `CLI11_PARSE`.
    - If `x` is not empty, print the values received for `--not_deprecated`.
    - If no arguments are received, print a message indicating no arguments were received.
- **Output**: The function returns an integer value `0`, indicating successful execution.


