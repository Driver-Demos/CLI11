# Purpose
This C++ source code file is part of a library designed to facilitate command-line interface (CLI) creation and management, specifically focusing on formatting help and usage messages for CLI applications. The file defines a series of inline functions within the `CLI` namespace, which are part of a `Formatter` class. These functions are responsible for generating formatted strings that describe the application's options, groups, subcommands, and overall usage. The code includes methods like [`make_group`](#stringmake_group), [`make_positionals`](#stringmake_positionals), [`make_groups`](#stringmake_groups), [`make_description`](#stringmake_description), [`make_usage`](#stringmake_usage), [`make_footer`](#stringmake_footer), and [`make_help`](#stringmake_help), each of which constructs a specific part of the help message by iterating over the application's options and subcommands, and formatting them according to the specified rules.

The file is structured to be included in other parts of the CLI library, as indicated by the use of `#pragma once` and the inclusion of necessary headers. It provides a narrow but essential functionality within the broader context of the CLI library, focusing on the presentation layer of command-line applications. The code does not define a public API directly but rather implements internal methods that are likely used by other components of the library to generate user-facing help documentation. The use of inline functions suggests an emphasis on performance, as these functions are intended to be expanded at compile time, reducing the overhead of function calls.
# Imports and Dependencies

---
- `../Formatter.hpp`
- `algorithm`
- `string`
- `utility`
- `vector`


# Functions

---
### make\_group<!-- {{#callable:CLI::std::string::make_group}} -->
The `make_group` function formats a group of options into a string representation, including the group name and each option's formatted output.
- **Inputs**:
    - `group`: A string representing the name of the group to be formatted.
    - `is_positional`: A boolean indicating whether the options are positional or not.
    - `opts`: A vector of pointers to `Option` objects that belong to the group.
- **Control Flow**:
    - Initialize a stringstream object `out` to build the output string.
    - Append the group name followed by a colon and a newline to the `out` stream.
    - Iterate over each `Option` pointer in the `opts` vector.
    - For each option, append the result of `make_option(opt, is_positional)` to the `out` stream.
    - Return the constructed string from the `out` stream.
- **Output**: A formatted string representing the group and its options.
- **Functions called**:
    - [`CLI::std::string::make_option`](#stringmake_option)


---
### make\_positionals<!-- {{#callable:CLI::std::string::make_positionals}} -->
The `make_positionals` function generates a formatted string of positional options for a given application.
- **Inputs**:
    - `app`: A pointer to an `App` object, representing the application for which positional options are to be formatted.
- **Control Flow**:
    - Retrieve a list of options from the `app` object that have a non-empty group and are positional using a lambda function.
    - Check if the list of options is empty; if so, return an empty string.
    - If the list is not empty, call the [`make_group`](#stringmake_group) function with the label 'POSITIONALS', a boolean indicating the options are positional, and the list of options, then return the result.
- **Output**: A string representing the formatted positional options for the application, or an empty string if there are no positional options.
- **Functions called**:
    - [`CLI::std::string::make_group`](#stringmake_group)


---
### make\_groups<!-- {{#callable:CLI::std::string::make_groups}} -->
The `make_groups` function formats and returns a string representation of non-positional options grouped by their respective groups from a given application, excluding help options when in subcommand mode.
- **Inputs**:
    - `app`: A pointer to an `App` object representing the application whose options are to be formatted.
    - `mode`: An `AppFormatMode` enum value indicating the formatting mode, which affects whether help options are included.
- **Control Flow**:
    - Initialize a stringstream `out` to accumulate the formatted output.
    - Retrieve the list of groups from the `app` object using `get_groups()`.
    - Iterate over each group in the list of groups.
    - For each group, retrieve the list of non-positional options that belong to the group and are not help options if the mode is `Sub`.
    - If the group is not empty and has options, format the group and its options using [`make_group`](#stringmake_group) and append the result to `out`.
    - Return the accumulated string from the stringstream `out`.
- **Output**: A formatted string representing the non-positional options grouped by their respective groups, excluding help options in subcommand mode.
- **Functions called**:
    - [`CLI::std::string::make_group`](#stringmake_group)


---
### make\_description<!-- {{#callable:CLI::std::string::make_description}} -->
The `make_description` function generates a formatted description string for a given application, including details about required options and constraints.
- **Inputs**:
    - `app`: A pointer to an `App` object, which contains information about the application's description, required options, and constraints.
- **Control Flow**:
    - Retrieve the application's description using `app->get_description()` and store it in `desc`.
    - Get the minimum and maximum required options using `app->get_require_option_min()` and `app->get_require_option_max()`.
    - If the application is marked as required (`app->get_required()`), append a 'REQUIRED' label to the description.
    - If the minimum required options (`min_options`) is greater than 0, append a message to `desc` indicating the exact, range, or minimum number of required options based on the values of `min_options` and `max_options`.
    - If only the maximum options (`max_options`) is greater than 0, append a message to `desc` indicating the maximum number of allowed options.
    - Return the formatted description string, appending two newlines if `desc` is not empty, or an empty string otherwise.
- **Output**: A formatted string describing the application, including any required options and constraints, or an empty string if no description is available.


---
### make\_usage<!-- {{#callable:CLI::std::string::make_usage}} -->
The `make_usage` function generates a usage string for a command-line application, detailing the usage pattern, options, positionals, and subcommands.
- **Inputs**:
    - `app`: A pointer to an `App` object representing the command-line application for which the usage string is being generated.
    - `name`: A string representing the name of the application or command, which will be included in the usage output.
- **Control Flow**:
    - Retrieve the usage string from the `app` object using `get_usage()`.
    - If the usage string is not empty, return it with two newlines appended.
    - Initialize a stringstream `out` and append a newline to it.
    - Check if `name` is empty; if so, append 'Usage:' to `out`, otherwise append `name`.
    - Retrieve non-positional options from `app` and append '[OPTIONS]' to `out` if any exist.
    - Retrieve positional options from `app` and append their usage names to `out` if any exist.
    - Check for subcommands in `app` that are not disabled and have a name; append 'SUBCOMMAND' or 'SUBCOMMANDS' to `out` based on the subcommand requirements.
    - Append two newlines to `out` and return the resulting string.
- **Output**: A string representing the formatted usage information for the application, including options, positionals, and subcommands.
- **Functions called**:
    - [`CLI::std::string::make_option_usage`](#stringmake_option_usage)


---
### make\_footer<!-- {{#callable:CLI::std::string::make_footer}} -->
The `make_footer` function generates a formatted footer string for a given application if the footer is not empty.
- **Inputs**:
    - `app`: A pointer to an `App` object from which the footer string is retrieved.
- **Control Flow**:
    - Retrieve the footer string from the `App` object using `app->get_footer()`.
    - Check if the retrieved footer string is empty.
    - If the footer is empty, return an empty string.
    - If the footer is not empty, prepend and append newline characters to the footer and return the formatted string.
- **Output**: A formatted string containing the footer with newline characters, or an empty string if the footer is empty.


---
### make\_help<!-- {{#callable:CLI::std::string::make_help}} -->
The `make_help` function generates a formatted help message for a given application, including its description, usage, positional options, groups, subcommands, and footer.
- **Inputs**:
    - `app`: A pointer to an `App` object representing the application for which the help message is being generated.
    - `name`: A `std::string` representing the name of the application or command.
    - `mode`: An `AppFormatMode` enum value indicating the format mode, which can affect how subcommands are processed.
- **Control Flow**:
    - If the mode is `AppFormatMode::Sub`, the function immediately calls [`make_expanded`](#stringmake_expanded) to handle subcommands with overridden formatters.
    - A `std::stringstream` is initialized to build the help message.
    - If the application's name is empty and it has a parent, the group's name is added to the output unless it is 'SUBCOMMANDS'.
    - The application's description is formatted and added to the output, either as a paragraph or a simple string based on the paragraph formatting setting.
    - The usage, positional options, groups, and subcommands are sequentially appended to the output using respective helper functions.
    - The footer is formatted and appended to the output, again considering paragraph formatting settings.
    - The constructed help message is returned as a string.
- **Output**: A `std::string` containing the formatted help message for the application.
- **Functions called**:
    - [`CLI::std::string::make_expanded`](#stringmake_expanded)
    - [`CLI::std::string::make_description`](#stringmake_description)
    - [`CLI::std::string::make_usage`](#stringmake_usage)
    - [`CLI::std::string::make_positionals`](#stringmake_positionals)
    - [`CLI::std::string::make_groups`](#stringmake_groups)
    - [`CLI::std::string::make_subcommands`](#stringmake_subcommands)
    - [`CLI::std::string::make_footer`](#stringmake_footer)


---
### make\_subcommands<!-- {{#callable:CLI::std::string::make_subcommands}} -->
The `make_subcommands` function generates a formatted string representation of subcommands for a given application, organized by their groups.
- **Inputs**:
    - `app`: A pointer to an `App` object representing the application whose subcommands are to be formatted.
    - `mode`: An `AppFormatMode` enum value that specifies the formatting mode for the subcommands.
- **Control Flow**:
    - Initialize a stringstream `out` to accumulate the formatted output.
    - Retrieve all subcommands of the given `app` using `get_subcommands`.
    - Iterate over each subcommand to check if it has a name and group, and collect unique group names in `subcmd_groups_seen`.
    - For each unique group in `subcmd_groups_seen`, append the group name to `out` and retrieve subcommands belonging to that group.
    - Iterate over each subcommand in the group, and depending on the `mode`, append either a detailed help or a brief subcommand description to `out`.
- **Output**: A `std::string` containing the formatted representation of the subcommands, organized by their groups.
- **Functions called**:
    - [`CLI::std::string::make_expanded`](#stringmake_expanded)
    - [`CLI::std::string::make_subcommand`](#stringmake_subcommand)


---
### make\_subcommand<!-- {{#callable:CLI::std::string::make_subcommand}} -->
The `make_subcommand` function formats and returns a string representation of a subcommand, including its name, requirement status, and description, formatted as a paragraph.
- **Inputs**:
    - `sub`: A pointer to an `App` object representing the subcommand to be formatted.
- **Control Flow**:
    - Initialize a stringstream `out` to build the formatted output.
    - Construct the subcommand's name with indentation, display name, and a 'REQUIRED' label if applicable.
    - Output the formatted name to the stringstream with left alignment and a specified column width.
    - Use `detail::streamOutAsParagraph` to format the subcommand's description as a paragraph, considering the right column width and indentation.
    - Append a newline character to the output.
    - Return the formatted string from the stringstream.
- **Output**: A formatted string representing the subcommand, including its name, requirement status, and description.


---
### make\_expanded<!-- {{#callable:CLI::std::string::make_expanded}} -->
The `make_expanded` function generates a detailed string representation of a command-line application's subcommand, including its name, description, aliases, positionals, groups, subcommands, and footer, formatted according to specified settings.
- **Inputs**:
    - `sub`: A pointer to an `App` object representing the subcommand to be formatted.
    - `mode`: An `AppFormatMode` enumeration value that specifies the formatting mode for the subcommand.
- **Control Flow**:
    - Initialize a stringstream `out` and append the display name of the subcommand followed by a newline.
    - Check if description paragraph formatting is enabled; if so, format the description as a paragraph and append it to `out`, otherwise append the description directly followed by a newline.
    - If the subcommand has no name but has aliases, format the aliases and append them to `out`.
    - Append the formatted positionals, groups, and subcommands of the subcommand to `out`.
    - Check if footer paragraph formatting is enabled; if so, format the footer as a paragraph and append it to `out`, otherwise append the footer directly followed by a newline.
    - Append an additional newline to `out` and return the resulting string.
- **Output**: A `std::string` containing the formatted representation of the subcommand.
- **Functions called**:
    - [`CLI::std::string::make_description`](#stringmake_description)
    - [`CLI::std::string::make_positionals`](#stringmake_positionals)
    - [`CLI::std::string::make_groups`](#stringmake_groups)
    - [`CLI::std::string::make_subcommands`](#stringmake_subcommands)
    - [`CLI::std::string::make_footer`](#stringmake_footer)


---
### make\_option<!-- {{#callable:CLI::std::string::make_option}} -->
The `make_option` function formats and returns a string representation of a command-line option, considering whether it is positional or not.
- **Inputs**:
    - `opt`: A pointer to an `Option` object representing the command-line option to be formatted.
    - `is_positional`: A boolean indicating whether the option is positional (true) or not (false).
- **Control Flow**:
    - Initialize a stringstream `out` to build the formatted option string.
    - If `is_positional` is true, format the option name and options, align them to the left, and append the description if available.
    - If `is_positional` is false, split the option names into short and long names, format them separately, and align them within specified column widths.
    - Adjust column widths if short names exceed their allocated space, and append the description if available.
    - Return the formatted string from the stringstream `out`.
- **Output**: A formatted string representing the command-line option, including its name, options, and description, aligned according to specified column widths.
- **Functions called**:
    - [`CLI::std::string::make_option_name`](#stringmake_option_name)
    - [`CLI::std::string::make_option_opts`](#stringmake_option_opts)
    - [`CLI::std::string::make_option_desc`](#stringmake_option_desc)


---
### make\_option\_name<!-- {{#callable:CLI::std::string::make_option_name}} -->
The `make_option_name` function generates the name of an option based on whether it is positional or not.
- **Inputs**:
    - `opt`: A pointer to an `Option` object whose name is to be generated.
    - `is_positional`: A boolean indicating whether the option is positional or not.
- **Control Flow**:
    - Check if the option is positional by evaluating `is_positional`.
    - If `is_positional` is true, call `opt->get_name(true, false)` to get the positional name of the option.
    - If `is_positional` is false, call `opt->get_name(false, true)` to get the non-positional name of the option.
- **Output**: Returns a `std::string` representing the name of the option, formatted based on its positional status.


---
### make\_option\_opts<!-- {{#callable:CLI::std::string::make_option_opts}} -->
The `make_option_opts` function generates a formatted string representing the options and constraints of a given command-line option.
- **Inputs**:
    - `opt`: A pointer to an `Option` object, which contains details about a command-line option such as its name, type, default value, and constraints.
- **Control Flow**:
    - Initialize a stringstream `out` to build the output string.
    - Check if the option has a non-empty option text; if so, append it to `out`.
    - If the option text is empty, check if the option has a non-zero type size.
    - If the type size is non-zero, append the type name label if available.
    - Append the default string in square brackets if it is not empty.
    - If the expected maximum size equals a predefined constant, append an ellipsis; otherwise, if the expected minimum is greater than one, append the expected count prefixed by 'x'.
    - If the option is required, append a 'REQUIRED' label.
    - If the option has an environment variable name, append it in parentheses prefixed by 'Env:'.
    - If the option has dependencies (needs), append them prefixed by 'Needs:'.
    - If the option has exclusions, append them prefixed by 'Excludes:'.
    - Return the constructed string from the stringstream `out`.
- **Output**: A formatted string that describes the option's text, type, default value, requirements, environment variable, dependencies, and exclusions.


---
### make\_option\_desc<!-- {{#callable:CLI::std::string::make_option_desc}} -->
The `make_option_desc` function retrieves and returns the description of a given option.
- **Inputs**:
    - `opt`: A pointer to an `Option` object from which the description is to be retrieved.
- **Control Flow**:
    - The function calls the `get_description` method on the `Option` object pointed to by `opt`.
- **Output**: A `std::string` containing the description of the option.


---
### make\_option\_usage<!-- {{#callable:CLI::std::string::make_option_usage}} -->
The `make_option_usage` function generates a string representation of an option's usage, considering its positional status, expected occurrences, and requirement status.
- **Inputs**:
    - `opt`: A pointer to an `Option` object, representing the command-line option for which the usage string is being generated.
- **Control Flow**:
    - Initialize a stringstream `out` to build the usage string.
    - Call [`make_option_name`](#stringmake_option_name) with `opt` and `true` to get the option's name in positional format and append it to `out`.
    - Check if the option's `expected_max` is greater than or equal to `detail::expected_max_vector_size`; if true, append '...' to `out`.
    - Otherwise, if `expected_max` is greater than 1, append the expected count in the format '(Nx)' to `out`.
    - Return the usage string directly if the option is required, or wrap it in square brackets if it is optional.
- **Output**: A `std::string` representing the formatted usage of the option, indicating its name, multiplicity, and whether it is required or optional.
- **Functions called**:
    - [`CLI::std::string::make_option_name`](#stringmake_option_name)


