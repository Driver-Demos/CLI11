# Purpose
This C++ source code file is designed to create a command-line interface (CLI) application using the CLI11 library. The primary functionality of this code is to parse command-line arguments to set a "level" parameter, which can be one of three enumerated values: High, Medium, or Low. The code defines an enumeration `Level` and provides a custom output stream operator to display these levels as strings. This custom operator is used to override the default behavior of CLI11's enum streaming, allowing for a more descriptive output when the level is printed to the console. The code also utilizes a `std::map` to associate string inputs with the corresponding `Level` enum values, and employs CLI11's `CheckedTransformer` to ensure that the input is valid, with case-insensitive matching.

The file is structured as an executable program, with a [`main`](#main) function that initializes a `CLI::App` object to handle command-line parsing. The application requires the user to specify a level using the `-l` or `--level` option, and it enforces this requirement by marking the option as required. The use of CLI11's `CheckedTransformer` ensures that only valid inputs are accepted, providing a robust mechanism for input validation. The program concludes by printing the received level to the console, demonstrating the integration of custom enum streaming with CLI11's capabilities. This code is a focused example of how to leverage the CLI11 library to create a simple yet effective command-line tool with custom input handling and validation.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `map`
- `string`


# Data Structures

---
### Level<!-- {{#data_structure:Level}} -->
- **Type**: `enum`
- **Members**:
    - `High`: Represents a high level.
    - `Medium`: Represents a medium level.
    - `Low`: Represents a low level.
- **Description**: The `Level` enum class defines three distinct levels: High, Medium, and Low, which are used to categorize or specify the intensity or priority of a setting. This enum is strongly typed and scoped, ensuring type safety and preventing implicit conversions. It is used in conjunction with a command-line interface to allow users to specify a level setting, which is then transformed and validated using a map of string-to-enum mappings.


# Functions

---
### operator<<<!-- {{#callable:operator<<}} -->
The `operator<<` function overloads the stream insertion operator to output a string representation of a `Level` enum value to an `ostream`.
- **Inputs**:
    - `os`: A reference to an output stream (`std::ostream`) where the `Level` enum value will be written.
    - `level`: A constant reference to a `Level` enum value that needs to be converted to a string and output to the stream.
- **Control Flow**:
    - The function uses a `switch` statement to determine the string representation of the `Level` enum value.
    - If the `level` is `Level::High`, it outputs the string "High" to the stream.
    - If the `level` is `Level::Medium`, it outputs the string "Medium" to the stream.
    - If the `level` is `Level::Low`, it outputs the string "Low" to the stream.
    - After outputting the string representation of the `Level`, it appends the string " (ft rom custom ostream)" to the stream.
    - The function returns the modified output stream `os`.
- **Output**: The function returns a reference to the modified `std::ostream` object, allowing for chaining of stream operations.


---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application to parse a required level setting from the user input and outputs the corresponding enum value.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI::App object named `app` to handle command-line arguments.
    - Define a `Level` enum variable `level` with a default value of `Level::Low`.
    - Create a map to associate string representations ('high', 'medium', 'low') with corresponding `Level` enum values.
    - Add an option to the `app` to parse the `-l` or `--level` argument, requiring it to be specified, and transform it using the `CheckedTransformer` to ensure valid input.
    - Parse the command-line arguments using `CLI11_PARSE` macro, which processes the input and sets the `level` variable accordingly.
    - Output the received enum value using the overloaded `operator<<` for the `Level` enum.
- **Output**: The function outputs the string representation of the `Level` enum value received from the command-line input.


