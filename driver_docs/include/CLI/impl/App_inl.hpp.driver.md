# Purpose
This C++ source file is part of the CLI11 library, which is a command-line interface (CLI) parser for C++. The file defines the implementation of the `App` class, which is a core component of the library responsible for managing command-line applications. The `App` class provides functionality for defining and handling command-line options, flags, and subcommands. It supports features such as option inheritance, subcommand parsing, and configuration file processing. The class also includes mechanisms for handling errors, generating help messages, and managing option dependencies and exclusions.

The file includes several inline functions that implement the behavior of the `App` class, such as adding options and subcommands, parsing command-line arguments, and processing configuration files. It also defines utility functions for managing option states, handling errors, and generating help messages. The file is structured to be included in other parts of the CLI11 library, as indicated by the use of `#pragma once` and the inclusion of related headers. The code is designed to be flexible and extensible, allowing developers to create complex command-line applications with nested subcommands and customizable option parsing behavior.
# Imports and Dependencies

---
- `../App.hpp`
- `../Argv.hpp`
- `../Encoding.hpp`
- `algorithm`
- `iostream`
- `memory`
- `string`
- `utility`
- `vector`


# Data Structures

---
### App<!-- {{#data_structure:CLI::App}} -->
- **Description**: [See definition](../App.hpp.driver.md#CLIApp)
- **Member Functions**:
    - [`CLI::App::App`](../App.hpp.driver.md#AppApp)
    - [`CLI::App::App`](../App.hpp.driver.md#AppApp)
    - [`CLI::App::operator=`](../App.hpp.driver.md#Appoperator=)
    - [`CLI::App::~App`](../App.hpp.driver.md#AppApp)
    - [`CLI::App::callback`](../App.hpp.driver.md#Appcallback)
    - [`CLI::App::final_callback`](../App.hpp.driver.md#Appfinal_callback)
    - [`CLI::App::parse_complete_callback`](../App.hpp.driver.md#Appparse_complete_callback)
    - [`CLI::App::preparse_callback`](../App.hpp.driver.md#Apppreparse_callback)
    - [`CLI::App::allow_extras`](../App.hpp.driver.md#Appallow_extras)
    - [`CLI::App::required`](../App.hpp.driver.md#Apprequired)
    - [`CLI::App::disabled`](../App.hpp.driver.md#Appdisabled)
    - [`CLI::App::silent`](../App.hpp.driver.md#Appsilent)
    - [`CLI::App::allow_non_standard_option_names`](../App.hpp.driver.md#Appallow_non_standard_option_names)
    - [`CLI::App::allow_subcommand_prefix_matching`](../App.hpp.driver.md#Appallow_subcommand_prefix_matching)
    - [`CLI::App::disabled_by_default`](../App.hpp.driver.md#Appdisabled_by_default)
    - [`CLI::App::enabled_by_default`](../App.hpp.driver.md#Appenabled_by_default)
    - [`CLI::App::validate_positionals`](../App.hpp.driver.md#Appvalidate_positionals)
    - [`CLI::App::validate_optional_arguments`](../App.hpp.driver.md#Appvalidate_optional_arguments)
    - [`CLI::App::allow_config_extras`](../App.hpp.driver.md#Appallow_config_extras)
    - [`CLI::App::allow_config_extras`](../App.hpp.driver.md#Appallow_config_extras)
    - [`CLI::App::prefix_command`](../App.hpp.driver.md#Appprefix_command)
    - [`CLI::App::allow_windows_style_options`](../App.hpp.driver.md#Appallow_windows_style_options)
    - [`CLI::App::positionals_at_end`](../App.hpp.driver.md#Apppositionals_at_end)
    - [`CLI::App::configurable`](../App.hpp.driver.md#Appconfigurable)
    - [`CLI::App::formatter`](../App.hpp.driver.md#Appformatter)
    - [`CLI::App::formatter_fn`](../App.hpp.driver.md#Appformatter_fn)
    - [`CLI::App::config_formatter`](../App.hpp.driver.md#Appconfig_formatter)
    - [`CLI::App::parsed`](../App.hpp.driver.md#Appparsed)
    - [`CLI::App::option_defaults`](../App.hpp.driver.md#Appoption_defaults)
    - [`CLI::App::add_option`](../App.hpp.driver.md#Appadd_option)
    - [`CLI::App::add_option_no_stream`](../App.hpp.driver.md#Appadd_option_no_stream)
    - [`CLI::App::add_option_function`](../App.hpp.driver.md#Appadd_option_function)
    - [`CLI::App::add_option`](../App.hpp.driver.md#Appadd_option)
    - [`CLI::App::add_option`](../App.hpp.driver.md#Appadd_option)
    - [`CLI::App::add_flag`](../App.hpp.driver.md#Appadd_flag)
    - [`CLI::App::add_flag`](../App.hpp.driver.md#Appadd_flag)
    - [`CLI::App::add_flag`](../App.hpp.driver.md#Appadd_flag)
    - [`CLI::App::add_flag`](../App.hpp.driver.md#Appadd_flag)
    - [`CLI::App::add_flag`](../App.hpp.driver.md#Appadd_flag)
    - [`CLI::App::add_option_group`](../App.hpp.driver.md#Appadd_option_group)
    - [`CLI::App::group`](../App.hpp.driver.md#Appgroup)
    - [`CLI::App::require_subcommand`](../App.hpp.driver.md#Apprequire_subcommand)
    - [`CLI::App::require_subcommand`](../App.hpp.driver.md#Apprequire_subcommand)
    - [`CLI::App::require_subcommand`](../App.hpp.driver.md#Apprequire_subcommand)
    - [`CLI::App::require_option`](../App.hpp.driver.md#Apprequire_option)
    - [`CLI::App::require_option`](../App.hpp.driver.md#Apprequire_option)
    - [`CLI::App::require_option`](../App.hpp.driver.md#Apprequire_option)
    - [`CLI::App::fallthrough`](../App.hpp.driver.md#Appfallthrough)
    - [`CLI::App::subcommand_fallthrough`](../App.hpp.driver.md#Appsubcommand_fallthrough)
    - [`CLI::App::pre_callback`](../App.hpp.driver.md#Apppre_callback)
    - [`CLI::App::failure_message`](../App.hpp.driver.md#Appfailure_message)
    - [`CLI::App::ensure_utf8`](#Appensure_utf8)
    - [`CLI::App::name`](#Appname)
    - [`CLI::App::alias`](#Appalias)
    - [`CLI::App::immediate_callback`](#Appimmediate_callback)
    - [`CLI::App::ignore_case`](#Appignore_case)
    - [`CLI::App::ignore_underscore`](#Appignore_underscore)
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::App::set_help_flag`](#Appset_help_flag)
    - [`CLI::App::set_help_all_flag`](#Appset_help_all_flag)
    - [`CLI::App::set_version_flag`](#Appset_version_flag)
    - [`CLI::App::set_version_flag`](#Appset_version_flag)
    - [`CLI::App::_add_flag_internal`](#App_add_flag_internal)
    - [`CLI::App::add_flag_callback`](#Appadd_flag_callback)
    - [`CLI::App::add_flag_function`](#Appadd_flag_function)
    - [`CLI::App::set_config`](#Appset_config)
    - [`CLI::App::add_subcommand`](#Appadd_subcommand)
    - [`CLI::App::add_subcommand`](#Appadd_subcommand)
    - [`CLI::App::get_subcommand`](#Appget_subcommand)
    - [`CLI::App::get_subcommand`](#Appget_subcommand)
    - [`CLI::App::get_subcommand_no_throw`](#Appget_subcommand_no_throw)
    - [`CLI::App::get_subcommand`](#Appget_subcommand)
    - [`CLI::App::get_option_group`](#Appget_option_group)
    - [`CLI::App::exit`](#Appexit)
    - [`CLI::App::get_option_no_throw`](#Appget_option_no_throw)
    - [`CLI::App::get_option_no_throw`](#Appget_option_no_throw)
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
    - [`CLI::App::_compare_subcommand_names`](#App_compare_subcommand_names)

**Methods**

---
#### App::ensure\_utf8<!-- {{#callable:CLI::App::ensure_utf8}} -->
The `ensure_utf8` function converts command-line arguments to UTF-8 encoding on Windows systems, while returning the original arguments on other platforms.
- **Inputs**:
    - `argv`: A pointer to an array of C-style strings representing command-line arguments.
- **Control Flow**:
    - Check if the code is running on a Windows platform using the preprocessor directive `#ifdef _WIN32`.
    - If on Windows, ignore the input `argv` and compute a UTF-8 normalized version of the command-line arguments using `detail::compute_win32_argv()`.
    - Clear the `normalized_argv_view_` vector if it is not empty, then reserve space for the new arguments.
    - Iterate over each argument in `normalized_argv_`, convert it to a non-const `char*` using `const_cast`, and store it in `normalized_argv_view_`.
    - Return the data pointer of `normalized_argv_view_`.
    - If not on Windows, simply return the input `argv`.
- **Output**: A pointer to an array of C-style strings, either the original `argv` or a UTF-8 normalized version on Windows.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::name<!-- {{#callable:CLI::App::name}} -->
The `name` function sets the name of the application or subcommand, ensuring it does not conflict with existing subcommand names.
- **Inputs**:
    - `app_name`: A string representing the new name to be assigned to the application or subcommand.
- **Control Flow**:
    - Check if the current `App` object has a parent.
    - If it has a parent, store the current name in `oname` and set `name_` to `app_name`.
    - Compare the new name with existing subcommand names using [`_compare_subcommand_names`](#App_compare_subcommand_names).
    - If a conflict is found, revert `name_` to `oname` and throw an `OptionAlreadyAdded` exception.
    - If no parent exists, simply set `name_` to `app_name`.
    - Set `has_automatic_name_` to `false`.
    - Return the current `App` object.
- **Output**: Returns a pointer to the current `App` object (`this`).
- **Functions called**:
    - [`CLI::App::_compare_subcommand_names`](#App_compare_subcommand_names)
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::alias<!-- {{#callable:CLI::App::alias}} -->
The `alias` method adds an alias name to the current `App` object, ensuring it does not conflict with existing subcommand names.
- **Inputs**:
    - `app_name`: A string representing the alias name to be added to the `App` object.
- **Control Flow**:
    - Check if `app_name` is empty or contains invalid characters, throwing an `IncorrectConstruction` exception if so.
    - If the `App` object has a parent, add `app_name` to the `aliases_` vector and check for conflicts with existing subcommand names using [`_compare_subcommand_names`](#App_compare_subcommand_names).
    - If a conflict is found, remove `app_name` from `aliases_` and throw an `OptionAlreadyAdded` exception.
    - If no parent exists, simply add `app_name` to the `aliases_` vector.
- **Output**: Returns a pointer to the current `App` object (`this`).
- **Functions called**:
    - [`CLI::App::_compare_subcommand_names`](#App_compare_subcommand_names)
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::immediate\_callback<!-- {{#callable:CLI::App::immediate_callback}} -->
The `immediate_callback` function sets the `immediate_callback_` flag and swaps the `final_callback_` and `parse_complete_callback_` functions based on the flag's value.
- **Inputs**:
    - `immediate`: A boolean value indicating whether the callback should be executed immediately upon parse completion.
- **Control Flow**:
    - Set the `immediate_callback_` member variable to the value of the `immediate` parameter.
    - If `immediate_callback_` is true, check if `final_callback_` is set and `parse_complete_callback_` is not set, then swap them.
    - If `immediate_callback_` is false, check if `final_callback_` is not set and `parse_complete_callback_` is set, then swap them.
    - Return the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance (`this`).
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::ignore\_case<!-- {{#callable:CLI::App::ignore_case}} -->
The `ignore_case` method in the `App` class sets the case sensitivity for subcommand names, ensuring no conflicts arise when case insensitivity is enabled.
- **Inputs**:
    - `value`: A boolean indicating whether to enable or disable case insensitivity for subcommand names.
- **Control Flow**:
    - Check if `value` is true and `ignore_case_` is false.
    - If true, set `ignore_case_` to true and determine the parent app to check for subcommand name conflicts.
    - Compare subcommand names between the current app and its parent to detect conflicts.
    - If conflicts are found, reset `ignore_case_` to false and throw an `OptionAlreadyAdded` exception with a conflict message.
    - Set `ignore_case_` to the provided `value`.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **Functions called**:
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
    - [`CLI::App::_compare_subcommand_names`](#App_compare_subcommand_names)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::ignore\_underscore<!-- {{#callable:CLI::App::ignore_underscore}} -->
The `ignore_underscore` function sets the `ignore_underscore_` flag for an `App` object and checks for subcommand name conflicts if the flag is enabled.
- **Inputs**:
    - `value`: A boolean value indicating whether to enable or disable the ignore underscore feature.
- **Control Flow**:
    - Check if `value` is true and `ignore_underscore_` is false.
    - If true, set `ignore_underscore_` to true and determine the parent `App` object.
    - Compare subcommand names between the current `App` and its parent to find conflicts.
    - If conflicts are found, set `ignore_underscore_` back to false and throw an `OptionAlreadyAdded` exception with a conflict message.
    - Set `ignore_underscore_` to the value of `value`.
- **Output**: Returns a pointer to the current `App` object (`this`).
- **Functions called**:
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
    - [`CLI::App::_compare_subcommand_names`](#App_compare_subcommand_names)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::add\_option<!-- {{#callable:CLI::App::add_option}} -->
The `add_option` function adds a new option to the `App` class, ensuring it does not conflict with existing options and setting up its default behavior.
- **Inputs**:
    - `option_name`: A string representing the name of the option to be added.
    - `option_callback`: A callback function that will be executed when the option is parsed.
    - `option_description`: A string providing a description of the option.
    - `defaulted`: A boolean indicating whether the option should capture its default value immediately.
    - `func`: A function that returns a string, used to capture the default value of the option.
- **Control Flow**:
    - Create an `Option` object `myopt` with the provided parameters and the current `App` context.
    - Check if `myopt` already exists in the `options_` vector; if not, proceed to add it.
    - If `myopt` has no long or short names, check for potential conflicts with existing positional options and throw an exception if conflicts are found.
    - If `myopt` has long or short names and a parent `App` exists, check for conflicts with the parent's options and throw an exception if conflicts are found.
    - If non-standard options are allowed and `myopt` has short names, check for conflicts with existing short options and throw an exception if conflicts are found.
    - Add `myopt` to the `options_` vector, set its default function, and capture its default string if `defaulted` is true.
    - Copy default settings from `option_defaults_` to the new option and capture the default string if necessary.
    - Return a pointer to the newly added `Option` object.
- **Output**: A pointer to the newly added `Option` object, or throws an exception if the option cannot be added due to conflicts.
- **Functions called**:
    - [`CLI::App::get_option_no_throw`](#Appget_option_no_throw)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::set\_help\_flag<!-- {{#callable:CLI::App::set_help_flag}} -->
The `set_help_flag` function sets or removes a help flag for the application, replacing any existing help flag if present.
- **Inputs**:
    - `flag_name`: A string representing the name of the help flag to be set; if empty, the help flag is removed.
    - `help_description`: A constant reference to a string that describes the help flag.
- **Control Flow**:
    - Check if a help flag already exists (`help_ptr_` is not null), and if so, remove it and set `help_ptr_` to null.
    - If `flag_name` is not empty, add a new help flag with the given `flag_name` and `help_description`, and set `help_ptr_` to this new flag.
    - Set the newly added help flag to be non-configurable.
- **Output**: Returns a pointer to the newly set help flag (`Option *`), or null if the help flag was removed.
- **Functions called**:
    - [`CLI::bool::remove_option`](#boolremove_option)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::set\_help\_all\_flag<!-- {{#callable:CLI::App::set_help_all_flag}} -->
The `set_help_all_flag` function sets or removes a 'help all' flag for the application, which provides a comprehensive help message when triggered.
- **Inputs**:
    - `help_name`: A string representing the name of the 'help all' flag; if empty, the flag is removed.
    - `help_description`: A string providing a description for the 'help all' flag.
- **Control Flow**:
    - Check if `help_all_ptr_` is not null, indicating an existing 'help all' flag, and remove it using [`remove_option`](#boolremove_option) if present.
    - Set `help_all_ptr_` to null to clear any existing 'help all' flag.
    - If `help_name` is not empty, add a new flag using `add_flag` with `help_name` and `help_description`, and set it to be non-configurable.
    - Return the pointer to the newly set or removed 'help all' flag.
- **Output**: Returns a pointer to the `Option` object representing the 'help all' flag, or null if the flag is removed.
- **Functions called**:
    - [`CLI::bool::remove_option`](#boolremove_option)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::set\_version\_flag<!-- {{#callable:CLI::App::set_version_flag}} -->
The `set_version_flag` function sets or removes a version flag for the application, which when triggered, throws a `CallForVersion` exception with the specified version string.
- **Inputs**:
    - `flag_name`: A string representing the name of the version flag to be set or removed.
    - `versionString`: A constant string representing the version information to be displayed when the version flag is triggered.
    - `version_help`: A constant string providing help information for the version flag.
- **Control Flow**:
    - Check if `version_ptr_` is not null, indicating an existing version flag, and remove it if present.
    - If `flag_name` is not empty, add a new version flag with a callback that throws a `CallForVersion` exception with `versionString` when triggered.
    - Set the `configurable` property of the new version flag to false, preventing it from being configured through a configuration file.
    - Return the pointer to the newly created or updated version flag.
- **Output**: Returns a pointer to the `Option` object representing the version flag.
- **Functions called**:
    - [`CLI::bool::remove_option`](#boolremove_option)
    - [`CLI::App::add_flag_callback`](#Appadd_flag_callback)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::\_add\_flag\_internal<!-- {{#callable:CLI::App::_add_flag_internal}} -->
The `_add_flag_internal` function adds a flag option to the application, handling default flag values and ensuring the flag is not positional.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `fun`: A callback function of type `CLI::callback_t` to be executed when the flag is triggered.
    - `flag_description`: A string describing the flag's purpose.
- **Control Flow**:
    - Initialize an `Option` pointer `opt` to `nullptr`.
    - Check if the `flag_name` has default flag values using `detail::has_default_flag_values`.
    - If default values exist, retrieve them using `detail::get_default_flag_values`, remove them from the flag name, and add the option using [`add_option`](#Appadd_option).
    - For each default flag name, add it to `opt->fnames_` and set `opt->default_flag_values_`.
    - If no default values exist, add the option using [`add_option`](#Appadd_option).
    - Check if the option is positional using `opt->get_positional()`.
    - If positional, remove the option and throw an `IncorrectConstruction::PositionalFlag` exception.
    - Set the option's multi-option policy to `MultiOptionPolicy::TakeLast`, expected count to 0, and required status to false.
    - Return the `opt` pointer.
- **Output**: Returns a pointer to the newly created `Option` object.
- **Functions called**:
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::bool::remove_option`](#boolremove_option)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::add\_flag\_callback<!-- {{#callable:CLI::App::add_flag_callback}} -->
The `add_flag_callback` function adds a flag to the application that triggers a specified callback function when the flag is set.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `function`: A callback function of type `std::function<void(void)>` that is executed when the flag is set.
    - `flag_description`: A string providing a description of the flag.
- **Control Flow**:
    - Define a lambda function `fun` that captures the `function` argument.
    - Within the lambda, use `lexical_cast` to convert the first result to a boolean `trigger`.
    - If the conversion is successful and `trigger` is true, call the `function`.
    - Return the result of the `lexical_cast` operation.
    - Call [`_add_flag_internal`](#App_add_flag_internal) with the flag name, the lambda function, and the flag description to add the flag to the application.
- **Output**: Returns a pointer to an `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::App::_add_flag_internal`](#App_add_flag_internal)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::add\_flag\_function<!-- {{#callable:CLI::App::add_flag_function}} -->
The `add_flag_function` method adds a flag to the application that triggers a specified function with the count of the flag occurrences as an argument.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `function`: A function that takes a `std::int64_t` argument, which will be called with the count of the flag occurrences.
    - `flag_description`: A string describing the flag's purpose or usage.
- **Control Flow**:
    - A lambda function `fun` is created, which captures the `function` argument and takes a `CLI::results_t` as input.
    - Inside the lambda, `lexical_cast` is used to convert the first element of `res` to a `std::int64_t` and store it in `flag_count`.
    - The `function` is then called with `flag_count` as its argument.
    - The lambda returns `true` to indicate successful processing.
    - The [`_add_flag_internal`](#App_add_flag_internal) method is called with `flag_name`, the lambda `fun`, and `flag_description`, which adds the flag to the application.
    - The method returns an `Option` pointer with a `multi_option_policy` set to `MultiOptionPolicy::Sum`.
- **Output**: Returns a pointer to an `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::App::_add_flag_internal`](#App_add_flag_internal)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::set\_config<!-- {{#callable:CLI::App::set_config}} -->
The `set_config` function configures a command-line option for reading a configuration file, with optional default filename and requirement settings.
- **Inputs**:
    - `option_name`: A string representing the name of the configuration option to be set.
    - `default_filename`: A string representing the default filename for the configuration file, if any.
    - `help_message`: A string providing a help message for the configuration option.
    - `config_required`: A boolean indicating whether the configuration file is required.
- **Control Flow**:
    - If `config_ptr_` is not null, remove the existing configuration option and set `config_ptr_` to null.
    - If `option_name` is not empty, add a new option with the given `option_name` and `help_message`.
    - If `config_required` is true, mark the new option as required.
    - If `default_filename` is not empty, set it as the default string for the option and enable force callback.
    - Set the option to be non-configurable and apply a multi-option policy to take the last value and reverse it.
    - Return the pointer to the newly configured option.
- **Output**: Returns a pointer to the newly configured `Option` object.
- **Functions called**:
    - [`CLI::bool::remove_option`](#boolremove_option)
    - [`CLI::App::add_option`](#Appadd_option)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::add\_subcommand<!-- {{#callable:CLI::App::add_subcommand}} -->
The [`add_subcommand`](#Appadd_subcommand) function adds a new subcommand to the current `App` object, ensuring the subcommand name is valid and creating a new `App` instance for the subcommand.
- **Inputs**:
    - `subcommand_name`: A string representing the name of the subcommand to be added.
    - `subcommand_description`: A string providing a description of the subcommand.
- **Control Flow**:
    - Check if `subcommand_name` is not empty and validate it using `detail::valid_name_string`.
    - If the first character of `subcommand_name` is invalid, throw an `IncorrectConstruction` exception.
    - Iterate over each character in `subcommand_name` to ensure they are valid, throwing an `IncorrectConstruction` exception if any invalid character is found.
    - Create a new `App` instance for the subcommand using `subcommand_description` and `subcommand_name`.
    - Call [`add_subcommand`](#Appadd_subcommand) with the newly created `App` instance to add it to the current `App` object.
- **Output**: Returns a pointer to the newly added subcommand `App` instance.
- **Functions called**:
    - [`CLI::App::add_subcommand`](#Appadd_subcommand)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::get\_subcommand<!-- {{#callable:CLI::App::get_subcommand}} -->
The `get_subcommand` function retrieves a subcommand from the list of subcommands in the `App` class that matches the given pointer, throwing an exception if the subcommand is not found.
- **Inputs**:
    - `subcom`: A pointer to the `App` object representing the subcommand to be retrieved.
- **Control Flow**:
    - Check if the input `subcom` is `nullptr` and throw an `OptionNotFound` exception if it is.
    - Iterate over the `subcommands_` vector, which contains pointers to subcommand `App` objects.
    - For each subcommand pointer, check if it matches the input `subcom`.
    - If a match is found, return the matching subcommand pointer.
    - If no match is found after iterating through all subcommands, throw an `OptionNotFound` exception with the name of the subcommand.
- **Output**: Returns a pointer to the `App` object that matches the input subcommand pointer, or throws an `OptionNotFound` exception if no match is found.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::get\_subcommand\_no\_throw<!-- {{#callable:CLI::App::get_subcommand_no_throw}} -->
The `get_subcommand_no_throw` function retrieves a subcommand by name from the `App` class without throwing an exception if the subcommand is not found.
- **Inputs**:
    - `subcom`: A `std::string` representing the name of the subcommand to retrieve.
- **Control Flow**:
    - The function calls the private method [`_find_subcommand`](#App_find_subcommand) with the provided subcommand name, and two `false` flags indicating that it should not ignore disabled subcommands or used subcommands.
    - The [`_find_subcommand`](#App_find_subcommand) method searches through the list of subcommands in the `App` class to find a match for the given name.
    - If a matching subcommand is found, it is returned; otherwise, `nullptr` is returned.
- **Output**: Returns a pointer to the `App` object representing the subcommand if found, or `nullptr` if not found.
- **Functions called**:
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::get\_option\_group<!-- {{#callable:CLI::App::get_option_group}} -->
The `get_option_group` function retrieves a subcommand from the `subcommands_` vector that matches a given group name and has an empty name, or throws an `OptionNotFound` exception if no such subcommand exists.
- **Inputs**:
    - `group_name`: A string representing the name of the group to search for among the subcommands.
- **Control Flow**:
    - Iterate over each subcommand in the `subcommands_` vector.
    - Check if the subcommand's name is empty and its group matches the `group_name`.
    - If a matching subcommand is found, return a pointer to it.
    - If no matching subcommand is found after the loop, throw an `OptionNotFound` exception with the `group_name`.
- **Output**: A pointer to the `App` object representing the subcommand that matches the specified group name.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::exit<!-- {{#callable:CLI::App::exit}} -->
The `exit` function handles different types of errors by printing appropriate messages to the output streams and returning the corresponding exit code.
- **Inputs**:
    - `e`: An `Error` object representing the error that occurred, which contains information such as the error name and exit code.
    - `out`: An output stream (`std::ostream`) where help or version information is printed if applicable.
    - `err`: An output stream (`std::ostream`) where error messages are printed if applicable.
- **Control Flow**:
    - Check if the error name is 'RuntimeError'; if so, return the exit code without printing anything.
    - If the error name is 'CallForHelp', print the help message to the `out` stream and return the exit code.
    - If the error name is 'CallForAllHelp', print the full help message to the `out` stream and return the exit code.
    - If the error name is 'CallForVersion', print the version information to the `out` stream and return the exit code.
    - If the exit code is not `ExitCodes::Success` and a failure message function is set, print the failure message to the `err` stream.
- **Output**: The function returns an integer representing the exit code associated with the error.
- **Functions called**:
    - [`CLI::CLI11_INLINE::string::help`](#stringhelp)
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::get\_option\_no\_throw<!-- {{#callable:CLI::App::get_option_no_throw}} -->
The `get_option_no_throw` function attempts to find an option by name within the current application and its nameless subcommands, returning a pointer to the option if found, or nullptr if not.
- **Inputs**:
    - `option_name`: A string representing the name of the option to search for.
- **Control Flow**:
    - Iterate over the `options_` vector of the current `App` instance.
    - For each `Option_p` in `options_`, check if the option's name matches `option_name` using `check_name`.
    - If a match is found, return the pointer to the option using `opt.get()`.
    - If no match is found in the current `App`, iterate over the `subcommands_` vector.
    - For each subcommand, check if it is nameless (i.e., `get_name().empty()`).
    - If a subcommand is nameless, recursively call `get_option_no_throw` on the subcommand.
    - If a match is found in a subcommand, return the pointer to the option.
    - If no match is found in any subcommand, return `nullptr`.
- **Output**: A pointer to the `Option` object if found, otherwise `nullptr`.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::\_find\_subcommand<!-- {{#callable:CLI::App::_find_subcommand}} -->
The `_find_subcommand` function searches for a subcommand within the `App` class's subcommands list that matches a given name, considering certain conditions like whether the subcommand is disabled or already used.
- **Inputs**:
    - `subc_name`: A string representing the name of the subcommand to search for.
    - `ignore_disabled`: A boolean flag indicating whether to ignore subcommands that are disabled.
    - `ignore_used`: A boolean flag indicating whether to ignore subcommands that have already been used.
- **Control Flow**:
    - Initialize a pointer `bcom` to `nullptr` to store the best matching subcommand found.
    - Iterate over each subcommand in the `subcommands_` vector.
    - If a subcommand is disabled and `ignore_disabled` is true, skip it.
    - If a subcommand has an empty name, recursively call `_find_subcommand` on it.
    - If a matching subcommand is found in the recursive call, check if `bcom` is already set; if so, return `nullptr` to indicate ambiguity.
    - If `allow_prefix_matching_` is false, return the found subcommand immediately.
    - Check the name of the current subcommand against `subc_name` using `check_name_detail`.
    - If a match is found and the subcommand is not used or `ignore_used` is false, return the subcommand if the match is exact or set `bcom` if it's a prefix match.
    - Return `bcom`, which is either the best match found or `nullptr` if no suitable subcommand was found.
- **Output**: Returns a pointer to the `App` object representing the matching subcommand, or `nullptr` if no match is found or if there is ambiguity.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::\_get\_fallthrough\_parent<!-- {{#callable:CLI::App::_get_fallthrough_parent}} -->
The function `_get_fallthrough_parent` retrieves the nearest valid parent `App` object that has a non-empty name, starting from the current `App` object's parent.
- **Inputs**: None
- **Control Flow**:
    - Check if `parent_` is `nullptr`, and if so, throw a `HorribleError` indicating no valid parent exists.
    - Initialize `fallthrough_parent` with `parent_`.
    - Enter a loop that continues as long as `fallthrough_parent` has a non-null `parent_` and its name is empty.
    - In each iteration, update `fallthrough_parent` to its own parent.
    - Return `fallthrough_parent`.
- **Output**: Returns a pointer to the nearest valid parent `App` object with a non-empty name.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)


---
#### App::\_compare\_subcommand\_names<!-- {{#callable:CLI::App::_compare_subcommand_names}} -->
The function `_compare_subcommand_names` checks for name conflicts between a given subcommand and a base command's subcommands, returning the conflicting name if found.
- **Inputs**:
    - `subcom`: A reference to the subcommand `App` object whose name and aliases are being checked for conflicts.
    - `base`: A reference to the base `App` object containing the list of subcommands to check against.
- **Control Flow**:
    - Initialize a static empty string `estring` to return in case of no conflicts.
    - Check if the `subcom` is disabled; if so, return `estring`.
    - Iterate over each subcommand `subc` in `base.subcommands_`.
    - Skip the iteration if `subc` is the same as `subcom` or if `subc` is disabled.
    - Check if `subcom`'s name matches any of `subc`'s names or aliases, returning the matching name if found.
    - Check if `subc`'s name matches any of `subcom`'s names or aliases, returning the matching name if found.
    - If `subc` is an option group (name is empty), recursively call `_compare_subcommand_names` to check deeper.
    - If `subcom` is an option group (name is empty), recursively call `_compare_subcommand_names` to check deeper.
    - Return `estring` if no conflicts are found.
- **Output**: A reference to a `std::string` containing the conflicting subcommand name or an empty string if no conflict is found.
- **See also**: [`CLI::App`](../App.hpp.driver.md#CLIApp)  (Data Structure)



# Functions

---
### remove\_option<!-- {{#callable:CLI::bool::remove_option}} -->
Removes an `Option` from the application, ensuring that it is no longer referenced by any other options.
- **Inputs**:
    - `opt`: A pointer to the `Option` object that needs to be removed from the application.
- **Control Flow**:
    - Iterates through all options in the application to remove any dependencies on the `opt` being removed.
    - Checks if `opt` is currently set as the help, help all, or config pointer and sets those pointers to nullptr if they match.
    - Uses `std::find_if` to locate the `opt` in the `options_` vector.
    - If found, erases the `opt` from the `options_` vector and returns true; otherwise, returns false.
- **Output**: Returns true if the `Option` was successfully removed; otherwise, returns false.


---
### remove\_subcommand<!-- {{#callable:CLI::bool::remove_subcommand}} -->
The `remove_subcommand` function removes a specified subcommand from the application if it exists.
- **Inputs**:
    - `subcom`: A pointer to the `App` object representing the subcommand to be removed.
- **Control Flow**:
    - Iterates through all subcommands to ensure that no other subcommands have dependencies on the subcommand being removed by calling `remove_excludes` and `remove_needs`.
    - Uses `std::find_if` to locate the specified subcommand in the `subcommands_` vector.
    - If the subcommand is found, it is erased from the `subcommands_` vector and the function returns true.
    - If the subcommand is not found, the function returns false.
- **Output**: Returns a boolean indicating whether the subcommand was successfully removed (true) or not found (false).


---
### get\_subcommand\_ptr<!-- {{#callable:CLI::CLI11_INLINE::App_p::get_subcommand_ptr}} -->
Retrieves a pointer to a subcommand at a specified index.
- **Inputs**:
    - `index`: An integer representing the index of the desired subcommand.
- **Control Flow**:
    - Checks if the provided index is non-negative.
    - Converts the index to an unsigned integer.
    - Checks if the unsigned index is within the bounds of the `subcommands_` vector.
    - If valid, returns the subcommand pointer at the specified index.
    - If invalid, throws an `OptionNotFound` exception with the index as a message.
- **Output**: Returns a pointer to the subcommand at the specified index, or throws an exception if the index is out of bounds.


---
### count\_all<!-- {{#callable:CLI::CLI11_INLINE::size_t::count_all}} -->
Counts the total number of options and subcommands parsed in the `App` instance.
- **Inputs**: None
- **Control Flow**:
    - Initializes a counter `cnt` to zero.
    - Iterates over each option in `options_` and adds the count of each option to `cnt`.
    - Iterates over each subcommand in `subcommands_` and adds the result of `count_all()` from each subcommand to `cnt`.
    - If the name of the app is not empty, adds the number of times the subcommand was called (stored in `parsed_`) to `cnt`.
- **Output**: Returns the total count of options and subcommands that have been parsed.


---
### clear<!-- {{#callable:CLI::void::clear}} -->
The `clear` method resets the state of the `App` instance by clearing parsed data and options.
- **Inputs**: None
- **Control Flow**:
    - Sets `parsed_` to 0, indicating no commands have been parsed.
    - Sets `pre_parse_called_` to false, indicating that pre-parsing has not occurred.
    - Clears the `missing_` vector, which tracks missing options.
    - Clears the `parsed_subcommands_` vector, which tracks subcommands that have been parsed.
    - Iterates over each option in `options_` and calls their `clear` method to reset their state.
    - Iterates over each subcommand in `subcommands_` and calls their `clear` method to reset their state.
- **Output**: The function does not return a value; it modifies the internal state of the `App` instance.


---
### parse<!-- {{#callable:CLI::void::parse}} -->
The `parse` function processes command-line arguments, validates them, and configures the application accordingly.
- **Inputs**:
    - `args`: A rvalue reference to a vector of strings containing command-line arguments to be parsed.
- **Control Flow**:
    - Checks if the application has already been parsed and clears previous state if necessary.
    - Increments the `parsed_` counter to indicate that parsing is in progress.
    - Calls the [`_validate`](#void_validate) method to ensure the current configuration is valid.
    - Calls the [`_configure`](#void_configure) method to set up the application state based on the current configuration.
    - Sets the `parent_` pointer to nullptr, indicating that this instance is the top-level application.
    - Resets the `parsed_` counter to 0 after configuration.
    - Calls the [`_parse`](#void_parse) method to process the provided arguments.
    - Invokes the [`run_callback`](#voidrun_callback) method to execute any registered callbacks after parsing.
- **Output**: The function does not return a value; it modifies the internal state of the `App` instance based on the parsed arguments and may trigger callbacks.
- **Functions called**:
    - [`CLI::void::clear`](#voidclear)
    - [`CLI::void::_validate`](#void_validate)
    - [`CLI::void::_configure`](#void_configure)
    - [`CLI::void::_parse`](#void_parse)
    - [`CLI::void::run_callback`](#voidrun_callback)


---
### maybe\_narrow<!-- {{#callable:CLI::detail::std::string::maybe_narrow}} -->
The `maybe_narrow` function converts a wide character string to a narrow character string.
- **Inputs**:
    - `str`: A pointer to a wide character string (`const wchar_t*`) that needs to be converted to a narrow string.
- **Control Flow**:
    - The function directly calls the `narrow` function with the input wide character string.
    - The `narrow` function is expected to handle the conversion from wide to narrow character representation.
- **Output**: Returns a `std::string` that represents the converted narrow character string.


---
### parse\_char\_t<!-- {{#callable:CLI::void::parse_char_t}} -->
Parses command line arguments of type `CharT` and sets the application name if not already set.
- **Inputs**:
    - `argc`: An integer representing the number of command line arguments.
    - `argv`: A pointer to an array of command line arguments of type `CharT`.
- **Control Flow**:
    - Checks if the application name is empty or if it has an automatic name flag set.
    - If true, sets the application name using the first command line argument after narrowing it to a string.
    - Creates a vector to hold the command line arguments excluding the application name.
    - Iterates over the command line arguments in reverse order, narrowing each argument and adding it to the vector.
    - Calls the [`parse`](#voidparse) method with the vector of arguments.
- **Output**: The function does not return a value; it modifies the state of the application by setting the name and parsing the arguments.
- **Functions called**:
    - [`CLI::void::parse`](#voidparse)


---
### parse\_from\_stream<!-- {{#callable:CLI::void::parse_from_stream}} -->
The `parse_from_stream` function processes input from a given input stream, validating and configuring the application before parsing the stream.
- **Inputs**:
    - `input`: A reference to an `std::istream` object from which the application will read input data.
- **Control Flow**:
    - Checks if the application has not been parsed yet by evaluating `parsed_`.
    - If not parsed, calls `_validate()` to ensure the application is in a valid state.
    - Calls `_configure()` to set up the application based on its current state.
    - Calls `_parse_stream(input)` to read and process the input from the provided stream.
    - Finally, invokes `run_callback()` to execute any registered callbacks after parsing.
- **Output**: The function does not return a value; it modifies the state of the application based on the parsed input and may trigger callbacks.
- **Functions called**:
    - [`CLI::void::_validate`](#void_validate)
    - [`CLI::void::_configure`](#void_configure)
    - [`CLI::void::_parse_stream`](#void_parse_stream)
    - [`CLI::void::run_callback`](#voidrun_callback)


---
### get\_subcommands<!-- {{#callable:CLI::std::vector<App *>::get_subcommands}} -->
Retrieves a vector of subcommands from the `App` class, optionally filtered by a provided predicate.
- **Inputs**:
    - `filter`: A callable function that takes a pointer to an `App` object and returns a boolean, used to filter the subcommands.
- **Control Flow**:
    - Initializes a vector `subcomms` with the size of `subcommands_` to hold pointers to the subcommands.
    - Uses `std::transform` to populate `subcomms` with raw pointers from `subcommands_`.
    - Checks if the `filter` function is provided; if so, it uses `std::remove_if` to remove elements from `subcomms` that do not satisfy the filter condition.
    - Returns the filtered or unfiltered vector of subcommands.
- **Output**: Returns a vector of pointers to `App` objects representing the subcommands, potentially filtered based on the provided predicate.


---
### remove\_excludes<!-- {{#callable:CLI::bool::remove_excludes}} -->
The `remove_excludes` method removes a specified `App` instance from the list of excluded subcommands and recursively removes the current instance from the excluded list of the specified instance.
- **Inputs**:
    - `app`: A pointer to an `App` instance that is to be removed from the list of excluded subcommands.
- **Control Flow**:
    - The method begins by searching for the specified `app` in the `exclude_subcommands_` list.
    - If the `app` is not found, the method returns false.
    - If the `app` is found, it is removed from the `exclude_subcommands_` list.
    - The method then recursively calls `remove_excludes` on the found `app`, passing the current instance as an argument.
    - Finally, the method returns true to indicate that the removal was successful.
- **Output**: The method returns a boolean value: true if the `app` was successfully removed from the exclusions, and false if it was not found in the list.


---
### remove\_needs<!-- {{#callable:CLI::bool::remove_needs}} -->
The `remove_needs` function removes a specified `App` instance from the list of required subcommands.
- **Inputs**:
    - `app`: A pointer to the `App` instance that needs to be removed from the list of required subcommands.
- **Control Flow**:
    - The function uses `std::find` to search for the specified `app` in the `need_subcommands_` vector.
    - If the `app` is not found (i.e., the iterator equals the end of the vector), the function returns false.
    - If the `app` is found, it is erased from the `need_subcommands_` vector, and the function returns true.
- **Output**: Returns a boolean value indicating whether the removal was successful (true) or if the `app` was not found in the list (false).


---
### help<!-- {{#callable:CLI::FailureMessage::std::string::help}} -->
Generates a help message string based on the provided application and error.
- **Inputs**:
    - `app`: A pointer to an `App` object that contains the application's help information.
    - `e`: An `Error` object that provides details about the error that occurred.
- **Control Flow**:
    - Constructs a header string that includes the error name and message from the `Error` object.
    - Appends the help information from the `App` object by calling its `help()` method.
    - Returns the complete help message string.
- **Output**: A string containing the formatted error message followed by the application's help information.


---
### version<!-- {{#callable:CLI::CLI11_INLINE::string::version}} -->
The `version` method retrieves the version information of the application.
- **Inputs**:
    - `this`: A constant reference to the current instance of the `App` class.
- **Control Flow**:
    - Check if `version_ptr_` is not null to proceed with version retrieval.
    - Store the current results of `version_ptr_` in `rv` for later restoration.
    - Clear the results of `version_ptr_` and add a result indicating a version request.
    - Attempt to run the callback associated with `version_ptr_`.
    - If a `CLI::CallForVersion` exception is caught, store the exception message in `val`.
    - Restore the original results to `version_ptr_`.
- **Output**: Returns a string containing the version information if available, or an empty string if not.


---
### get\_options<!-- {{#callable:CLI::std::vector<Option *>::get_options}} -->
The `get_options` function retrieves a filtered list of `Option` pointers from the application, including options from subcommands.
- **Inputs**:
    - `filter`: A callable function that takes a pointer to an `Option` and returns a boolean, used to filter the options.
- **Control Flow**:
    - Creates a vector `options` to hold pointers to `Option` objects, initialized with the size of `options_`.
    - Uses `std::transform` to populate `options` with raw pointers from `options_`.
    - If a `filter` is provided, it uses `std::remove_if` to erase options that do not satisfy the filter condition.
    - Iterates over each subcommand in `subcommands_`, checking for nameless subcommands that belong to a specific group.
    - Recursively calls `get_options` on each relevant subcommand to gather their options, appending them to the `options` vector.
    - Returns the final list of options.
- **Output**: Returns a vector of pointers to `Option` objects that match the filter criteria, including options from subcommands.


---
### get\_display\_name<!-- {{#callable:CLI::CLI11_INLINE::string::get_display_name}} -->
Returns a display name for the application, optionally including its aliases.
- **Inputs**:
    - `with_aliases`: A boolean flag indicating whether to include aliases in the display name.
- **Control Flow**:
    - Checks if the `name_` member variable is empty; if so, constructs a display name indicating the option group.
    - If `aliases_` is empty or `with_aliases` is false, returns the `name_` directly.
    - If `with_aliases` is true and there are aliases, constructs a display name by appending each alias to the `name_`.
- **Output**: Returns a string representing the display name of the application, which may include its aliases if specified.


---
### check\_name<!-- {{#callable:CLI::CLI11_INLINE::check_name}} -->
The `check_name` function verifies if a given name matches the application's name or any of its aliases.
- **Inputs**:
    - `name_to_check`: A `std::string` representing the name to be checked against the application's name and aliases.
- **Control Flow**:
    - The function calls [`check_name_detail`](#NameMatchcheck_name_detail) with the `name_to_check` after moving it to avoid unnecessary copies.
    - The result of [`check_name_detail`](#NameMatchcheck_name_detail) is compared to `NameMatch::none` to determine if there was a match.
- **Output**: Returns a boolean value indicating whether the `name_to_check` matches the application's name or any of its aliases.
- **Functions called**:
    - [`CLI::CLI11_INLINE::NameMatch::check_name_detail`](#NameMatchcheck_name_detail)


---
### check\_name\_detail<!-- {{#callable:CLI::CLI11_INLINE::NameMatch::check_name_detail}} -->
The `check_name_detail` function checks if a given name matches the application's name or any of its aliases, considering case and underscore options.
- **Inputs**:
    - `name_to_check`: A `std::string` representing the name to be checked against the application's name and aliases.
- **Control Flow**:
    - The function initializes a local variable `local_name` with the application's name.
    - If `ignore_underscore_` is true, it removes underscores from both `local_name` and `name_to_check` using `detail::remove_underscore`.
    - If `ignore_case_` is true, it converts both `local_name` and `name_to_check` to lowercase using `detail::to_lower`.
    - It checks for an exact match between `local_name` and `name_to_check`, returning `NameMatch::exact` if they match.
    - If prefix matching is allowed and `name_to_check` is shorter than `local_name`, it checks if `local_name` starts with `name_to_check`, returning `NameMatch::prefix` if true.
    - The function iterates through the `aliases_` vector, applying the same checks for each alias.
    - If no matches are found, it returns `NameMatch::none`.
- **Output**: Returns an enumeration value of type `App::NameMatch`, indicating whether the name matches exactly, matches as a prefix, or does not match at all.


---
### get\_groups<!-- {{#callable:CLI::CLI11_INLINE::vector<std::string>::App::get_groups}} -->
The `get_groups` method retrieves a list of unique groups from the options associated with the application.
- **Inputs**: None
- **Control Flow**:
    - Initialize an empty vector `groups` to store unique group names.
    - Iterate over each option in the `options_` vector.
    - For each option, check if its group name is already in the `groups` vector using `std::find`.
    - If the group name is not found, add it to the `groups` vector.
- **Output**: Returns a vector of strings containing unique group names from the options.


---
### remaining<!-- {{#callable:CLI::CLI11_INLINE::vector<std::string>::App::remaining}} -->
The `remaining` function retrieves a list of missing options or arguments from the current application and its subcommands.
- **Inputs**:
    - `recurse`: A boolean flag indicating whether to recursively check subcommands for missing options.
- **Control Flow**:
    - Initializes an empty vector `miss_list` to store missing options.
    - Iterates over the `missing_` member to populate `miss_list` with missing options from the current application.
    - If `recurse` is true, checks if extras are allowed and iterates over subcommands to gather their missing options if they are nameless.
    - Recursively calls `remaining` on each parsed subcommand to gather their missing options and appends them to `miss_list`.
- **Output**: Returns a vector of strings containing the names of missing options or arguments.


---
### remaining\_for\_passthrough<!-- {{#callable:CLI::CLI11_INLINE::vector<std::string>::App::remaining_for_passthrough}} -->
The `remaining_for_passthrough` function retrieves a list of missing arguments and reverses their order.
- **Inputs**:
    - `recurse`: A boolean flag indicating whether to include missing arguments from subcommands.
- **Control Flow**:
    - Calls the [`remaining`](#Appremaining) method to get a list of missing arguments based on the `recurse` flag.
    - Reverses the order of the elements in the `miss_list` vector.
- **Output**: Returns a vector of strings containing the reversed list of missing arguments.
- **Functions called**:
    - [`CLI::CLI11_INLINE::vector<std::string>::App::remaining`](#Appremaining)


---
### remaining\_size<!-- {{#callable:CLI::CLI11_INLINE::size_t::remaining_size}} -->
Calculates the number of remaining options that are not marked as positional, optionally including those from subcommands.
- **Inputs**:
    - `recurse`: A boolean flag indicating whether to include the remaining options from subcommands in the count.
- **Control Flow**:
    - Counts the number of options in the `missing_` vector that are not classified as `POSITIONAL_MARK`.
    - If `recurse` is true, iterates over each subcommand in `subcommands_` and adds their remaining size to the total count.
- **Output**: Returns the total count of remaining options as a `std::size_t`.


---
### \_validate<!-- {{#callable:CLI::void::_validate}} -->
Validates the configuration of command-line options and subcommands within an application.
- **Inputs**:
    - `this`: A constant reference to the current instance of the `App` class.
- **Control Flow**:
    - Counts the number of positional-only arguments that are expected and checks if their count exceeds the allowed limit.
    - If the count of positional arguments exceeds one, it checks how many of them are required and throws an `InvalidError` if the requirements are not met.
    - Iterates through all subcommands, recursively calling `_validate` on each to ensure their configurations are also valid.
    - Counts the number of nameless subcommands and checks if the minimum and maximum required options are satisfied, throwing an `InvalidError` if not.
- **Output**: The function does not return a value; instead, it throws exceptions if validation fails.


---
### \_configure<!-- {{#callable:CLI::void::_configure}} -->
The `_configure` method initializes the state of the `App` object and its subcommands based on the current startup mode.
- **Inputs**: None
- **Control Flow**:
    - Checks the `default_startup` mode to set the `disabled_` state of the `App` object.
    - Iterates over each subcommand in `subcommands_`.
    - For each subcommand, clears its name if it has an automatic name.
    - Sets `fallthrough_` and `prefix_command_` to false if the subcommand's name is empty.
    - Assigns the parent of the subcommand to the current `App` object.
    - Recursively calls `_configure` on each subcommand.
- **Output**: The function does not return a value; it modifies the state of the `App` object and its subcommands.


---
### run\_callback<!-- {{#callable:CLI::void::run_callback}} -->
Executes registered callbacks for the application and its subcommands based on the parsing state.
- **Inputs**:
    - `final_mode`: A boolean flag indicating whether this is the final callback execution phase.
    - `suppress_final_callback`: A boolean flag that, when true, prevents the execution of the final callback.
- **Control Flow**:
    - Calls `pre_callback()` to perform any necessary pre-execution setup.
    - If not in final mode and a parse complete callback is set, it executes the `parse_complete_callback_`.
    - Iterates over all subcommands and recursively calls `run_callback()` on each subcommand that is a direct child.
    - Iterates over option groups and calls `run_callback()` on those that have been parsed.
    - If the final callback is set, parsed items exist, and suppression is not requested, it executes the `final_callback_`.
- **Output**: This function does not return a value but triggers various callbacks based on the application's state and the provided flags.
- **Functions called**:
    - [`CLI::std::vector<const App *>::get_subcommands`](#vector<const App *>get_subcommands)
    - [`CLI::CLI11_INLINE::size_t::count_all`](#size_tcount_all)


---
### \_valid\_subcommand<!-- {{#callable:CLI::CLI11_INLINE::_valid_subcommand}} -->
Checks if a given subcommand is valid within the current application context.
- **Inputs**:
    - `current`: A `std::string` representing the name of the subcommand to validate.
    - `ignore_used`: A `bool` indicating whether to ignore already used subcommands in the validation process.
- **Control Flow**:
    - First, it checks if the maximum number of subcommands has been reached; if so, it checks the parent application for validity.
    - It attempts to find the specified subcommand using the [`_find_subcommand`](#App_find_subcommand) method.
    - If the subcommand is found, it returns true.
    - If the subcommand is not found and fallthrough is allowed, it checks the parent application for validity.
    - If no valid subcommand is found, it returns false.
- **Output**: Returns a `bool` indicating whether the specified subcommand is valid.
- **Functions called**:
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)


---
### \_recognize<!-- {{#callable:CLI::CLI11_INLINE::Classifier::_recognize}} -->
The `_recognize` function classifies a given command string into various categories such as subcommand, long option, short option, or positional argument.
- **Inputs**:
    - `current`: A `std::string` representing the command or argument to be classified.
    - `ignore_used_subcommands`: A `bool` indicating whether to ignore subcommands that have already been used.
- **Control Flow**:
    - Checks if the `current` string is a positional marker ('--') and returns `POSITIONAL_MARK` if true.
    - Validates if `current` is a valid subcommand using [`_valid_subcommand`](#CLI11_INLINE_valid_subcommand) and returns `SUBCOMMAND` if true.
    - Attempts to split `current` as a long option using `detail::split_long` and returns `LONG` if successful.
    - Attempts to split `current` as a short option using `detail::split_short` and checks if it resembles a number or option.
    - If `allow_windows_style_options_` is true, checks if `current` is a Windows-style option and returns `WINDOWS_STYLE` if true.
    - Checks if `current` is a subcommand terminator ('++') and returns `SUBCOMMAND_TERMINATOR` if true.
    - If `current` contains a dot, it checks for a subcommand and recursively calls `_recognize` on the substring after the dot.
    - If none of the conditions are met, returns `NONE`.
- **Output**: Returns a value from the `detail::Classifier` enumeration indicating the classification of the `current` command.
- **Functions called**:
    - [`CLI::CLI11_INLINE::_valid_subcommand`](#CLI11_INLINE_valid_subcommand)
    - [`CLI::App::get_option_no_throw`](#Appget_option_no_throw)
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)


---
### \_process\_config\_file<!-- {{#callable:CLI::void::_process_config_file}} -->
Processes the configuration file for the application.
- **Inputs**:
    - `this`: A pointer to the current instance of the `App` class.
- **Control Flow**:
    - Checks if `config_ptr_` is not null to proceed with processing.
    - Determines if a configuration file is required and if any files have been provided.
    - If no files are provided and a configuration is required, throws a `FileError`.
    - Iterates through the list of configuration files and processes each one.
    - If no files were successfully processed, clears the results and runs the callback.
- **Output**: No return value; the function modifies the state of the application based on the configuration file processing.
- **Functions called**:
    - [`CLI::bool::_process_config_file`](#bool_process_config_file)


---
### \_process\_env<!-- {{#callable:CLI::void::_process_env}} -->
The `_process_env` function processes environment variables for options and subcommands in the application.
- **Inputs**:
    - `none`: This function does not take any input parameters.
- **Control Flow**:
    - Iterates over each option in the `options_` vector.
    - For each option, checks if it has not been set and has an associated environment variable name.
    - Retrieves the value of the environment variable using `detail::get_environment_value`.
    - Validates the retrieved environment variable value using the option's `_validate` method.
    - If the validation is successful (result is empty), adds the environment variable value to the option's results.
    - Iterates over each subcommand in the `subcommands_` vector.
    - For each subcommand, checks if it has no name or if it has results and has not completed parsing.
    - Recursively calls `_process_env` on each subcommand.
- **Output**: This function does not return a value; it modifies the state of options and subcommands by adding results based on environment variables.


---
### \_process\_callbacks<!-- {{#callable:CLI::void::_process_callbacks}} -->
Processes callbacks for subcommands and options in the application.
- **Inputs**:
    - `none`: The function does not take any input parameters.
- **Control Flow**:
    - Iterates over each subcommand in `subcommands_` to process those with a complete callback and non-empty counts.
    - For each option in `options_`, it checks if the callback has not been run and executes it if necessary.
    - Finally, it processes any remaining subcommands that do not have a complete callback.
- **Output**: The function does not return a value; it executes callbacks associated with subcommands and options.


---
### \_process\_help\_flags<!-- {{#callable:CLI::void::_process_help_flags}} -->
Processes help flags for the application, determining if help or all help should be triggered.
- **Inputs**:
    - `trigger_help`: A boolean indicating whether the help flag has been triggered.
    - `trigger_all_help`: A boolean indicating whether the all help flag has been triggered.
- **Control Flow**:
    - Retrieve pointers to the help and help all options using `get_help_ptr()` and `get_help_all_ptr()`.
    - Check if the help option is present and has been triggered, setting `trigger_help` to true if so.
    - Check if the help all option is present and has been triggered, setting `trigger_all_help` to true if so.
    - If there are parsed subcommands, recursively call `_process_help_flags` on each subcommand.
    - If no subcommands are present and `trigger_all_help` is true, throw a `CallForAllHelp` exception.
    - If no subcommands are present and `trigger_help` is true, throw a `CallForHelp` exception.
- **Output**: The function does not return a value but may throw exceptions to indicate that help or all help should be displayed.


---
### \_process\_requirements<!-- {{#callable:CLI::void::_process_requirements}} -->
Processes the requirements for options and subcommands in the application.
- **Inputs**:
    - `none`: The function does not take any input arguments.
- **Control Flow**:
    - Initializes a boolean flag `excluded` to track if any options or subcommands are excluded.
    - Iterates over `exclude_options_` and `exclude_subcommands_` to check if any are counted, setting `excluded` and `excluder` accordingly.
    - If excluded and there are counted options, throws an `ExcludesError` with the name of the excluder.
    - Initializes a boolean flag `missing_needed` to track if any required options or subcommands are missing.
    - Iterates over `need_options_` and `need_subcommands_` to check if any are missing, setting `missing_needed` and `missing_need` accordingly.
    - If missing and there are counted options, throws a `RequiresError` with the name of the missing requirement.
    - Counts the number of used options and checks for required but empty options, throwing `RequiredError` if any are found.
    - Checks if the minimum required subcommands are met, throwing `RequiredError::Subcommand` if not.
    - Counts unnamed subcommands that are used and checks if the used options meet the required minimum and maximum, throwing `RequiredError::Option` if they do not.
    - Recursively processes requirements for each subcommand, throwing `RequiredError` if any required subcommand is missing.
- **Output**: The function does not return a value but may throw various errors (e.g., `ExcludesError`, `RequiresError`, `RequiredError`) based on the validation of options and subcommands.
- **Functions called**:
    - [`CLI::CLI11_INLINE::size_t::count_all`](#size_tcount_all)
    - [`CLI::CLI11_INLINE::string::get_display_name`](#stringget_display_name)
    - [`CLI::std::vector<const App *>::get_subcommands`](#vector<const App *>get_subcommands)


---
### \_process<!-- {{#callable:CLI::void::_process}} -->
Processes the application by handling help flags, configuration files, environment variables, callbacks, and requirements.
- **Inputs**: None
- **Control Flow**:
    - Calls `_process_help_flags()` to check for help requests before any other processing.
    - Enters a try block to handle potential `FileError` exceptions during configuration file processing.
    - Calls `_process_config_file()` to handle the application's configuration file.
    - If no configuration errors occur, calls `_process_env()` to handle environment variables.
    - Catches `CLI::FileError` exceptions to process callbacks before rethrowing the exception.
    - Calls `_process_callbacks()` to execute any registered callbacks.
    - Finally, calls `_process_requirements()` to validate any required options or subcommands.
- **Output**: The function does not return a value but may throw exceptions if errors are encountered during processing.
- **Functions called**:
    - [`CLI::void::_process_help_flags`](#void_process_help_flags)
    - [`CLI::bool::_process_config_file`](#bool_process_config_file)
    - [`CLI::void::_process_env`](#void_process_env)
    - [`CLI::void::_process_callbacks`](#void_process_callbacks)
    - [`CLI::void::_process_requirements`](#void_process_requirements)


---
### \_process\_extras<!-- {{#callable:CLI::void::_process_extras}} -->
Processes any extra command-line arguments that are not recognized as valid options or subcommands.
- **Inputs**:
    - `args`: A reference to a vector of strings representing the command-line arguments to be processed.
- **Control Flow**:
    - Checks if extras are allowed or if prefix commands are enabled.
    - If extras are not allowed, it counts the remaining unprocessed arguments.
    - If there are remaining arguments, it assigns them to 'args' and throws an 'ExtrasError'.
    - Iterates through each subcommand in 'subcommands_' and recursively calls '_process_extras' if the subcommand has been invoked.
- **Output**: The function does not return a value but may throw an 'ExtrasError' if there are unrecognized arguments.
- **Functions called**:
    - [`CLI::CLI11_INLINE::size_t::remaining_size`](#size_tremaining_size)
    - [`CLI::CLI11_INLINE::vector<std::string>::App::remaining`](#Appremaining)


---
### increment\_parsed<!-- {{#callable:CLI::void::increment_parsed}} -->
Increments the `parsed_` count of the `App` instance and recursively increments the parsed count for all subcommands that do not have a name.
- **Inputs**: None
- **Control Flow**:
    - The function first increments the `parsed_` member variable of the `App` instance.
    - It then iterates over each subcommand in the `subcommands_` vector.
    - For each subcommand, it checks if the subcommand's name is empty.
    - If the name is empty, it recursively calls `increment_parsed()` on that subcommand.
- **Output**: The function does not return a value; it modifies the internal state of the `App` instance and its subcommands.


---
### \_parse<!-- {{#callable:CLI::void::_parse}} -->
The `_parse` function processes command-line arguments by incrementing the parsed count, triggering pre-parse actions, parsing each argument, and handling any remaining items.
- **Inputs**:
    - `args`: A vector of strings representing command-line arguments to be parsed.
- **Control Flow**:
    - The function starts by incrementing the parsed count using `increment_parsed()`.
    - It triggers pre-parse actions with `_trigger_pre_parse(args.size())`.
    - A boolean flag `positional_only` is initialized to false.
    - A while loop iterates as long as there are arguments in `args`, calling `_parse_single(args, positional_only)` for each argument.
    - After parsing, it calls `_process()` to handle the parsed data.
    - Finally, it checks for any leftover arguments and processes them with `_process_extras()`.
- **Output**: The function does not return a value but modifies the state of the `App` instance by updating the parsed count, processing the arguments, and potentially throwing errors if there are unprocessed items.
- **Functions called**:
    - [`CLI::void::increment_parsed`](#voidincrement_parsed)
    - [`CLI::void::_trigger_pre_parse`](#void_trigger_pre_parse)
    - [`CLI::bool::_parse_single`](#bool_parse_single)
    - [`CLI::void::_process`](#void_process)
    - [`CLI::void::_process_extras`](#void_process_extras)


---
### \_parse\_stream<!-- {{#callable:CLI::void::_parse_stream}} -->
The `_parse_stream` function processes configuration data from an input stream.
- **Inputs**:
    - `input`: A reference to an input stream (`std::istream`) from which configuration data is read.
- **Control Flow**:
    - Calls `from_config` method of `config_formatter_` to read configuration values from the input stream.
    - Passes the retrieved values to [`_parse_config`](#void_parse_config) for further processing.
    - Increments the count of parsed configurations using [`increment_parsed`](#voidincrement_parsed).
    - Triggers pre-parse actions with the size of the values using [`_trigger_pre_parse`](#void_trigger_pre_parse).
    - Processes the parsed configurations with [`_process`](#void_process).
    - Checks for any leftover items in the input stream and processes them with [`_process_extras`](#void_process_extras).
- **Output**: The function does not return a value but may throw errors if there are leftover items in the input stream, depending on the configuration settings.
- **Functions called**:
    - [`CLI::void::_parse_config`](#void_parse_config)
    - [`CLI::void::increment_parsed`](#voidincrement_parsed)
    - [`CLI::void::_trigger_pre_parse`](#void_trigger_pre_parse)
    - [`CLI::void::_process`](#void_process)
    - [`CLI::void::_process_extras`](#void_process_extras)


---
### \_parse\_config<!-- {{#callable:CLI::void::_parse_config}} -->
The `_parse_config` function processes a vector of `ConfigItem` objects, parsing each item and throwing an error if any extras are found and extras are not allowed.
- **Inputs**:
    - `args`: A constant reference to a vector of `ConfigItem` objects that represent configuration items to be parsed.
- **Control Flow**:
    - Iterates over each `ConfigItem` in the `args` vector.
    - Calls the [`_parse_single_config`](#bool_parse_single_config) method for each `ConfigItem`.
    - If [`_parse_single_config`](#bool_parse_single_config) returns false and `allow_config_extras_` is set to error mode, a `ConfigError::Extras` exception is thrown.
- **Output**: The function does not return a value; it may throw a `ConfigError::Extras` exception if there are unrecognized configuration items.
- **Functions called**:
    - [`CLI::bool::_parse_single_config`](#bool_parse_single_config)


---
### \_add\_flag\_like\_result<!-- {{#callable:CLI::bool::_add_flag_like_result}} -->
The `_add_flag_like_result` function processes flag-like results for a given option based on the provided configuration item and input values.
- **Inputs**:
    - `op`: A pointer to an `Option` object that represents the command-line option being processed.
    - `item`: A `ConfigItem` reference that contains configuration details, including the expected inputs for the option.
    - `inputs`: A vector of strings representing the input values provided for the option.
- **Control Flow**:
    - Checks if the number of inputs in `item` is less than or equal to 1 to determine if flag parsing is needed.
    - Converts the configuration item to a flag representation using `config_formatter_`.
    - If the option has flag override disabled, checks the flag value and potentially retrieves a default value.
    - If not converted, checks if the result is not empty or if the expected maximum items is less than or equal to 1, then retrieves the flag value.
    - Adds the result to the option using `op->add_result(res)`.
    - If the number of inputs exceeds the expected maximum, throws an `ArgumentMismatch` or `ConversionError` based on the option's settings.
    - Validates each input against known flag values and adds valid inputs to the option, throwing an `InvalidError` for any invalid inputs.
- **Output**: Returns a boolean indicating whether the operation was successful, specifically true if the flag-like result was processed and added, or false if no processing occurred.


---
### \_parse\_single\_config<!-- {{#callable:CLI::bool::_parse_single_config}} -->
The `_parse_single_config` function processes a single configuration item, handling nested subcommands and various configuration directives.
- **Inputs**:
    - `item`: A `ConfigItem` reference representing the configuration item to be parsed.
    - `level`: A `std::size_t` indicating the current level of nested subcommands being processed.
- **Control Flow**:
    - Checks if the current level is less than the number of parents in the `item`, and if so, attempts to parse the item in the corresponding subcommand.
    - Handles section opening with '++' by incrementing the parsed count and triggering pre-parse actions.
    - Handles section closing with '--' by processing callbacks and requirements if the configuration is complete.
    - Attempts to retrieve an option corresponding to the item name, checking for long, short, and plain names.
    - If the option is not found, it captures missing items based on the configuration extras mode.
    - If the option is found but not configurable, it throws an error or ignores based on the configuration extras mode.
    - If the option is empty, it processes the inputs and runs the option's callback.
- **Output**: Returns a boolean indicating whether the parsing of the configuration item was successful.
- **Functions called**:
    - [`CLI::App::get_subcommand_no_throw`](#Appget_subcommand_no_throw)
    - [`CLI::void::increment_parsed`](#voidincrement_parsed)
    - [`CLI::void::_trigger_pre_parse`](#void_trigger_pre_parse)
    - [`CLI::void::_process_callbacks`](#void_process_callbacks)
    - [`CLI::void::_process_requirements`](#void_process_requirements)
    - [`CLI::void::run_callback`](#voidrun_callback)
    - [`CLI::App::get_option_no_throw`](#Appget_option_no_throw)
    - [`CLI::bool::_add_flag_like_result`](#bool_add_flag_like_result)


---
### \_parse\_single<!-- {{#callable:CLI::bool::_parse_single}} -->
The `_parse_single` function processes a single argument from a command line input, classifying it and determining the appropriate action based on its type.
- **Inputs**:
    - `args`: A reference to a vector of strings representing the command line arguments to be parsed.
    - `positional_only`: A reference to a boolean that indicates whether only positional arguments are allowed.
- **Control Flow**:
    - The function begins by initializing a return value `retval` to true.
    - It classifies the last argument in `args` using the [`_recognize`](#Classifier_recognize) method, which returns a `Classifier` type.
    - A switch statement is used to handle different cases based on the classifier type.
    - If the classifier is `POSITIONAL_MARK`, it pops the last argument and sets `positional_only` to true, checking for remaining positionals.
    - If the classifier is `SUBCOMMAND_TERMINATOR`, it pops the last argument and sets `retval` to false.
    - If the classifier is `SUBCOMMAND`, it calls [`_parse_subcommand`](#bool_parse_subcommand) to handle subcommand parsing.
    - For `LONG`, `SHORT`, and `WINDOWS_STYLE` classifiers, it calls [`_parse_arg`](#bool_parse_arg) to process the argument as an option.
    - If the classifier is `NONE`, it attempts to parse the argument as a positional argument using [`_parse_positional`](#bool_parse_positional).
- **Output**: The function returns a boolean indicating whether the parsing was successful or not.
- **Functions called**:
    - [`CLI::CLI11_INLINE::Classifier::_recognize`](#Classifier_recognize)
    - [`CLI::CLI11_INLINE::_has_remaining_positionals`](#CLI11_INLINE_has_remaining_positionals)
    - [`CLI::void::_move_to_missing`](#void_move_to_missing)
    - [`CLI::bool::_parse_subcommand`](#bool_parse_subcommand)
    - [`CLI::bool::_parse_arg`](#bool_parse_arg)
    - [`CLI::bool::_parse_positional`](#bool_parse_positional)


---
### \_count\_remaining\_positionals<!-- {{#callable:CLI::CLI11_INLINE::size_t::_count_remaining_positionals}} -->
Counts the number of remaining positional arguments that are required or optional.
- **Inputs**:
    - `required_only`: A boolean flag indicating whether to count only required positional arguments.
- **Control Flow**:
    - Initializes a counter `retval` to zero.
    - Iterates over each option in the `options_` collection.
    - Checks if the option is positional and if it should be counted based on the `required_only` flag.
    - If the option is required and has a minimum expected item count, it calculates how many more items are needed and adds that to `retval`.
    - Returns the total count of remaining positional arguments.
- **Output**: Returns the total number of remaining positional arguments that are either required or optional, depending on the input flag.


---
### \_has\_remaining\_positionals<!-- {{#callable:CLI::CLI11_INLINE::_has_remaining_positionals}} -->
The `_has_remaining_positionals` function checks if there are any positional options that have not met their minimum expected count.
- **Inputs**: None
- **Control Flow**:
    - Iterates over each option in the `options_` vector.
    - For each option, checks if it is a positional option and if its count is less than the expected minimum.
    - If such an option is found, returns true immediately.
    - If no such options are found after checking all, returns false.
- **Output**: Returns a boolean value indicating whether there are remaining positional options that have not met their minimum expected count.


---
### \_parse\_positional<!-- {{#callable:CLI::bool::_parse_positional}} -->
The `_parse_positional` function processes positional arguments from a command line interface, determining their validity and associating them with the appropriate options.
- **Inputs**:
    - `args`: A reference to a vector of strings representing the command line arguments, where the last element is treated as the current positional argument.
    - `haltOnSubcommand`: A boolean flag indicating whether to stop processing if a subcommand is encountered.
- **Control Flow**:
    - The function retrieves the last argument from `args` as the current positional argument.
    - If `positionals_at_end_` is true, it checks for required positional options that must be filled before processing other options.
    - If no required positional options are found, it checks for optional positional options that can accept the current argument.
    - If a matching option is found, it processes the argument, adds it to the option's results, and may trigger a callback.
    - If no matching option is found, it checks for subcommands that can handle the argument.
    - If a subcommand is found, it processes the argument as a subcommand and returns.
    - If no valid option or subcommand is found, it handles the argument as missing or extra.
- **Output**: Returns a boolean indicating whether the parsing of the positional argument was successful.
- **Functions called**:
    - [`CLI::CLI11_INLINE::size_t::_count_remaining_positionals`](#size_t_count_remaining_positionals)
    - [`CLI::bool::_add_flag_like_result`](#bool_add_flag_like_result)
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)
    - [`CLI::void::_move_to_missing`](#void_move_to_missing)


---
### \_parse\_subcommand<!-- {{#callable:CLI::bool::_parse_subcommand}} -->
Parses a subcommand from the provided argument list and handles its execution.
- **Inputs**:
    - `args`: A reference to a vector of strings representing command-line arguments, where the last element is expected to be a subcommand.
- **Control Flow**:
    - Checks if there are remaining positional arguments that are required; if so, it parses them and returns true.
    - Attempts to find the subcommand corresponding to the last argument in `args`.
    - If the subcommand is not found, it checks for dot notation to potentially identify a subcommand.
    - If a valid subcommand is found, it removes the subcommand from `args`, executes its parsing, and triggers pre-parse callbacks for parent applications.
    - If no valid subcommand is found and the current application has no parent, it throws an error indicating the subcommand is missing.
- **Output**: Returns true if a subcommand was successfully parsed and executed; otherwise, it returns false or throws an error if the subcommand is missing.
- **Functions called**:
    - [`CLI::CLI11_INLINE::size_t::_count_remaining_positionals`](#size_t_count_remaining_positionals)
    - [`CLI::bool::_parse_positional`](#bool_parse_positional)
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)


---
### \_parse\_arg<!-- {{#callable:CLI::bool::_parse_arg}} -->
Parses command-line arguments based on their type and updates the application state accordingly.
- **Inputs**:
    - `args`: A reference to a vector of strings representing the command-line arguments.
    - `current_type`: An enumeration value indicating the type of argument being parsed (LONG, SHORT, WINDOWS_STYLE, etc.).
    - `local_processing_only`: A boolean flag indicating whether to restrict processing to local options only.
- **Control Flow**:
    - The function retrieves the last argument from the 'args' vector to process it.
    - Based on the 'current_type', it attempts to split the argument into its name and value using appropriate helper functions.
    - If the argument is not found in the options, it checks for subcommands and attempts to parse them.
    - If the argument is a non-standard option, it tries to handle it accordingly.
    - The function collects results based on the parsed argument and updates the application state, including handling required and optional arguments.
- **Output**: Returns true if the argument was successfully parsed and processed; otherwise, it may throw exceptions for errors encountered during parsing.
- **Functions called**:
    - [`CLI::App::_find_subcommand`](#App_find_subcommand)
    - [`CLI::void::increment_parsed`](#voidincrement_parsed)
    - [`CLI::void::_trigger_pre_parse`](#void_trigger_pre_parse)
    - [`CLI::App::_get_fallthrough_parent`](#App_get_fallthrough_parent)
    - [`CLI::void::_move_to_missing`](#void_move_to_missing)
    - [`CLI::CLI11_INLINE::size_t::_count_remaining_positionals`](#size_t_count_remaining_positionals)
    - [`CLI::CLI11_INLINE::Classifier::_recognize`](#Classifier_recognize)


---
### \_trigger\_pre\_parse<!-- {{#callable:CLI::void::_trigger_pre_parse}} -->
The `_trigger_pre_parse` function manages the pre-parsing state and invokes a callback if certain conditions are met.
- **Inputs**:
    - `remaining_args`: A `std::size_t` representing the number of arguments remaining to be parsed.
- **Control Flow**:
    - Checks if `pre_parse_called_` is false; if so, sets it to true and calls `pre_parse_callback_` with `remaining_args`.
    - If `pre_parse_called_` is true and `immediate_callback_` is true, it checks if `name_` is not empty.
    - If `name_` is not empty, it saves the current `parsed_` count, moves `missing_` to `extras`, clears the state, and resets `parsed_` and `missing_`.
- **Output**: The function does not return a value; it modifies the internal state of the `App` class and may invoke a callback function.
- **Functions called**:
    - [`CLI::void::clear`](#voidclear)


---
### \_move\_to\_missing<!-- {{#callable:CLI::void::_move_to_missing}} -->
Moves a value to a missing list based on the current state of the application.
- **Inputs**:
    - `val_type`: A `detail::Classifier` enum value indicating the type of the value being moved.
    - `val`: A `std::string` representing the value that is to be moved to the missing list.
- **Control Flow**:
    - Checks if extras are allowed or if there are no subcommands.
    - If either condition is true, the value is added to the `missing_` list.
    - Iterates through subcommands to find a suitable place for the value if extras are not allowed.
    - If no suitable place is found, the value is added to the `missing_` list.
- **Output**: The function does not return a value; it modifies the internal state of the application by adding the value to the `missing_` list.


---
### \_move\_option<!-- {{#callable:CLI::void::_move_option}} -->
Moves an `Option` from the current `App` to a specified subcommand `App`.
- **Inputs**:
    - `opt`: A pointer to the `Option` object that is to be moved.
    - `app`: A pointer to the `App` object that represents the subcommand to which the option will be moved.
- **Control Flow**:
    - Checks if the `opt` pointer is null and throws an `OptionNotFound` exception if it is.
    - Iterates through the `subcommands_` of the current `App` to verify if the provided `app` is a valid subcommand.
    - Throws an `OptionNotFound` exception if the `app` is not found in the subcommands.
    - Checks if the `opt` is a help option or a config option and throws an `OptionAlreadyAdded` exception if it is.
    - Searches for the `opt` in the current `App`'s options and throws an `OptionNotFound` exception if it is not found.
    - Checks if the `opt` already exists in the target `app`'s options and throws an `OptionAlreadyAdded` exception if it does.
    - Moves the `opt` to the target `app`'s options and erases it from the current `App`'s options.
- **Output**: This function does not return a value; it modifies the state of the `App` by moving the specified `Option`.


---
### TriggerOn<!-- {{#callable:CLI::TriggerOn}} -->
The `TriggerOn` function enables a list of applications by setting their default states and registering a callback to enable them when a specified trigger application is parsed.
- **Inputs**:
    - `trigger_app`: A pointer to the `App` instance that will trigger the enabling of other applications.
    - `apps_to_enable`: A vector of pointers to `App` instances that are to be enabled.
- **Control Flow**:
    - Iterates over each application in `apps_to_enable` to set their default enabled state to false and mark them as disabled.
    - Registers a callback on `trigger_app` that, when invoked, will enable each application in `apps_to_enable`.
- **Output**: The function does not return a value; it modifies the state of the applications and sets up a callback for enabling them.


---
### TriggerOff<!-- {{#callable:CLI::TriggerOff}} -->
The `TriggerOff` function disables specified applications and sets a callback to handle their state.
- **Inputs**:
    - `trigger_app`: A pointer to the `App` instance that will trigger the disabling of other applications.
    - `apps_to_enable`: A vector of pointers to `App` instances that are to be disabled.
- **Control Flow**:
    - The function iterates over each application in the `apps_to_enable` vector.
    - For each application, it calls `disabled_by_default(false)` to enable it by default and `enabled_by_default()` to set it as enabled.
    - It sets a callback on `trigger_app` using `preparse_callback`, which will disable each application in `apps_to_enable` when triggered.
- **Output**: The function does not return a value; it modifies the state of the applications and sets a callback.


---
### deprecate\_option<!-- {{#callable:CLI::deprecate_option}} -->
The `deprecate_option` function marks an `Option` as deprecated and suggests a replacement.
- **Inputs**:
    - `opt`: A pointer to the `Option` object that is to be marked as deprecated.
    - `replacement`: A string representing the name of the option that should be used instead of the deprecated option.
- **Control Flow**:
    - A `Validator` object named `deprecate_warning` is created, which outputs a deprecation warning message when triggered.
    - The `application_index` method of `deprecate_warning` is called with an argument of 0.
    - The `check` method of the `opt` is called with `deprecate_warning` to validate the option.
    - If the `replacement` string is not empty, the description of the `opt` is updated to include a deprecation notice.
- **Output**: The function does not return a value; it modifies the state of the `Option` and outputs a warning message to the console.


---
### retire\_option<!-- {{#callable:CLI::retire_option}} -->
The [`retire_option`](#CLIretire_option) function marks an option as retired in the given application.
- **Inputs**:
    - `app`: A reference to an `App` object representing the application in which the option is being retired.
    - `option_name`: A string representing the name of the option to be retired.
- **Control Flow**:
    - The function first retrieves the option associated with the provided `option_name` from the `app` using `get_option_no_throw`.
    - If the option exists, it calls the overloaded [`retire_option`](#CLIretire_option) function to handle the retirement process.
    - If the option does not exist, it creates a new option with the same name, indicating that it has been retired and has no effect.
- **Output**: The function does not return a value; it modifies the state of the application by retiring the specified option.
- **Functions called**:
    - [`CLI::retire_option`](#CLIretire_option)


---
### simple<!-- {{#callable:CLI::FailureMessage::std::string::simple}} -->
Generates a formatted error message suggesting help commands based on the provided error.
- **Inputs**:
    - `app`: A pointer to an `App` object that contains the application context.
    - `e`: An `Error` object that contains information about the error that occurred.
- **Control Flow**:
    - Initializes a string `header` with the error message obtained from `e.what()`.
    - Checks if the `app` has a help pointer and adds its name to the `names` vector if it exists.
    - Checks if the `app` has a help-all pointer and adds its name to the `names` vector if it exists.
    - If the `names` vector is not empty, appends a suggestion to the `header` indicating how to get more information.
- **Output**: Returns a string containing the formatted error message along with suggestions for help commands.


