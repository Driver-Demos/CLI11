# Purpose
This C++ source code file demonstrates the implementation of a custom lexical cast function within the context of a command-line interface application using the CLI11 library. The primary purpose of this file is to showcase how to extend the CLI11 library's functionality by defining a custom conversion function that can interpret command-line input and convert it into a user-defined data structure. The code defines a template struct `Values` that holds three values of a generic type, and a specific instantiation `DoubleValues` for `double` types. The custom [`lexical_cast`](#lexical_cast) function is designed to work with `Values<double>`, and it is placed in the same namespace to ensure proper argument-dependent lookup (ADL).

The file includes a [`main`](#main) function that sets up a CLI11 application, adds a command-line option group, and associates the `--dv` option with the `DoubleValues` instance. The [`argparse`](#argparse) function is responsible for adding this option to the application, with a default string value of "0". The code is structured to be an executable, as indicated by the presence of the [`main`](#main) function, and it serves as an example of how to integrate custom data parsing into a CLI application. The file does not define public APIs or external interfaces beyond the command-line options it configures, focusing instead on demonstrating the integration of custom parsing logic within the CLI11 framework.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `sstream`
- `string`


# Global Variables

---
### doubles
- **Type**: `DoubleValues`
- **Description**: The variable `doubles` is an instance of the `DoubleValues` type, which is a typedef for the `Values` struct template specialized with `double`. This struct contains three double-precision floating-point members: `a`, `b`, and `c`. The `doubles` variable is used to store and manage these three double values.
- **Use**: The `doubles` variable is used in the `argparse` function to add a command-line option `--dv` that can be set by the user, with a default string value of "0".


# Data Structures

---
### Values<!-- {{#data_structure:Values}} -->
- **Type**: `struct`
- **Members**:
    - `a`: A member of type T, defaulting to int, representing a value in the structure.
    - `b`: A member of type T, defaulting to int, representing a value in the structure.
    - `c`: A member of type T, defaulting to int, representing a value in the structure.
- **Description**: The `Values` struct is a templated data structure that holds three members of the same type, which defaults to `int`. It is designed to store a trio of values, allowing for flexibility in the type of data it can contain by specifying a different type when instantiating the struct. This makes it versatile for various applications where a group of three related values need to be managed together.


# Functions

---
### lexical\_cast<!-- {{#callable:lexical_cast}} -->
The `lexical_cast` function logs a message indicating it was called with a given string input and always returns true.
- **Inputs**:
    - `input`: A constant reference to a `std::string` representing the input value to be processed.
    - `v`: A reference to a `Values<double>` object, which is not used in the function body.
- **Control Flow**:
    - The function takes a string input and a `Values<double>` reference as parameters.
    - It outputs a message to the standard output indicating the function was called and displays the input value.
    - The function then returns `true`, regardless of the input or the state of the `Values<double>` reference.
- **Output**: The function returns a boolean value `true`.


---
### argparse<!-- {{#callable:argparse}} -->
The `argparse` function adds a command-line option `--dv` to a given option group, which is linked to a `DoubleValues` object and has a default string value of "0".
- **Inputs**:
    - `group`: A pointer to a `CLI::Option_group` object where the `--dv` option will be added.
- **Control Flow**:
    - The function calls `add_option` on the provided `group` to add a new command-line option `--dv`.
    - The `--dv` option is associated with the `doubles` object of type `DoubleValues`.
    - The default string value for the `--dv` option is set to "0".
- **Output**: The function does not return any value.


---
### main<!-- {{#callable:main}} -->
The `main` function initializes a CLI application, sets up command-line argument parsing, and executes the parsing process.
- **Inputs**:
    - `argc`: An integer representing the number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the actual command-line arguments.
- **Control Flow**:
    - Create an instance of `CLI::App` named `app` to manage the command-line interface.
    - Call [`argparse`](#argparse) function with a new option group named "param" added to `app`, which sets up a command-line option `--dv` for `DoubleValues`.
    - Execute the command-line parsing using `CLI11_PARSE` macro with `app`, `argc`, and `argv`.
    - Return 0 to indicate successful execution.
- **Output**: The function returns an integer value `0`, indicating successful execution of the program.
- **Functions called**:
    - [`argparse`](#argparse)


