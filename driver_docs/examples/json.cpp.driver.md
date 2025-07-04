# Purpose
This C++ source code file is designed to provide functionality for handling command-line interface (CLI) configurations using JSON format. It leverages the CLI11 library to parse command-line arguments and the nlohmann::json library to manage JSON data. The primary class, `ConfigJSON`, extends the `CLI::Config` class to enable conversion between CLI options and JSON configurations. The [`to_config`](#ConfigJSONto_config) method serializes the application's options into a JSON string, while the [`from_config`](#ConfigJSONfrom_config) method deserializes JSON input into a vector of `CLI::ConfigItem` objects, which represent the configuration items. This class supports both single and multiple option values, as well as default values, and handles subcommands recursively.

The file includes a [`main`](#main) function, indicating that it is an executable program. The [`main`](#main) function sets up a CLI application using the CLI11 library, adds a flag and an option, and configures the application to use the `ConfigJSON` formatter for configuration handling. The program parses command-line arguments and outputs the configuration as a JSON string. This code provides a focused functionality for integrating JSON-based configuration management into CLI applications, making it easier to handle complex configurations and subcommands in a structured and human-readable format.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `memory`
- `nlohmann/json.hpp`
- `string`
- `vector`


# Data Structures

---
### ConfigJSON<!-- {{#data_structure:ConfigJSON}} -->
- **Type**: `class`
- **Description**: The `ConfigJSON` class is a custom configuration handler that extends the `CLI::Config` class, designed to serialize and deserialize command-line interface (CLI) options and configurations into JSON format. It overrides the `to_config` method to convert CLI options into a JSON object, handling both flags and non-flag options, and supports nested subcommands. The `from_config` method reads a JSON input stream and converts it back into a vector of `CLI::ConfigItem` objects, allowing for easy integration of JSON-based configuration files with CLI applications.
- **Member Functions**:
    - [`ConfigJSON::to_config`](#ConfigJSONto_config)
    - [`ConfigJSON::from_config`](#ConfigJSONfrom_config)
    - [`ConfigJSON::_from_config`](#ConfigJSON_from_config)
- **Inherits From**:
    - `CLI::Config`

**Methods**

---
#### ConfigJSON::to\_config<!-- {{#callable:ConfigJSON::to_config}} -->
The [`to_config`](../include/CLI/impl/Config_inl.hpp.driver.md#stringto_config) function generates a JSON configuration string from a CLI application, including options and subcommands, with an option to include default values.
- **Inputs**:
    - `app`: A pointer to a `CLI::App` object representing the command-line application whose configuration is to be converted to JSON.
    - `default_also`: A boolean flag indicating whether default values should be included in the JSON output.
    - `(unnamed boolean)`: An unused boolean parameter.
    - `(unnamed string)`: An unused string parameter.
- **Control Flow**:
    - Initialize a JSON object `j` to store the configuration.
    - Iterate over each option in the `app` using `get_options()` method.
    - For each option, check if it has a long name and is configurable.
    - If the option is not a flag (has a type size), check the count of occurrences and add the result or default value to `j`.
    - If the option is a flag, set the JSON value to true, the count, or false based on the count and `default_also` flag.
    - Iterate over each subcommand in the `app` using `get_subcommands()` method.
    - Recursively call [`to_config`](../include/CLI/impl/Config_inl.hpp.driver.md#stringto_config) for each subcommand and add the result to `j`.
    - Return the JSON object `j` as a formatted string with an indentation of 4 spaces.
- **Output**: A formatted JSON string representing the configuration of the CLI application, including options and subcommands.
- **Functions called**:
    - [`CLI::std::string::to_config`](../include/CLI/impl/Config_inl.hpp.driver.md#stringto_config)
- **See also**: [`ConfigJSON`](#ConfigJSON)  (Data Structure)


---
#### ConfigJSON::from\_config<!-- {{#callable:ConfigJSON::from_config}} -->
The `from_config` function reads JSON data from an input stream and converts it into a vector of `CLI::ConfigItem` objects.
- **Inputs**:
    - `input`: An input stream (`std::istream`) from which JSON data is read.
- **Control Flow**:
    - Initialize a JSON object `j`.
    - Read JSON data from the input stream into `j`.
    - Call the private method [`_from_config`](#ConfigJSON_from_config) with the JSON object `j` to convert it into a vector of `CLI::ConfigItem` objects.
- **Output**: A vector of `CLI::ConfigItem` objects representing the configuration data parsed from the JSON input.
- **Functions called**:
    - [`ConfigJSON::_from_config`](#ConfigJSON_from_config)
- **See also**: [`ConfigJSON`](#ConfigJSON)  (Data Structure)


---
#### ConfigJSON::\_from\_config<!-- {{#callable:ConfigJSON::_from_config}} -->
The `_from_config` function recursively parses a JSON object to extract configuration items, converting them into a vector of `CLI::ConfigItem` objects.
- **Inputs**:
    - `j`: A JSON object or value to be parsed.
    - `name`: An optional string representing the current key name in the JSON hierarchy, defaulting to an empty string.
    - `prefix`: An optional vector of strings representing the hierarchy of parent keys, defaulting to an empty vector.
- **Control Flow**:
    - Initialize an empty vector `results` to store the parsed configuration items.
    - Check if the JSON `j` is an object; if so, iterate over each key-value pair.
    - For each key-value pair, copy the current `prefix`, append the current `name` if it's not empty, and recursively call `_from_config` on the value with the updated name and prefix.
    - Insert the results of the recursive call into the `results` vector.
    - If `j` is not an object and `name` is not empty, create a new `CLI::ConfigItem`, set its `name` and `parents` fields, and determine the type of `j` to populate the `inputs` field accordingly.
    - If `j` is a boolean, convert it to a string and add to `inputs`.
    - If `j` is a number, convert it to a string using a stringstream and add to `inputs`.
    - If `j` is a string, directly add it to `inputs`.
    - If `j` is an array, iterate over its elements and add each to `inputs`.
    - If `j` is none of the above types, throw a `CLI::ConversionError` indicating a conversion failure.
    - If `j` is not an object and `name` is empty, throw a `CLI::ConversionError` indicating that top-level values must be objects.
    - Return the `results` vector containing all parsed configuration items.
- **Output**: A vector of `CLI::ConfigItem` objects representing the parsed configuration items from the JSON input.
- **See also**: [`ConfigJSON`](#ConfigJSON)  (Data Structure)



# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application, configures it with JSON formatting, parses command-line arguments, and outputs the configuration as a JSON string.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Create a `CLI::App` object named `app` to manage command-line options.
    - Set the configuration formatter of `app` to use a custom `ConfigJSON` formatter for JSON output.
    - Declare an integer variable `item` to store the value of the `--item` option.
    - Add a flag `--simple` to the application, which can be set by the user.
    - Add an option `--item` to the application, which assigns its value to the `item` variable.
    - Set the configuration file option to `--config`, allowing configuration to be loaded from a file.
    - Parse the command-line arguments using `CLI11_PARSE`, which processes the options and flags.
    - Output the current configuration of the application as a JSON string using `app.config_to_str(true, true)` and print it to the standard output.
- **Output**: The function outputs the application's configuration as a formatted JSON string to the standard output.


