# Purpose
This C++ source code file is an executable program that demonstrates the use of the CLI11 library, a command-line interface parser for C++. The primary purpose of this code is to showcase custom formatting capabilities for command-line options using a derived class, [`MyFormatter`](#MyFormatterMyFormatter), which extends the `CLI::Formatter` class. The custom formatter modifies how options are displayed by overriding the [`make_option_opts`](#MyFormattermake_option_opts) method. The program sets up a command-line application with the `CLI::App` class, adding flags and subcommands to illustrate the functionality of the CLI11 library.

The code defines a main function that initializes a `CLI::App` object, configures a custom help flag, and applies the custom formatter with a specified column width. It adds a flag to the main application and two subcommands, each with its own flag, demonstrating how to structure a command-line application with multiple layers of commands. The `CLI11_PARSE` macro is used to parse the command-line arguments, and the program outputs a message indicating its purpose when executed. This file serves as an example of how to implement and customize command-line interfaces in C++ using the CLI11 library, providing a clear demonstration of its capabilities and flexibility.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `memory`
- `string`


# Data Structures

---
### MyFormatter<!-- {{#data_structure:MyFormatter}} -->
- **Type**: `class`
- **Description**: The `MyFormatter` class is a custom formatter that inherits from the `CLI::Formatter` class, providing a specialized implementation for formatting command-line interface options. It overrides the `make_option_opts` method to return a fixed string " OPTION", which is used to format the options in the CLI application. This class is used to customize the appearance of command-line options when displaying help messages in a CLI application.
- **Member Functions**:
    - [`MyFormatter::MyFormatter`](#MyFormatterMyFormatter)
    - [`MyFormatter::make_option_opts`](#MyFormattermake_option_opts)
- **Inherits From**:
    - `CLI::Formatter`

**Methods**

---
#### MyFormatter::MyFormatter<!-- {{#callable:MyFormatter::MyFormatter}} -->
The `make_option_opts` method in the `MyFormatter` class returns a fixed string " OPTION" for any given `CLI::Option`.
- **Inputs**:
    - `CLI::Option *`: A pointer to a `CLI::Option` object, representing a command-line option, though it is not used in the function.
- **Control Flow**:
    - The method is an override of a virtual function from the `CLI::Formatter` base class.
    - It takes a pointer to a `CLI::Option` as an argument but does not utilize it in its logic.
    - The method simply returns the string " OPTION" regardless of the input.
- **Output**: A `std::string` containing the text " OPTION".
- **See also**: [`MyFormatter`](#MyFormatter)  (Data Structure)


---
#### MyFormatter::make\_option\_opts<!-- {{#callable:MyFormatter::make_option_opts}} -->
The `make_option_opts` function returns a fixed string " OPTION" for formatting command-line options.
- **Inputs**:
    - `CLI::Option *`: A pointer to a CLI::Option object, which represents a command-line option.
- **Control Flow**:
    - The function takes a pointer to a CLI::Option object as an argument.
    - It overrides the base class method to provide a custom implementation.
    - The function returns a fixed string " OPTION" regardless of the input.
- **Output**: A string " OPTION" is returned, which is used for formatting command-line options.
- **See also**: [`MyFormatter`](#MyFormatter)  (Data Structure)



# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application with custom formatting and subcommands, then parses the command-line arguments.
- **Inputs**:
    - `argc`: An integer representing the number of command-line arguments.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Create a CLI::App object to manage the command-line interface.
    - Set a custom help flag '--help-all' to display all help information.
    - Instantiate a shared pointer to a custom formatter `MyFormatter` and set its column width to 15.
    - Assign the custom formatter to the CLI application.
    - Add a flag '--flag' to the main application.
    - Create a subcommand 'one' with a description and add a flag '--oneflag' to it.
    - Create another subcommand 'two' with a description and add a flag '--twoflag' to it.
    - Parse the command-line arguments using the CLI11_PARSE macro.
    - Output a message to the console indicating the purpose of the application.
- **Output**: Returns an integer 0, indicating successful execution.


