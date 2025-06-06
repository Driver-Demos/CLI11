# Purpose
The provided C++ code is a header file for a command-line interface (CLI) library, specifically part of the CLI11 library. This library is designed to facilitate the creation and management of command-line applications by providing a structured way to define commands, options, flags, and subcommands. The primary class in this file is `CLI::App`, which represents a command-line application or a subcommand within an application. It includes methods for adding options and flags, setting callbacks, handling subcommands, and managing parsing logic. The file also defines several helper functions and classes, such as [`Option_group`](#Option_groupOption_group) for grouping options and `AppFriend` for testing purposes.

The `CLI::App` class is central to the library's functionality, allowing users to define the behavior of their command-line applications. It supports features like option parsing, subcommand management, and error handling. The class provides a variety of methods to customize the application's behavior, such as setting help messages, version information, and configuration file handling. The file also includes several utility functions and enumerations to support the parsing and execution of command-line arguments. Overall, this header file is a comprehensive component of the CLI11 library, providing essential tools for building robust command-line interfaces in C++.
# Imports and Dependencies

---
- `algorithm`
- `cstdint`
- `functional`
- `iostream`
- `iterator`
- `memory`
- `numeric`
- `set`
- `sstream`
- `string`
- `utility`
- `vector`
- `ConfigFwd.hpp`
- `Error.hpp`
- `FormatterFwd.hpp`
- `Macros.hpp`
- `Option.hpp`
- `Split.hpp`
- `StringTools.hpp`
- `TypeTools.hpp`
- `impl/App_inl.hpp`


# Data Structures

---
### Classifier<!-- {{#data_structure:CLI::detail::Classifier}} -->
- **Type**: `enum class`
- **Members**:
    - `NONE`: Represents no classification.
    - `POSITIONAL_MARK`: Indicates a positional mark in command line parsing.
    - `SHORT`: Represents a short option in command line parsing.
    - `LONG`: Represents a long option in command line parsing.
    - `WINDOWS_STYLE`: Represents a Windows-style option in command line parsing.
    - `SUBCOMMAND`: Indicates a subcommand in command line parsing.
    - `SUBCOMMAND_TERMINATOR`: Marks the end of a subcommand in command line parsing.
- **Description**: The `Classifier` enum class is used to categorize different types of command line arguments or options in a command line interface (CLI) parsing context. It provides a set of constants that represent various classifications such as positional marks, short and long options, Windows-style options, subcommands, and subcommand terminators. This classification helps in parsing and processing command line inputs effectively.


---
### config\_extras\_mode<!-- {{#data_structure:CLI::config_extras_mode}} -->
- **Type**: `enum class`
- **Members**:
    - `error`: Represents the mode where extras in config files result in an error.
    - `ignore`: Represents the mode where extras in config files are ignored.
    - `ignore_all`: Represents the mode where all extras in config files are ignored.
    - `capture`: Represents the mode where extras in config files are captured for further processing.
- **Description**: The `config_extras_mode` is an enumeration that defines different modes for handling extra entries in configuration files. It provides four modes: `error`, `ignore`, `ignore_all`, and `capture`, each represented by an integer value starting from 0. This enum is used to specify how the application should behave when encountering unexpected or additional configuration parameters, allowing for flexible handling of configuration file parsing.
- **Member Functions**:
    - [`CLI::config_extras_mode::get_allow_config_extras`](#config_extras_modeget_allow_config_extras)

**Methods**

---
#### config\_extras\_mode::get\_allow\_config\_extras<!-- {{#callable:CLI::config_extras_mode::get_allow_config_extras}} -->
The `get_allow_config_extras` function returns the current mode for handling extra configuration options in config files.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `allow_config_extras_` member variable, which is of type `config_extras_mode`.
- **Output**: The function returns a value of type `config_extras_mode`, which indicates how extra configuration options are handled.
- **See also**: [`CLI::config_extras_mode`](#CLIconfig_extras_mode)  (Data Structure)



---
### App<!-- {{#data_structure:CLI::App}} -->
- **Type**: `class`
- **Members**:
    - `name_`: Stores the subcommand or program name.
    - `description_`: Holds the description of the current program or subcommand.
    - `allow_extras_`: Indicates if extra arguments are allowed without error.
    - `allow_config_extras_`: Specifies how to handle extra arguments in config files.
    - `prefix_command_`: Determines if processing should stop on an unrecognized option.
    - `has_automatic_name_`: Indicates if the name was automatically generated.
    - `required_`: Specifies if the subcommand is required.
    - `disabled_`: Indicates if the subcommand is disabled.
    - `pre_parse_called_`: Flag indicating if the pre-parse callback has been triggered.
    - `immediate_callback_`: Indicates if the callback should be executed immediately after parsing.
    - `pre_parse_callback_`: Function to run before parsing starts.
    - `parse_complete_callback_`: Function to run when parsing is complete.
    - `final_callback_`: Function to run when all processing is complete.
    - `option_defaults_`: Holds default values for options.
    - `options_`: Stores the list of options for the app.
    - `usage_`: Usage information for help output.
    - `usage_callback_`: Function to generate usage information for help output.
    - `footer_`: Footer information for help output.
    - `footer_callback_`: Function to generate footer information for help output.
    - `help_ptr_`: Pointer to the help flag option.
    - `help_all_ptr_`: Pointer to the help all flag option.
    - `version_ptr_`: Pointer to the version flag option.
    - `formatter_`: Formatter for help printing.
    - `failure_message_`: Function to print error messages.
    - `missing_`: Stores missing options as pairs of classifier and string.
    - `parse_order_`: List of options in the original parse order.
    - `parsed_subcommands_`: List of subcommands collected in order.
    - `exclude_subcommands_`: Set of subcommands that are exclusionary to this one.
    - `exclude_options_`: Set of options that are exclusionary to this app.
    - `need_subcommands_`: Set of subcommands required by this one.
    - `need_options_`: Set of options required by this app.
    - `subcommands_`: Storage for the list of subcommands.
    - `ignore_case_`: Indicates if the program name is case-insensitive.
    - `ignore_underscore_`: Indicates if underscores should be ignored.
    - `fallthrough_`: Allows options to fall through to parent commands.
    - `subcommand_fallthrough_`: Allows subcommands to fall through to parent commands.
    - `allow_windows_style_options_`: Allows Windows-style options.
    - `positionals_at_end_`: Specifies that positional arguments come at the end.
    - `default_startup`: Specifies the startup mode for the app.
    - `configurable_`: Indicates if the subcommand can be triggered via config files.
    - `validate_positionals_`: Indicates if positional options are validated before assigning.
    - `validate_optional_arguments_`: Indicates if optional vector arguments are validated before assigning.
    - `silent_`: Indicates if the subcommand is silent and won't show up in the list.
    - `allow_non_standard_options_`: Indicates if non-standard option arguments are allowed.
    - `allow_prefix_matching_`: Indicates if subcommands can match with prefix matching.
    - `parsed_`: Counts the number of times this command/subcommand was parsed.
    - `require_subcommand_min_`: Minimum required subcommands.
    - `require_subcommand_max_`: Maximum number of subcommands allowed.
    - `require_option_min_`: Minimum required options.
    - `require_option_max_`: Maximum number of options allowed.
    - `parent_`: Pointer to the parent if this is a subcommand.
    - `group_`: Group membership for the subcommand.
    - `aliases_`: Alias names for the subcommand.
    - `config_ptr_`: Pointer to the config option.
    - `config_formatter_`: Formatter for config printing.
    - `normalized_argv_`: Storage for normalized arguments on Windows.
    - `normalized_argv_view_`: View of normalized arguments on Windows.
- **Description**: The `App` class is a comprehensive data structure designed to manage command-line applications, supporting subcommands, options, and configuration files. It provides extensive functionality for parsing command-line arguments, handling errors, and generating help messages. The class supports features like case-insensitive names, prefix matching, and Windows-style options, making it versatile for various command-line interface requirements. It also includes mechanisms for managing subcommands, options, and their dependencies, ensuring robust command-line application development.
- **Member Functions**:
    - [`CLI::App::App`](#AppApp)
    - [`CLI::App::App`](#AppApp)
    - [`CLI::App::operator=`](#Appoperator=)
    - [`CLI::App::~App`](#AppApp)
    - [`CLI::App::callback`](#Appcallback)
    - [`CLI::App::final_callback`](#Appfinal_callback)
    - [`CLI::App::parse_complete_callback`](#Appparse_complete_callback)
    - [`CLI::App::preparse_callback`](#Apppreparse_callback)
    - [`CLI::App::allow_extras`](#Appallow_extras)
    - [`CLI::App::required`](#Apprequired)
    - [`CLI::App::disabled`](#Appdisabled)
    - [`CLI::App::silent`](#Appsilent)
    - [`CLI::App::allow_non_standard_option_names`](#Appallow_non_standard_option_names)
    - [`CLI::App::allow_subcommand_prefix_matching`](#Appallow_subcommand_prefix_matching)
    - [`CLI::App::disabled_by_default`](#Appdisabled_by_default)
    - [`CLI::App::enabled_by_default`](#Appenabled_by_default)
    - [`CLI::App::validate_positionals`](#Appvalidate_positionals)
    - [`CLI::App::validate_optional_arguments`](#Appvalidate_optional_arguments)
    - [`CLI::App::allow_config_extras`](#Appallow_config_extras)
    - [`CLI::App::allow_config_extras`](#Appallow_config_extras)
    - [`CLI::App::prefix_command`](#Appprefix_command)
    - [`CLI::App::allow_windows_style_options`](#Appallow_windows_style_options)
    - [`CLI::App::positionals_at_end`](#Apppositionals_at_end)
    - [`CLI::App::configurable`](#Appconfigurable)
    - [`CLI::App::formatter`](#Appformatter)
    - [`CLI::App::formatter_fn`](#Appformatter_fn)
    - [`CLI::App::config_formatter`](#Appconfig_formatter)
    - [`CLI::App::parsed`](#Appparsed)
    - [`CLI::App::option_defaults`](#Appoption_defaults)
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::App::add_option_no_stream`](#Appadd_option_no_stream)
    - [`CLI::App::add_option_function`](#Appadd_option_function)
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::App::add_flag`](#Appadd_flag)
    - [`CLI::App::add_flag`](#Appadd_flag)
    - [`CLI::App::add_flag`](#Appadd_flag)
    - [`CLI::App::add_flag`](#Appadd_flag)
    - [`CLI::App::add_flag`](#Appadd_flag)
    - [`CLI::App::add_option_group`](#Appadd_option_group)
    - [`CLI::App::group`](#Appgroup)
    - [`CLI::App::require_subcommand`](#Apprequire_subcommand)
    - [`CLI::App::require_subcommand`](#Apprequire_subcommand)
    - [`CLI::App::require_subcommand`](#Apprequire_subcommand)
    - [`CLI::App::require_option`](#Apprequire_option)
    - [`CLI::App::require_option`](#Apprequire_option)
    - [`CLI::App::require_option`](#Apprequire_option)
    - [`CLI::App::fallthrough`](#Appfallthrough)
    - [`CLI::App::subcommand_fallthrough`](#Appsubcommand_fallthrough)
    - [`CLI::App::pre_callback`](#Apppre_callback)
    - [`CLI::App::failure_message`](#Appfailure_message)
    - [`CLI::App::ensure_utf8`](impl/App_inl.hpp.driver.md#Appensure_utf8)
    - [`CLI::App::name`](impl/App_inl.hpp.driver.md#Appname)
    - [`CLI::App::alias`](impl/App_inl.hpp.driver.md#Appalias)
    - [`CLI::App::immediate_callback`](impl/App_inl.hpp.driver.md#Appimmediate_callback)
    - [`CLI::App::ignore_case`](impl/App_inl.hpp.driver.md#Appignore_case)
    - [`CLI::App::ignore_underscore`](impl/App_inl.hpp.driver.md#Appignore_underscore)
    - [`CLI::App::add_option`](impl/App_inl.hpp.driver.md#Appadd_option)
    - [`CLI::App::set_help_flag`](impl/App_inl.hpp.driver.md#Appset_help_flag)
    - [`CLI::App::set_help_all_flag`](impl/App_inl.hpp.driver.md#Appset_help_all_flag)
    - [`CLI::App::set_version_flag`](impl/App_inl.hpp.driver.md#Appset_version_flag)
    - [`CLI::App::set_version_flag`](impl/App_inl.hpp.driver.md#Appset_version_flag)
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
    - [`CLI::App::add_flag_callback`](impl/App_inl.hpp.driver.md#Appadd_flag_callback)
    - [`CLI::App::add_flag_function`](impl/App_inl.hpp.driver.md#Appadd_flag_function)
    - [`CLI::App::set_config`](impl/App_inl.hpp.driver.md#Appset_config)
    - [`CLI::App::add_subcommand`](impl/App_inl.hpp.driver.md#Appadd_subcommand)
    - [`CLI::App::add_subcommand`](impl/App_inl.hpp.driver.md#Appadd_subcommand)
    - [`CLI::App::get_subcommand`](impl/App_inl.hpp.driver.md#Appget_subcommand)
    - [`CLI::App::get_subcommand`](impl/App_inl.hpp.driver.md#Appget_subcommand)
    - [`CLI::App::get_subcommand_no_throw`](impl/App_inl.hpp.driver.md#Appget_subcommand_no_throw)
    - [`CLI::App::get_subcommand`](impl/App_inl.hpp.driver.md#Appget_subcommand)
    - [`CLI::App::get_option_group`](impl/App_inl.hpp.driver.md#Appget_option_group)
    - [`CLI::App::exit`](impl/App_inl.hpp.driver.md#Appexit)
    - [`CLI::App::get_option_no_throw`](impl/App_inl.hpp.driver.md#Appget_option_no_throw)
    - [`CLI::App::get_option_no_throw`](impl/App_inl.hpp.driver.md#Appget_option_no_throw)
    - [`CLI::App::_find_subcommand`](impl/App_inl.hpp.driver.md#App_find_subcommand)
    - [`CLI::App::_get_fallthrough_parent`](impl/App_inl.hpp.driver.md#App_get_fallthrough_parent)
    - [`CLI::App::_compare_subcommand_names`](impl/App_inl.hpp.driver.md#App_compare_subcommand_names)

**Methods**

---
#### App::App<!-- {{#callable:CLI::App::App}} -->
Constructs an `App` instance with optional description and name, and sets a help flag.
- **Inputs**:
    - `app_description`: A string that describes the application, defaulting to an empty string.
    - `app_name`: A string that represents the name of the application, defaulting to an empty string.
- **Control Flow**:
    - The constructor initializes the `App` by calling another constructor with the provided description and name, passing a nullptr for the parent.
    - It then calls the [`set_help_flag`](impl/App_inl.hpp.driver.md#Appset_help_flag) method to define a help flag for the application.
- **Output**: This function does not return a value; it initializes an instance of the `App` class.
- **Functions called**:
    - [`CLI::App::set_help_flag`](impl/App_inl.hpp.driver.md#Appset_help_flag)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::App<!-- {{#callable:CLI::App::App}} -->
The `App` constructor initializes a command line application with a description and name.
- **Inputs**:
    - `app_description`: A string that describes the application or subcommand.
    - `app_name`: A string that represents the name of the application; if empty, the parser will set it.
- **Control Flow**:
    - The constructor initializes member variables with default values.
    - It calls a private constructor to set up the application with the provided description and name.
    - The help flag is set to provide usage information.
- **Output**: The constructor does not return a value but initializes an instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::\~App<!-- {{#callable:CLI::App::~App}} -->
The `~App` function is a virtual destructor for the `App` class, ensuring proper cleanup of resources when an instance of `App` or its derived classes is destroyed.
- **Inputs**: None
- **Control Flow**:
    - The destructor is declared as virtual, allowing derived classes to override it and ensuring that the correct destructor is called for derived class instances.
    - The destructor has a default implementation, which means it does not perform any specific actions beyond what is automatically handled by the compiler.
- **Output**: The function does not return any value, as it is a destructor; its purpose is to clean up resources associated with the `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::callback<!-- {{#callable:CLI::App::callback}} -->
Sets a callback function to be executed upon completion of parsing, either immediately or as a final callback.
- **Inputs**:
    - `app_callback`: A `std::function<void()>` that represents the callback function to be executed after parsing is complete.
- **Control Flow**:
    - Checks the `immediate_callback_` flag to determine if the callback should be set as `parse_complete_callback_` or `final_callback_`.
    - If `immediate_callback_` is true, the provided callback is assigned to `parse_complete_callback_` using `std::move`.
    - If `immediate_callback_` is false, the provided callback is assigned to `final_callback_` using `std::move`.
    - Returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::final\_callback<!-- {{#callable:CLI::App::final_callback}} -->
Sets a final callback function to be executed when all processing in the `App` class has completed.
- **Inputs**:
    - `app_callback`: A `std::function<void()>` that represents the callback function to be executed after all processing is complete.
- **Control Flow**:
    - The function takes a `std::function<void()>` as an argument and moves it into the member variable `final_callback_`.
    - It returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::parse\_complete\_callback<!-- {{#callable:CLI::App::parse_complete_callback}} -->
Sets a callback function to be executed when parsing is complete.
- **Inputs**:
    - `pc_callback`: A `std::function<void()>` that represents the callback to be executed upon completion of parsing.
- **Control Flow**:
    - The function takes a `std::function<void()>` as an argument and moves it into the member variable `parse_complete_callback_`.
    - It returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::preparse\_callback<!-- {{#callable:CLI::App::preparse_callback}} -->
Sets a pre-parse callback function for the `App` instance.
- **Inputs**:
    - `pp_callback`: A `std::function` that takes a `std::size_t` argument, which will be called before parsing begins.
- **Control Flow**:
    - The input callback function `pp_callback` is moved into the member variable `pre_parse_callback_`.
    - The function returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_extras<!-- {{#callable:CLI::App::allow_extras}} -->
Sets the `allow_extras_` flag to indicate whether extra command line arguments should be permitted.
- **Inputs**:
    - `allow`: A boolean value that determines if extra arguments are allowed; defaults to true.
- **Control Flow**:
    - The function sets the member variable `allow_extras_` to the value of the `allow` parameter.
    - It returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::required<!-- {{#callable:CLI::App::required}} -->
Sets the `required_` flag for the `App` instance to indicate whether the subcommand is required.
- **Inputs**:
    - `require`: A boolean value that determines if the subcommand is required; defaults to true.
- **Control Flow**:
    - The function assigns the input boolean value to the member variable `required_`.
    - It then returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::disabled<!-- {{#callable:CLI::App::disabled}} -->
Sets the `disabled_` flag of the `App` instance to indicate whether the subcommand is disabled.
- **Inputs**:
    - `disable`: A boolean value that determines whether to disable the subcommand; defaults to true.
- **Control Flow**:
    - The function sets the member variable `disabled_` to the value of the `disable` parameter.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::silent<!-- {{#callable:CLI::App::silent}} -->
Sets the `silent_` flag of the `App` class to control whether the subcommand is displayed in the processed list.
- **Inputs**:
    - `silence`: A boolean flag indicating whether to silence the subcommand; defaults to true.
- **Control Flow**:
    - The function assigns the value of the `silence` parameter to the member variable `silent_`.
    - The function returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_non\_standard\_option\_names<!-- {{#callable:CLI::App::allow_non_standard_option_names}} -->
Sets the flag to allow or disallow non-standard option names in the application.
- **Inputs**:
    - `allowed`: A boolean value indicating whether non-standard option names are allowed; defaults to true.
- **Control Flow**:
    - The function sets the member variable `allow_non_standard_options_` to the value of the `allowed` parameter.
    - The function returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_subcommand\_prefix\_matching<!-- {{#callable:CLI::App::allow_subcommand_prefix_matching}} -->
Sets the flag for allowing prefix matching of subcommands.
- **Inputs**:
    - `allowed`: A boolean value indicating whether prefix matching for subcommands should be allowed; defaults to true.
- **Control Flow**:
    - The function sets the member variable `allow_prefix_matching_` to the value of the `allowed` parameter.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::disabled\_by\_default<!-- {{#callable:CLI::App::disabled_by_default}} -->
Sets the default startup mode for the application to either disabled or stable based on the input parameter.
- **Inputs**:
    - `disable`: A boolean flag indicating whether to disable the application by default; defaults to true.
- **Control Flow**:
    - If the 'disable' parameter is true, the 'default_startup' is set to 'disabled'.
    - If 'disable' is false, 'default_startup' is set to 'enabled' if it was previously 'enabled', otherwise it is set to 'stable'.
- **Output**: Returns a pointer to the current instance of the App class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::enabled\_by\_default<!-- {{#callable:CLI::App::enabled_by_default}} -->
Sets the default startup mode for the application based on the input parameter.
- **Inputs**:
    - `enable`: A boolean flag indicating whether to enable the application by default; defaults to true.
- **Control Flow**:
    - If 'enable' is true, set 'default_startup' to 'startup_mode::enabled'.
    - If 'enable' is false, check if 'default_startup' is 'startup_mode::disabled'; if so, keep it as 'disabled', otherwise set it to 'stable'.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::validate\_positionals<!-- {{#callable:CLI::App::validate_positionals}} -->
Sets the flag for validating positional arguments in the `App` class.
- **Inputs**:
    - `validate`: A boolean flag indicating whether to enable or disable validation of positional arguments, defaulting to true.
- **Control Flow**:
    - The function sets the member variable `validate_positionals_` to the value of the `validate` parameter.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::validate\_optional\_arguments<!-- {{#callable:CLI::App::validate_optional_arguments}} -->
Sets the flag for validating optional arguments in the `App` class.
- **Inputs**:
    - `validate`: A boolean flag indicating whether to enable or disable validation of optional arguments, defaulting to true.
- **Control Flow**:
    - The function takes a boolean parameter `validate` which defaults to true.
    - It assigns the value of `validate` to the member variable `validate_optional_arguments_`.
    - Finally, it returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_config\_extras<!-- {{#callable:CLI::App::allow_config_extras}} -->
Sets the configuration mode for handling extra arguments in the application.
- **Inputs**:
    - `allow`: A boolean flag indicating whether to allow extra configuration arguments; defaults to true.
- **Control Flow**:
    - If the `allow` parameter is true, set `allow_config_extras_` to `config_extras_mode::capture` and `allow_extras_` to true.
    - If the `allow` parameter is false, set `allow_config_extras_` to `config_extras_mode::error`.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_config\_extras<!-- {{#callable:CLI::App::allow_config_extras}} -->
Sets the configuration mode for handling extra arguments in configuration files.
- **Inputs**:
    - `mode`: An enumeration value of type `config_extras_mode` that specifies how to handle extra arguments in configuration files.
- **Control Flow**:
    - The function assigns the provided `mode` to the member variable `allow_config_extras_`.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::prefix\_command<!-- {{#callable:CLI::App::prefix_command}} -->
Sets the `prefix_command_` flag to determine if the application should stop processing on an unrecognized option.
- **Inputs**:
    - `is_prefix`: A boolean flag indicating whether to treat the command as a prefix command, defaulting to true.
- **Control Flow**:
    - The function sets the member variable `prefix_command_` to the value of `is_prefix`.
    - The function returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::allow\_windows\_style\_options<!-- {{#callable:CLI::App::allow_windows_style_options}} -->
Sets the `allow_windows_style_options_` flag to enable or disable Windows-style options.
- **Inputs**:
    - `value`: A boolean value indicating whether to allow Windows-style options (default is true).
- **Control Flow**:
    - The function sets the member variable `allow_windows_style_options_` to the provided boolean value.
    - It returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::positionals\_at\_end<!-- {{#callable:CLI::App::positionals_at_end}} -->
Sets the `positionals_at_end_` flag to indicate whether positional arguments should be placed at the end of the argument sequence.
- **Inputs**:
    - `value`: A boolean flag that determines if positional arguments should be placed at the end of the argument sequence, defaulting to true.
- **Control Flow**:
    - The function assigns the input boolean `value` to the member variable `positionals_at_end_`.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::configurable<!-- {{#callable:CLI::App::configurable}} -->
Sets the `configurable_` flag of the `App` class to indicate if the subcommand can be triggered via configuration files.
- **Inputs**:
    - `value`: A boolean value that determines whether the subcommand is configurable; defaults to true.
- **Control Flow**:
    - The function assigns the input boolean value to the member variable `configurable_`.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::formatter<!-- {{#callable:CLI::App::formatter}} -->
Sets the formatter for help printing in the `App` class.
- **Inputs**:
    - `fmt`: A shared pointer to a `FormatterBase` object that defines how help messages are formatted.
- **Control Flow**:
    - The function assigns the provided `fmt` to the member variable `formatter_` of the `App` class.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::formatter\_fn<!-- {{#callable:CLI::App::formatter_fn}} -->
The `formatter_fn` method sets a custom formatter for the `App` instance.
- **Inputs**:
    - `fmt`: A `std::function` that takes a pointer to an `App`, a `std::string`, and an `AppFormatMode`, and returns a `std::string` for formatting.
- **Control Flow**:
    - The method assigns a new `FormatterLambda` instance, initialized with the provided `fmt` function, to the `formatter_` member variable.
    - It then returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::config\_formatter<!-- {{#callable:CLI::App::config_formatter}} -->
The `config_formatter` method sets the configuration formatter for the `App` instance.
- **Inputs**:
    - `fmt`: A shared pointer to a `Config` object that will be used as the configuration formatter.
- **Control Flow**:
    - The method assigns the provided `fmt` argument to the member variable `config_formatter_`.
    - It then returns a pointer to the current instance of `App`.
- **Output**: Returns a pointer to the current `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::parsed<!-- {{#callable:CLI::App::parsed}} -->
Checks if the subcommand has been parsed from the command line.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function evaluates the member variable `parsed_` which counts the number of times the command/subcommand was parsed.
    - It returns true if `parsed_` is greater than 0, indicating that the subcommand was indeed parsed.
- **Output**: Returns a boolean value: true if the subcommand was parsed, false otherwise.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::option\_defaults<!-- {{#callable:CLI::App::option_defaults}} -->
The `option_defaults` function returns a pointer to the `OptionDefaults` object associated with the `App` instance.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the `option_defaults_` member of the `App` class.
    - It returns the address of the `option_defaults_` member, which is of type `OptionDefaults`.
- **Output**: The output is a pointer to an `OptionDefaults` object, allowing access to the default values for options within the `App` instance.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option<!-- {{#callable:CLI::App::add_option}} -->
The [`add_option`](#Appadd_option) function adds a command-line option that assigns a value to a specified variable.
- **Inputs**:
    - `option_name`: A string representing the name of the option to be added.
    - `variable`: A reference to the variable that will store the value of the option.
    - `option_description`: An optional string providing a description of the option.
- **Control Flow**:
    - A lambda function is created to handle the conversion of command-line results to the specified variable type.
    - The [`add_option`](#Appadd_option) function is called with the option name, the conversion function, and the description.
    - The type name and size of the option are set based on the variable's type.
    - The expected count of the option is determined and set.
    - A callback for the default value is executed.
- **Output**: Returns a pointer to the `Option` object that was created and added.
- **Functions called**:
    - [`CLI::App::add_option`](#Appadd_option)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option\_no\_stream<!-- {{#callable:CLI::App::add_option_no_stream}} -->
Adds an option to a command line application without using a stream.
- **Inputs**:
    - `option_name`: The name of the option to be added.
    - `variable`: A reference to the variable that will be set when the option is used.
    - `option_description`: An optional description of the option.
- **Control Flow**:
    - A lambda function is created that captures the variable and converts the command line results into the variable's type.
    - The [`add_option`](impl/App_inl.hpp.driver.md#Appadd_option) function is called to register the option with the application, passing the name, conversion function, description, and other parameters.
    - The type name and size of the variable are set on the option, along with the expected count of values.
    - A callback for the default value is executed.
- **Output**: Returns a pointer to the created `Option` object.
- **Functions called**:
    - [`CLI::App::add_option`](impl/App_inl.hpp.driver.md#Appadd_option)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option\_function<!-- {{#callable:CLI::App::add_option_function}} -->
Adds an option to a command-line interface that executes a callback function with a specified argument type.
- **Inputs**:
    - `option_name`: The name of the option to be added.
    - `func`: A callback function that takes a constant reference of type ArgType.
    - `option_description`: An optional description of the option.
- **Control Flow**:
    - Creates a lambda function that captures the provided callback and processes the results from the command line.
    - Attempts to convert the command line results into the specified ArgType using lexical conversion.
    - If the conversion is successful, the callback function is executed with the converted value.
    - Calls the [`add_option`](impl/App_inl.hpp.driver.md#Appadd_option) method to register the option with the command-line interface.
    - Sets the type name, size, and expected count for the option based on ArgType.
- **Output**: Returns a pointer to the created `Option` object that represents the added option.
- **Functions called**:
    - [`CLI::App::add_option`](impl/App_inl.hpp.driver.md#Appadd_option)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option<!-- {{#callable:CLI::App::add_option}} -->
Adds an option to the command line application with a specified name.
- **Inputs**:
    - `option_name`: A string representing the name of the option to be added.
- **Control Flow**:
    - The function calls another overloaded version of [`add_option`](impl/App_inl.hpp.driver.md#Appadd_option) with default parameters for callback, description, and defaulted flag.
    - It does not perform any additional logic or checks before invoking the overloaded function.
- **Output**: Returns a pointer to the `Option` object that was created for the specified option name.
- **Functions called**:
    - [`CLI::App::add_option`](impl/App_inl.hpp.driver.md#Appadd_option)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option<!-- {{#callable:CLI::App::add_option}} -->
The [`add_option`](impl/App_inl.hpp.driver.md#Appadd_option) function adds an option to a command-line application with a specified name and description.
- **Inputs**:
    - `option_name`: A string representing the name of the option to be added.
    - `option_description`: A reference to a constant type T that describes the option.
- **Control Flow**:
    - The function checks if the type T is a constant type and can be converted to a string.
    - If the conditions are met, it calls another overloaded [`add_option`](impl/App_inl.hpp.driver.md#Appadd_option) function with the provided parameters.
- **Output**: Returns a pointer to the `Option` object that was added to the application.
- **Functions called**:
    - [`CLI::App::add_option`](impl/App_inl.hpp.driver.md#Appadd_option)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_flag<!-- {{#callable:CLI::App::add_flag}} -->
The `add_flag` function adds a flag option to the command line application.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
- **Control Flow**:
    - The function calls the internal method [`_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal) with the provided `flag_name`, an empty callback, and an empty string for the flag description.
    - The [`_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal) method is responsible for the actual addition of the flag to the application's options.
- **Output**: Returns a pointer to the `Option` object that represents the added flag.
- **Functions called**:
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_flag<!-- {{#callable:CLI::App::add_flag}} -->
The `add_flag` function adds a flag option to a command-line application with an associated description.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `flag_description`: A constant reference to a description string for the flag.
- **Control Flow**:
    - The function checks if the type of `flag_description` is a constant type that can be converted to a string.
    - If the type check passes, it calls the internal function [`_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal) with the flag name, an empty callback, and the flag description.
- **Output**: Returns a pointer to an `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_flag<!-- {{#callable:CLI::App::add_flag}} -->
Adds a flag to the command line interface that modifies a variable based on user input.
- **Inputs**:
    - `flag_name`: The name of the flag to be added to the command line interface.
    - `flag_result`: A reference to a variable that will hold the result of the flag.
    - `flag_description`: An optional description of the flag.
- **Control Flow**:
    - The function first defines a callback function that captures the reference to `flag_result`.
    - This callback is responsible for converting the command line input into the appropriate type and storing it in `flag_result`.
    - The function then calls [`_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal) to register the flag with the CLI framework, passing the flag name, callback, and description.
    - Finally, it applies default modifiers to the created option using `detail::default_flag_modifiers`.
- **Output**: Returns a pointer to the `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#detaillexical_cast)
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_flag<!-- {{#callable:CLI::App::add_flag}} -->
The `add_flag` function adds a command-line flag that can capture multiple results into a vector.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `flag_results`: A reference to a vector where the results of the flag will be stored.
    - `flag_description`: An optional string providing a description of the flag.
- **Control Flow**:
    - A lambda function is defined to handle the callback when the flag is encountered, which processes the results.
    - The lambda iterates over the results, converting each element to the appropriate type and storing it in the `flag_results` vector.
    - The function then calls [`_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal) to register the flag with the specified name, callback, and description.
    - It sets the multi-option policy to 'TakeAll' to allow capturing multiple values and runs the default callback.
- **Output**: Returns a pointer to an `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#detaillexical_cast)
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_flag<!-- {{#callable:CLI::App::add_flag}} -->
The `add_flag` function adds a command-line flag to an application, allowing it to trigger a specified callback function.
- **Inputs**:
    - `flag_name`: A string representing the name of the flag to be added.
    - `function`: A callback function of type `std::function<void(std::int64_t)>` that will be executed when the flag is triggered.
    - `flag_description`: An optional string providing a description of the flag.
- **Control Flow**:
    - The function calls [`add_flag_function`](impl/App_inl.hpp.driver.md#Appadd_flag_function), passing the flag name, function, and description after moving them to avoid unnecessary copies.
- **Output**: Returns a pointer to an `Option` object representing the added flag.
- **Functions called**:
    - [`CLI::App::add_flag_function`](impl/App_inl.hpp.driver.md#Appadd_flag_function)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::add\_option\_group<!-- {{#callable:CLI::App::add_option_group}} -->
Creates and adds an option group to the application.
- **Inputs**:
    - `group_name`: The name of the option group to be created.
    - `group_description`: An optional description for the option group.
- **Control Flow**:
    - Checks if the provided `group_name` is valid using `detail::valid_alias_name_string`.
    - If the name is invalid, throws an [`IncorrectConstruction`](Error.hpp.driver.md#IncorrectConstruction) exception.
    - Creates a shared pointer to a new `Option_group` instance with the provided name and description.
    - Retrieves a raw pointer from the shared pointer for further use.
    - Casts the shared pointer to `App_p` for compatibility with older GCC versions.
    - Clears the footer of the new option group and sets a help flag.
    - Adds the new option group as a subcommand to the application.
- **Output**: Returns a pointer to the newly created `Option_group`.
- **Functions called**:
    - [`IncorrectConstruction`](Error.hpp.driver.md#IncorrectConstruction)
    - [`Option_group::add_subcommand`](#Option_groupadd_subcommand)
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::group<!-- {{#callable:CLI::App::group}} -->
Sets the group name for the `App` instance and returns a pointer to the instance.
- **Inputs**:
    - `group_name`: A `std::string` representing the name of the group to be assigned to the `App` instance.
- **Control Flow**:
    - The function assigns the provided `group_name` to the member variable `group_` of the `App` instance.
    - It then returns a pointer to the current instance of `App` (i.e., `this`).
- **Output**: Returns a pointer to the `App` instance after updating its group name.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_subcommand<!-- {{#callable:CLI::App::require_subcommand}} -->
Sets the minimum required subcommands to 1 and allows unlimited maximum subcommands.
- **Inputs**: None
- **Control Flow**:
    - Sets `require_subcommand_min_` to 1, indicating at least one subcommand is required.
    - Sets `require_subcommand_max_` to 0, indicating there is no upper limit on the number of subcommands allowed.
    - Returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_subcommand<!-- {{#callable:CLI::App::require_subcommand}} -->
The `require_subcommand` function sets the minimum and maximum number of required subcommands for an `App` instance.
- **Inputs**:
    - `value`: An integer that specifies the number of required subcommands; negative values indicate a maximum limit.
- **Control Flow**:
    - The function checks if the input `value` is less than 0.
    - If `value` is negative, it sets `require_subcommand_min_` to 0 and `require_subcommand_max_` to the absolute value of `value`.
    - If `value` is non-negative, it sets both `require_subcommand_min_` and `require_subcommand_max_` to the value of `value`.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_subcommand<!-- {{#callable:CLI::App::require_subcommand}} -->
Sets the minimum and maximum number of required subcommands for the `App` instance.
- **Inputs**:
    - `min`: The minimum number of subcommands that must be provided.
    - `max`: The maximum number of subcommands that can be provided; a value of 0 indicates no limit.
- **Control Flow**:
    - Assigns the value of `min` to the member variable `require_subcommand_min_`.
    - Assigns the value of `max` to the member variable `require_subcommand_max_`.
    - Returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_option<!-- {{#callable:CLI::App::require_option}} -->
The `require_option` function sets the minimum required options for the `App` class to 1 and the maximum to unlimited.
- **Inputs**: None
- **Control Flow**:
    - The function directly modifies the member variables `require_option_min_` and `require_option_max_` of the `App` class.
    - It sets `require_option_min_` to 1, indicating that at least one option is required.
    - It sets `require_option_max_` to 0, indicating that there is no upper limit on the number of options.
- **Output**: The function returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_option<!-- {{#callable:CLI::App::require_option}} -->
The `require_option` function sets the minimum and maximum number of required options for a command line application.
- **Inputs**:
    - `value`: An integer that specifies the number of required options; negative values indicate a maximum limit.
- **Control Flow**:
    - If `value` is less than 0, it sets `require_option_min_` to 0 and `require_option_max_` to the absolute value of `value`.
    - If `value` is 0 or greater, it sets both `require_option_min_` and `require_option_max_` to `value`.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::require\_option<!-- {{#callable:CLI::App::require_option}} -->
The `require_option` function sets the minimum and maximum number of options required for the `App` instance.
- **Inputs**:
    - `min`: The minimum number of options that must be provided.
    - `max`: The maximum number of options that can be provided, where 0 indicates unlimited.
- **Control Flow**:
    - The function assigns the input `min` to the member variable `require_option_min_`.
    - The function assigns the input `max` to the member variable `require_option_max_`.
    - Finally, it returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::fallthrough<!-- {{#callable:CLI::App::fallthrough}} -->
Sets the `fallthrough_` flag to allow options to be passed to parent commands.
- **Inputs**:
    - `value`: A boolean flag indicating whether to allow fallthrough of options to parent commands, defaulting to true.
- **Control Flow**:
    - The function sets the member variable `fallthrough_` to the value of the input parameter `value`.
    - It then returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::subcommand\_fallthrough<!-- {{#callable:CLI::App::subcommand_fallthrough}} -->
Sets the `subcommand_fallthrough_` flag to the specified boolean value.
- **Inputs**:
    - `value`: A boolean value that determines whether subcommands are allowed to fall through.
- **Control Flow**:
    - The function assigns the input boolean value to the member variable `subcommand_fallthrough_`.
    - The function returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current instance of the `App` class.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::pre\_callback<!-- {{#callable:CLI::App::pre_callback}} -->
The `pre_callback` function is a virtual method that allows subclasses to execute custom code before the parsing of command line arguments begins.
- **Inputs**: None
- **Control Flow**:
    - The function does not contain any logic or control flow statements.
    - It serves as a placeholder for derived classes to implement their own pre-parsing logic.
- **Output**: The function does not return any value and is intended to be overridden by subclasses to perform actions before parsing.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)


---
#### App::failure\_message<!-- {{#callable:CLI::App::failure_message}} -->
Sets a custom failure message function for the `App` class.
- **Inputs**:
    - `function`: A `std::function` that takes a pointer to an `App` instance and an `Error` reference, returning a `std::string` representing the failure message.
- **Control Flow**:
    - The function assigns the provided `function` to the member variable `failure_message_` of the `App` class.
    - No additional logic or control flow is present; the function simply performs the assignment.
- **Output**: This function does not return a value; it modifies the internal state of the `App` instance by setting the `failure_message_` member.
- **See also**: [`CLI::App`](#CLIApp)  (Data Structure)



---
### startup\_mode<!-- {{#data_structure:CLI::App::startup_mode}} -->
- **Type**: `enum`
- **Members**:
    - `stable`: Represents a stable startup mode with no changes.
    - `enabled`: Represents a startup mode where the application is enabled.
    - `disabled`: Represents a startup mode where the application is disabled.
- **Description**: The `startup_mode` enum class defines three possible startup modes for an application: `stable`, `enabled`, and `disabled`. These modes are used to specify how the application should behave during startup, with `stable` indicating no change, `enabled` indicating the application should start in an enabled state, and `disabled` indicating the application should start in a disabled state.


---
### NameMatch<!-- {{#data_structure:CLI::NameMatch}} -->
- **Type**: `enum`
- **Members**:
    - `none`: Represents no match with a value of 0.
    - `exact`: Represents an exact match with a value of 1.
    - `prefix`: Represents a prefix match with a value of 2.
- **Description**: The `NameMatch` enum class is used to define different types of name matching strategies, specifically for determining if a name matches exactly, as a prefix, or not at all. It is defined with an underlying type of `std::uint8_t`, allowing for efficient storage and comparison of these match types.


---
### Option\_group<!-- {{#data_structure:Option_group}} -->
- **Type**: `class`
- **Members**:
    - `group_`: Stores the group name for the option group.
    - `help_ptr_`: Pointer to the help flag, if any, for the option group.
    - `help_all_ptr_`: Pointer to the help all flag, if any, for the option group.
    - `parent_`: Pointer to the parent App object, indicating the hierarchy of the option group.
- **Description**: The `Option_group` class is a specialized extension of the `App` class designed to manage groups of options within a command-line interface application. It allows for the organization of options into logical groups, facilitating better structure and readability of command-line options. The class provides mechanisms to add existing options and subcommands to the group, and it ensures that option groups have automatic fallthrough behavior, meaning that options not recognized by the group can be passed up to the parent application. This class is particularly useful for complex CLI applications where options need to be grouped for clarity and functionality.
- **Member Functions**:
    - [`Option_group::Option_group`](#Option_groupOption_group)
    - [`Option_group::add_option`](#Option_groupadd_option)
    - [`Option_group::add_options`](#Option_groupadd_options)
    - [`Option_group::add_options`](#Option_groupadd_options)
    - [`Option_group::add_subcommand`](#Option_groupadd_subcommand)
- **Inherits From**:
    - [`CLI::App::App`](#AppApp)

**Methods**

---
#### Option\_group::Option\_group<!-- {{#callable:Option_group::Option_group}} -->
The `Option_group` constructor initializes an option group with a description and name, setting up automatic fallthrough and disabling help flags if the group name is empty or starts with a '+'.

- **Inputs**:
    - `group_description`: A string representing the description of the option group.
    - `group_name`: A string representing the name of the option group.
    - `parent`: A pointer to the parent `App` object to which this option group belongs.
- **Control Flow**:
    - The constructor initializes the base class `App` with the `group_description`, an empty string, and the `parent` pointer.
    - It sets the group name using the [`group`](#Appgroup) method.
    - It checks if the `group_name` is empty or starts with a '+'.
    - If the condition is true, it disables the help flag and help all flag by setting them to empty strings.
- **Output**: The constructor does not return a value; it initializes an `Option_group` object.
- **Functions called**:
    - [`CLI::App::group`](#Appgroup)
    - [`CLI::App::set_help_flag`](impl/App_inl.hpp.driver.md#Appset_help_flag)
    - [`CLI::App::set_help_all_flag`](impl/App_inl.hpp.driver.md#Appset_help_all_flag)
- **See also**: [`Option_group`](#Option_group)  (Data Structure)


---
#### Option\_group::add\_option<!-- {{#callable:Option_group::add_option}} -->
The `add_option` function adds an existing `Option` to the `Option_group` by moving it from its current parent to the `Option_group` instance.
- **Inputs**:
    - `opt`: A pointer to the `Option` object that is to be added to the `Option_group`.
- **Control Flow**:
    - Check if the current `Option_group` has a parent using `get_parent()`; if not, throw an [`OptionNotFound`](Error.hpp.driver.md#HorribleErrorOptionNotFound) exception with a message indicating the option cannot be located.
    - Call the `_move_option` method on the parent to move the `Option` from its current location to the `Option_group`.
    - Return the `Option` pointer `opt`.
- **Output**: Returns the pointer to the `Option` that was added to the `Option_group`.
- **Functions called**:
    - [`CLI::get_parent`](#CLIget_parent)
    - [`HorribleError::OptionNotFound`](Error.hpp.driver.md#HorribleErrorOptionNotFound)
- **See also**: [`Option_group`](#Option_group)  (Data Structure)


---
#### Option\_group::add\_options<!-- {{#callable:Option_group::add_options}} -->
The `add_options` function adds one or more `Option` objects to an `Option_group` by calling the [`add_option`](#Option_groupadd_option) method for each `Option`.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that is to be added to the `Option_group`.
    - `args...`: A variadic template parameter representing additional `Option` pointers to be added to the `Option_group`.
- **Control Flow**:
    - The function first calls [`add_option`](#Option_groupadd_option) with the first `Option` pointer `opt`.
    - It then recursively calls `add_options` with the remaining `Option` pointers `args...`.
- **Output**: The function does not return a value; it modifies the `Option_group` by adding the specified `Option` objects to it.
- **Functions called**:
    - [`Option_group::add_option`](#Option_groupadd_option)
- **See also**: [`Option_group`](#Option_group)  (Data Structure)


---
#### Option\_group::add\_options<!-- {{#callable:Option_group::add_options}} -->
The [`add_options`](#Option_groupadd_options) function recursively adds multiple `Option` objects to an `Option_group` by calling [`add_option`](#Option_groupadd_option) on each one.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that is to be added to the `Option_group`.
    - `args`: A variadic template parameter representing additional `Option` pointers to be added to the `Option_group`.
- **Control Flow**:
    - The function first calls [`add_option`](#Option_groupadd_option) with the first `Option` pointer `opt` to add it to the `Option_group`.
    - It then recursively calls [`add_options`](#Option_groupadd_options) with the remaining `Option` pointers in `args` until all options are added.
- **Output**: The function does not return a value; it modifies the `Option_group` by adding the specified options.
- **Functions called**:
    - [`Option_group::add_option`](#Option_groupadd_option)
    - [`Option_group::add_options`](#Option_groupadd_options)
- **See also**: [`Option_group`](#Option_group)  (Data Structure)


---
#### Option\_group::add\_subcommand<!-- {{#callable:Option_group::add_subcommand}} -->
The [`add_subcommand`](impl/App_inl.hpp.driver.md#Appadd_subcommand) function adds an existing subcommand to an `Option_group` by first removing it from its current parent and then adding it to the current group.
- **Inputs**:
    - `subcom`: A pointer to an `App` object representing the subcommand to be added to the `Option_group`.
- **Control Flow**:
    - Retrieve the parent of the subcommand using `get_parent()` and obtain a shared pointer to the subcommand using `get_subcommand_ptr(subcom)`.
    - Remove the subcommand from its current parent using `remove_subcommand(subcom)`.
    - Add the subcommand to the current `Option_group` using `add_subcommand(std::move(subc))`.
    - Return the original subcommand pointer `subcom`.
- **Output**: Returns a pointer to the `App` object representing the subcommand that was added to the `Option_group`.
- **Functions called**:
    - [`CLI::App::add_subcommand`](impl/App_inl.hpp.driver.md#Appadd_subcommand)
- **See also**: [`Option_group`](#Option_group)  (Data Structure)



---
### AppFriend<!-- {{#data_structure:detail::AppFriend}} -->
- **Type**: `struct`
- **Description**: The `AppFriend` struct is a utility structure within the `CLI::detail` namespace, designed to provide access to certain protected member functions of the `App` class for testing purposes. It includes static template functions that wrap and forward arguments to the `App` class's private methods, such as `_parse_arg` and `_parse_subcommand`, allowing these methods to be tested without exposing them directly. Additionally, it provides a method to access the fallthrough parent of an `App` instance.
- **Member Functions**:
    - [`detail::AppFriend::parse_arg`](#AppFriendparse_arg)
    - [`detail::AppFriend::parse_subcommand`](#AppFriendparse_subcommand)
    - [`detail::AppFriend::parse_arg`](#AppFriendparse_arg)
    - [`detail::AppFriend::parse_subcommand`](#AppFriendparse_subcommand)
    - [`detail::AppFriend::get_fallthrough_parent`](#AppFriendget_fallthrough_parent)

**Methods**

---
#### AppFriend::parse\_arg<!-- {{#callable:detail::AppFriend::parse_arg}} -->
The `parse_arg` function is a template function that forwards its arguments to the `_parse_arg` method of the `App` class, enabling perfect forwarding of arguments.
- **Inputs**:
    - `app`: A pointer to an `App` object, which is the instance on which the `_parse_arg` method will be called.
    - `args`: A variadic template parameter pack representing the arguments to be perfectly forwarded to the `_parse_arg` method of the `App` class.
- **Control Flow**:
    - The function is a template function that accepts a pointer to an `App` object and a variadic number of arguments.
    - It uses `std::forward` to perfectly forward the arguments to the `_parse_arg` method of the `App` class.
    - The function returns the result of the `_parse_arg` method call.
- **Output**: The function returns the result of the `_parse_arg` method call on the `App` object, with the return type being deduced using `decltype(auto)`.
- **See also**: [`detail::AppFriend`](#detailAppFriend)  (Data Structure)


---
#### AppFriend::parse\_subcommand<!-- {{#callable:detail::AppFriend::parse_subcommand}} -->
The `parse_subcommand` function is a template function that forwards its arguments to the `_parse_subcommand` method of the `App` class, enabling the parsing of subcommands.
- **Inputs**:
    - `app`: A pointer to an `App` object, which represents the application or subcommand being parsed.
    - `args`: A variadic template parameter pack representing the arguments to be forwarded to the `_parse_subcommand` method.
- **Control Flow**:
    - The function is a template function that accepts a pointer to an `App` object and a variadic number of arguments.
    - It uses `std::forward` to perfectly forward the arguments to the `_parse_subcommand` method of the `App` class.
    - The function returns the result of the `_parse_subcommand` method call.
- **Output**: The function returns the result of the `_parse_subcommand` method, which is the type determined by the method's return type.
- **See also**: [`detail::AppFriend`](#detailAppFriend)  (Data Structure)


---
#### AppFriend::parse\_arg<!-- {{#callable:detail::AppFriend::parse_arg}} -->
The `parse_arg` function is a template function that forwards its arguments to the `_parse_arg` method of the `App` class, preserving the argument types and references.
- **Inputs**:
    - `app`: A pointer to an `App` object, which is the instance on which the `_parse_arg` method will be called.
    - `args`: A variadic template parameter pack representing the arguments to be perfectly forwarded to the `_parse_arg` method of the `App` class.
- **Control Flow**:
    - The function is a template function that accepts a pointer to an `App` object and a variadic number of arguments.
    - It uses `std::forward` to perfectly forward the arguments to the `_parse_arg` method of the `App` class, preserving their value categories (lvalue or rvalue).
    - The return type is deduced using `std::result_of` to match the return type of the `_parse_arg` method when called with the given arguments.
- **Output**: The output is the result of calling the `_parse_arg` method on the `App` object with the forwarded arguments, and its type is deduced to match the return type of `_parse_arg`.
- **See also**: [`detail::AppFriend`](#detailAppFriend)  (Data Structure)


---
#### AppFriend::parse\_subcommand<!-- {{#callable:detail::AppFriend::parse_subcommand}} -->
The `parse_subcommand` function is a template function that forwards its arguments to the `_parse_subcommand` method of the `App` class, allowing for perfect forwarding of arguments.
- **Inputs**:
    - `app`: A pointer to an `App` object, which is the instance on which the `_parse_subcommand` method will be called.
    - `args`: A variadic template parameter pack representing the arguments to be perfectly forwarded to the `_parse_subcommand` method.
- **Control Flow**:
    - The function is a template function that accepts a pointer to an `App` object and a variadic number of arguments.
    - It uses perfect forwarding to pass the arguments to the `_parse_subcommand` method of the `App` class.
    - The return type is deduced using `std::result_of` to match the return type of the `_parse_subcommand` method.
- **Output**: The output is the result of the `_parse_subcommand` method of the `App` class, with the return type deduced to match that method's return type.
- **See also**: [`detail::AppFriend`](#detailAppFriend)  (Data Structure)


---
#### AppFriend::get\_fallthrough\_parent<!-- {{#callable:detail::AppFriend::get_fallthrough_parent}} -->
The `get_fallthrough_parent` function retrieves the fallthrough parent of a given `App` object by calling its private method `_get_fallthrough_parent`. 
- **Inputs**:
    - `app`: A pointer to an `App` object for which the fallthrough parent is to be retrieved.
- **Control Flow**:
    - The function takes an `App` pointer as input.
    - It calls the private method `_get_fallthrough_parent` on the `App` object pointed to by the input pointer.
    - The result of the method call is returned.
- **Output**: A pointer to the fallthrough parent `App` object.
- **See also**: [`detail::AppFriend`](#detailAppFriend)  (Data Structure)



# Functions

---
### default\_flag\_modifiers<!-- {{#callable:CLI::detail::default_flag_modifiers}} -->
This function configures an `Option` object to use a summing policy for multiple options and sets a default string value.
- **Inputs**:
    - `opt`: A pointer to an `Option` object that will be modified to set its multi-option policy and default string.
- **Control Flow**:
    - The function first calls the `multi_option_policy` method on the `opt` object, passing `MultiOptionPolicy::Sum` to set the policy for handling multiple options.
    - Next, it sets the default string representation for the option to '0' using the `default_str` method.
    - Finally, it invokes the `force_callback` method to ensure that the callback associated with the option is executed.
- **Output**: The function returns a pointer to the modified `Option` object.


---
### get\_subcommands<!-- {{#callable:CLI::CLI11_NODISCARD::vector<App *>::get_subcommands}} -->
The `get_subcommand` method retrieves a subcommand by its name from the current command application.
- **Inputs**:
    - `subcom`: A string representing the name of the subcommand to retrieve.
- **Control Flow**:
    - The method first checks if the provided subcommand name is empty, returning the first subcommand if it is.
    - It then iterates through the list of subcommands, checking each one to see if its name matches the provided name.
    - If a match is found, the corresponding subcommand is returned.
    - If no match is found, the method returns a null pointer.
- **Output**: Returns a pointer to the subcommand if found, or null if the subcommand does not exist.
- **Functions called**:
    - [`CLI::App::set_help_flag`](impl/App_inl.hpp.driver.md#Appset_help_flag)
    - [`CLI::App::add_option`](#Appadd_option)
    - [`CLI::App::_add_flag_internal`](impl/App_inl.hpp.driver.md#App_add_flag_internal)
    - [`CLI::detail::lexical_cast`](TypeTools.hpp.driver.md#detaillexical_cast)
    - [`CLI::App::add_flag_function`](impl/App_inl.hpp.driver.md#Appadd_flag_function)
    - [`IncorrectConstruction`](Error.hpp.driver.md#IncorrectConstruction)
    - [`Option_group::add_subcommand`](#Option_groupadd_subcommand)
    - [`CLI::CLI11_INLINE::App_p::get_subcommand_ptr`](impl/App_inl.hpp.driver.md#App_pget_subcommand_ptr)
    - [`CLI::CLI11_INLINE::size_t::count_all`](impl/App_inl.hpp.driver.md#size_tcount_all)
    - [`CLI::get_option`](#CLIget_option)


---
### got\_subcommand<!-- {{#callable:CLI::got_subcommand}} -->
Checks if a specified subcommand has been parsed.
- **Inputs**:
    - `subcommand_name`: A string representing the name of the subcommand to check.
- **Control Flow**:
    - Calls [`get_subcommand_no_throw`](impl/App_inl.hpp.driver.md#Appget_subcommand_no_throw) with `subcommand_name` to retrieve the corresponding subcommand.
    - If the subcommand exists (not null), it checks if its `parsed_` count is greater than 0.
    - Returns true if the subcommand was parsed, otherwise returns false.
- **Output**: Returns a boolean indicating whether the specified subcommand has been parsed.
- **Functions called**:
    - [`CLI::App::get_subcommand_no_throw`](impl/App_inl.hpp.driver.md#Appget_subcommand_no_throw)


---
### excludes<!-- {{#callable:CLI::excludes}} -->
The `excludes` function adds a subcommand to the exclusion list of the current command, ensuring that it cannot be executed alongside the specified subcommand.
- **Inputs**:
    - `app`: A pointer to an `App` object that represents the subcommand to be excluded.
- **Control Flow**:
    - The function first checks if the input `app` is a null pointer and throws an [`OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound) exception if it is.
    - It then checks if the `app` is the same as the current instance (`this`), throwing an [`OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound) exception if true.
    - The function attempts to insert the `app` into the `exclude_subcommands_` set, which holds subcommands that cannot be executed together.
    - If the insertion is successful (indicated by `res.second` being true), it also adds the current instance (`this`) to the `exclude_subcommands_` set of the `app`.
- **Output**: Returns a pointer to the current instance (`this`) to allow for method chaining.
- **Functions called**:
    - [`HorribleError::OptionNotFound::OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound)


---
### needs<!-- {{#callable:CLI::needs}} -->
The `needs` function adds a specified `App` instance as a required subcommand for the current `App` instance.
- **Inputs**:
    - `app`: A pointer to an `App` instance that is to be added as a required subcommand.
- **Control Flow**:
    - The function first checks if the input `app` pointer is `nullptr`, and if so, it throws an [`OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound) exception with the message 'nullptr passed'.
    - Next, it checks if the input `app` is the same as the current instance (`this`), and if so, it throws an [`OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound) exception with the message 'cannot self reference in needs'.
    - If both checks pass, the input `app` is inserted into the `need_subcommands_` set, indicating that this subcommand is required.
    - Finally, the function returns the current instance (`this`) to allow for method chaining.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.
- **Functions called**:
    - [`HorribleError::OptionNotFound::OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound)


---
### usage<!-- {{#callable:CLI::usage}} -->
Sets a callback function to generate usage information for the command line application.
- **Inputs**:
    - `usage_function`: A callable object (function, lambda, etc.) that returns a string representing the usage information.
- **Control Flow**:
    - The input `usage_function` is moved into the member variable `usage_callback_`.
    - The function returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.


---
### footer<!-- {{#callable:CLI::footer}} -->
Sets a callback function to generate a footer for help output.
- **Inputs**:
    - `footer_function`: A `std::function` that returns a `std::string`, which will be used to generate the footer text for help output.
- **Control Flow**:
    - The function takes a `std::function<std::string()>` as an argument.
    - It moves the provided function into the member variable `footer_callback_`.
    - The function returns a pointer to the current `App` instance.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.


---
### config\_to\_str<!-- {{#callable:CLI::std::string::config_to_str}} -->
Converts the configuration of the application to a string format.
- **Inputs**:
    - `default_also`: A boolean flag indicating whether to include default values in the output.
    - `write_description`: A boolean flag indicating whether to include descriptions of the configuration options in the output.
- **Control Flow**:
    - The function calls the `to_config` method of the `config_formatter_` member, passing itself and the input flags.
    - The `to_config` method is responsible for generating the string representation of the configuration based on the provided parameters.
- **Output**: Returns a string that represents the application's configuration, formatted according to the specified options.


---
### get\_formatter<!-- {{#callable:CLI::std::shared_ptr<FormatterBase>::get_formatter}} -->
Returns a shared pointer to the current `FormatterBase` instance.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the member variable `formatter_` which is a shared pointer to a `FormatterBase` object.
- **Output**: A `std::shared_ptr<FormatterBase>` that points to the current formatter used for help printing.


---
### get\_config\_formatter<!-- {{#callable:CLI::std::shared_ptr<Config>::get_config_formatter}} -->
Returns a shared pointer to the `Config` object used for formatting.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the member variable `config_formatter_` which is a shared pointer to a `Config` object.
- **Output**: Returns a `std::shared_ptr<Config>` that points to the current configuration formatter.


---
### get\_config\_formatter\_base<!-- {{#callable:CLI::std::shared_ptr<ConfigBase>::get_config_formatter_base}} -->
Returns a shared pointer to a `ConfigBase` object by casting the `config_formatter_` member.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - Checks if static RTTI is enabled using the preprocessor directive `CLI11_USE_STATIC_RTTI`.
    - If static RTTI is not enabled, it uses `std::dynamic_pointer_cast` to cast `config_formatter_` to `ConfigBase`.
    - If static RTTI is enabled, it uses `std::static_pointer_cast` for the cast.
- **Output**: Returns a `std::shared_ptr<ConfigBase>` that points to the `config_formatter_` member, casted appropriately based on the RTTI settings.


---
### get\_description<!-- {{#callable:CLI::std::string::get_description}} -->
Retrieves the description of the application or subcommand.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the value of the member variable `description_`.
- **Output**: Returns a `std::string` containing the description of the application or subcommand.


---
### description<!-- {{#callable:CLI::description}} -->
Sets the description of the application and returns a pointer to the application instance.
- **Inputs**:
    - `app_description`: A `std::string` representing the description of the application.
- **Control Flow**:
    - The function takes a string input representing the application description.
    - It uses `std::move` to efficiently transfer the input string to the member variable `description_`.
    - Finally, it returns a pointer to the current instance of the `App` class.
- **Output**: Returns a pointer to the current `App` instance, allowing for method chaining.


---
### get\_option<!-- {{#callable:CLI::get_option}} -->
Retrieves an `Option` by its name, throwing an exception if not found.
- **Inputs**:
    - `option_name`: A `std::string` representing the name of the option to retrieve.
- **Control Flow**:
    - Calls [`get_option_no_throw`](impl/App_inl.hpp.driver.md#Appget_option_no_throw) with `option_name` to attempt to retrieve the option.
    - Checks if the returned pointer is `nullptr`, indicating the option was not found.
    - If the option is not found, throws an [`OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound) exception with the `option_name`.
    - If the option is found, returns the pointer to the `Option`.
- **Output**: Returns a pointer to the `Option` associated with the given `option_name`.
- **Functions called**:
    - [`CLI::App::get_option_no_throw`](impl/App_inl.hpp.driver.md#Appget_option_no_throw)
    - [`HorribleError::OptionNotFound::OptionNotFound`](Error.hpp.driver.md#OptionNotFoundOptionNotFound)


---
### operator\[\]<!-- {{#callable:CLI::operator[]}} -->
The `operator[]` function provides a convenient way to access an `Option` object by its name.
- **Inputs**:
    - `option_name`: A pointer to a C-style string (const char*) representing the name of the option to retrieve.
- **Control Flow**:
    - The function calls [`get_option`](#CLIget_option) with the provided `option_name`.
    - The result of [`get_option`](#CLIget_option) is returned directly.
- **Output**: Returns a pointer to the `Option` object associated with the specified name, or nullptr if the option does not exist.
- **Functions called**:
    - [`CLI::get_option`](#CLIget_option)


---
### get\_ignore\_case<!-- {{#callable:CLI::get_ignore_case}} -->
The `get_ignore_case` function retrieves the current status of the `ignore_case_` flag.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the private member variable `ignore_case_`.
    - It returns the value of `ignore_case_` without any additional processing.
- **Output**: The function returns a boolean value indicating whether case sensitivity is ignored in the application.


---
### get\_ignore\_underscore<!-- {{#callable:CLI::get_ignore_underscore}} -->
The `get_ignore_underscore` function retrieves the current value of the `ignore_underscore_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `ignore_underscore_`.
    - It returns the value of `ignore_underscore_` without any additional logic or conditions.
- **Output**: The function returns a boolean value indicating whether underscores should be ignored.


---
### get\_fallthrough<!-- {{#callable:CLI::get_fallthrough}} -->
Returns the value of the `fallthrough_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `fallthrough_`.
    - It returns the boolean value of `fallthrough_` without any additional logic or conditions.
- **Output**: A boolean value indicating whether fallthrough is allowed.


---
### get\_subcommand\_fallthrough<!-- {{#callable:CLI::get_subcommand_fallthrough}} -->
Retrieves the value of the `subcommand_fallthrough_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `subcommand_fallthrough_` member variable without any conditions or loops.
- **Output**: Returns a boolean indicating whether subcommand fallthrough is enabled.


---
### get\_allow\_windows\_style\_options<!-- {{#callable:CLI::get_allow_windows_style_options}} -->
Retrieves the current setting for allowing Windows-style options in the command line application.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `allow_windows_style_options_`.
    - It returns the value of `allow_windows_style_options_` without any additional logic or conditions.
- **Output**: Returns a boolean value indicating whether Windows-style options are allowed.


---
### get\_positionals\_at\_end<!-- {{#callable:CLI::get_positionals_at_end}} -->
Returns the value of the `positionals_at_end_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `positionals_at_end_`.
    - It returns the boolean value stored in `positionals_at_end_`.
- **Output**: A boolean indicating whether positional arguments are allowed at the end of the command line.


---
### get\_configurable<!-- {{#callable:CLI::get_configurable}} -->
The `get_configurable` function retrieves the value of the `configurable_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `configurable_`.
    - It returns the boolean value of `configurable_` without any additional logic or conditions.
- **Output**: Returns a boolean indicating whether the app is configurable.


---
### get\_group<!-- {{#callable:CLI::get_group}} -->
Returns a constant reference to the `group_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `group_` without any conditions or loops.
- **Output**: A constant reference to a `std::string` representing the group name of the command line application.


---
### get\_usage<!-- {{#callable:CLI::std::string::get_usage}} -->
The `get_usage` function generates a usage string for the command line application, optionally including a callback-generated usage description.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function checks if `usage_callback_` is set (not null).
    - If `usage_callback_` is set, it calls this function to get a usage string and appends the `usage_` string to it.
    - If `usage_callback_` is not set, it simply returns the `usage_` string.
- **Output**: The function returns a `std::string` that contains the usage information for the application, which may include additional information from a callback if provided.


---
### get\_footer<!-- {{#callable:CLI::std::string::get_footer}} -->
The `get_footer` function retrieves the footer text for a command line application, optionally appending a callback-generated string.
- **Inputs**:
    - `footer_callback_`: A function pointer that, if set, generates additional footer text.
    - `footer_`: A string containing the default footer text.
- **Control Flow**:
    - The function checks if `footer_callback_` is not null.
    - If `footer_callback_` is valid, it calls the function and concatenates its result with `footer_` and a newline character.
    - If `footer_callback_` is null, it simply returns `footer_`.
- **Output**: Returns a string that is either the concatenated result of the callback output and the footer, or just the footer if no callback is provided.


---
### get\_require\_subcommand\_min<!-- {{#callable:CLI::std::size_t::get_require_subcommand_min}} -->
The `get_require_subcommand_min` function retrieves the minimum number of required subcommands for the command line application.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `require_subcommand_min_`.
    - It returns the value of `require_subcommand_min_` without any additional logic or conditions.
- **Output**: The function returns a `std::size_t` value representing the minimum number of required subcommands.


---
### get\_require\_subcommand\_max<!-- {{#callable:CLI::std::size_t::get_require_subcommand_max}} -->
Retrieves the maximum number of required subcommands for the application.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `require_subcommand_max_`.
    - No conditional logic or loops are present in this function.
- **Output**: Returns a `std::size_t` representing the maximum number of subcommands that are required for the application.


---
### get\_require\_option\_min<!-- {{#callable:CLI::std::size_t::get_require_option_min}} -->
Retrieves the minimum number of required options for the command line application.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `require_option_min_`.
    - It returns the value of `require_option_min_` without any additional processing.
- **Output**: Returns a `std::size_t` representing the minimum number of options that must be provided when using the command line application.


---
### get\_require\_option\_max<!-- {{#callable:CLI::std::size_t::get_require_option_max}} -->
The `get_require_option_max` function retrieves the maximum number of options that can be required.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `require_option_max_`.
    - It returns the value of `require_option_max_` without any additional logic or conditions.
- **Output**: Returns a `std::size_t` representing the maximum number of required options.


---
### get\_prefix\_command<!-- {{#callable:CLI::get_prefix_command}} -->
The `get_prefix_command` function retrieves the value of the `prefix_command_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `prefix_command_`.
    - It returns the boolean value of `prefix_command_` without any conditional logic.
- **Output**: Returns a boolean indicating whether prefix command processing is enabled or not.


---
### get\_allow\_extras<!-- {{#callable:CLI::get_allow_extras}} -->
Returns the value of the `allow_extras_` member variable, indicating whether extra arguments are permitted.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `allow_extras_`.
    - It returns the boolean value of `allow_extras_` without any additional logic or conditions.
- **Output**: A boolean value indicating if extra arguments are allowed in the command line parsing.


---
### get\_required<!-- {{#callable:CLI::get_required}} -->
The `get_required` function returns the value of the `required_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `required_`.
    - It returns the boolean value of `required_` without any conditions or loops.
- **Output**: The output is a boolean indicating whether the subcommand is required to be processed.


---
### get\_disabled<!-- {{#callable:CLI::get_disabled}} -->
The `get_disabled` function retrieves the current state of the `disabled_` member variable.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly returns the value of the `disabled_` member variable without any conditional logic or loops.
- **Output**: Returns a boolean value indicating whether the subcommand or option group is disabled.


---
### get\_silent<!-- {{#callable:CLI::get_silent}} -->
The `get_silent` function retrieves the current state of the `silent_` flag.
- **Inputs**:
    - `this`: A constant pointer to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `silent_` of the class instance.
    - It returns the value of `silent_` without any additional logic or conditions.
- **Output**: The function returns a boolean value indicating whether the `silent_` flag is set to true or false.


---
### get\_allow\_non\_standard\_option\_names<!-- {{#callable:CLI::get_allow_non_standard_option_names}} -->
Retrieves the status of allowing non-standard option names in the command line application.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `allow_non_standard_options_`.
- **Output**: Returns a boolean value indicating whether non-standard option names are allowed.


---
### get\_allow\_subcommand\_prefix\_matching<!-- {{#callable:CLI::get_allow_subcommand_prefix_matching}} -->
Retrieves the value of the `allow_prefix_matching_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `allow_prefix_matching_`.
- **Output**: Returns a boolean indicating whether subcommand prefix matching is allowed.


---
### get\_immediate\_callback<!-- {{#callable:CLI::get_immediate_callback}} -->
The `get_immediate_callback` function retrieves the value of the `immediate_callback_` member variable.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the private member variable `immediate_callback_`.
    - It returns the value of `immediate_callback_` without any additional processing.
- **Output**: The function returns a boolean value indicating whether immediate callbacks are enabled (true) or not (false).


---
### get\_disabled\_by\_default<!-- {{#callable:CLI::get_disabled_by_default}} -->
The `get_disabled_by_default` function checks if the application is set to be disabled by default.
- **Inputs**: None
- **Control Flow**:
    - The function evaluates the condition of `default_startup` against the `startup_mode::disabled` enumeration.
    - It returns a boolean value indicating whether the application is disabled by default.
- **Output**: The function returns a boolean value: true if the application is disabled by default, false otherwise.


---
### get\_enabled\_by\_default<!-- {{#callable:CLI::get_enabled_by_default}} -->
Returns true if the default startup mode is set to enabled.
- **Inputs**: None
- **Control Flow**:
    - The function checks the value of the `default_startup` member variable.
    - It compares `default_startup` with the `startup_mode::enabled` enumeration.
    - If they are equal, it returns true; otherwise, it returns false.
- **Output**: Returns a boolean value indicating whether the default startup mode is enabled.


---
### get\_validate\_positionals<!-- {{#callable:CLI::get_validate_positionals}} -->
Retrieves the current status of the `validate_positionals_` flag.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `validate_positionals_`.
    - It returns the value of `validate_positionals_` without any additional logic or conditions.
- **Output**: Returns a boolean indicating whether positional arguments are validated before assignment.


---
### get\_validate\_optional\_arguments<!-- {{#callable:CLI::get_validate_optional_arguments}} -->
The `get_validate_optional_arguments` function retrieves the current state of the `validate_optional_arguments_` flag.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `validate_optional_arguments_`.
    - It returns the value of `validate_optional_arguments_` without any additional logic or conditions.
- **Output**: The function returns a boolean value indicating whether optional arguments are validated.


---
### get\_help\_ptr<!-- {{#callable:CLI::get_help_ptr}} -->
The `get_help_ptr` function returns a pointer to the help option associated with the command line application.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the member variable `help_ptr_` which is a pointer to an `Option` object.
    - It returns the value of `help_ptr_` without any additional processing or checks.
- **Output**: The output is a pointer to an `Option` object that represents the help option, or `nullptr` if no help option is set.


---
### get\_help\_all\_ptr<!-- {{#callable:CLI::get_help_all_ptr}} -->
Returns a pointer to the help all option.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `help_all_ptr_`.
- **Output**: A pointer to an `Option` object representing the help all option, or nullptr if it is not set.


---
### get\_config\_ptr<!-- {{#callable:CLI::get_config_ptr}} -->
Returns a pointer to the configuration option.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the value of the member variable `config_ptr_`.
- **Output**: Returns a pointer to an `Option` object representing the configuration option.


---
### get\_version\_ptr<!-- {{#callable:CLI::get_version_ptr}} -->
Returns a pointer to the version option of the command line application.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `version_ptr_`.
    - No conditional logic or loops are present; it simply returns the value of `version_ptr_`.
- **Output**: Returns a pointer to an `Option` object that represents the version flag, or nullptr if no version flag is set.


---
### get\_parent<!-- {{#callable:CLI::get_parent}} -->
Returns a pointer to the parent `App` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `parent_`.
- **Output**: A pointer to the parent `App` object, or `nullptr` if there is no parent.


---
### get\_name<!-- {{#callable:CLI::get_name}} -->
Returns a constant reference to the `name_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the `name_` member variable without any conditions or loops.
- **Output**: A constant reference to a `std::string` representing the name of the application or subcommand.


---
### get\_aliases<!-- {{#callable:CLI::std::get_aliases}} -->
The `get_aliases` function retrieves a constant reference to the vector of alias names associated with the command line application.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the member variable `aliases_`, which is a vector of strings.
    - No conditional logic or iterations are present in this function.
- **Output**: The output is a constant reference to a vector of strings containing the aliases for the command line application.


---
### clear\_aliases<!-- {{#callable:CLI::clear_aliases}} -->
The `clear_aliases` function clears all aliases associated with the `App` instance.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function calls the `clear` method on the `aliases_` member, which removes all elements from the aliases list.
    - After clearing the aliases, the function returns a pointer to the current `App` instance.
- **Output**: The function returns a pointer to the current `App` instance, allowing for method chaining.


---
### parse\_order<!-- {{#callable:CLI::std::parse_order}} -->
The `parse_order` function returns a constant reference to the vector of pointers representing the original order of options parsed.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `parse_order_` which is a vector of pointers to `Option` objects.
    - It returns this vector without any modifications or additional processing.
- **Output**: The output is a constant reference to a vector of `Option*`, which contains the pointers to the options in the order they were parsed.


---
### deprecate\_option<!-- {{#callable:deprecate_option}} -->
Marks a specified option in an `App` as deprecated.
- **Inputs**:
    - `app`: A reference to an `App` object that contains the option to be deprecated.
    - `option_name`: A string representing the name of the option to be deprecated.
    - `replacement`: An optional string that specifies a replacement option for the deprecated one.
- **Control Flow**:
    - The function retrieves the option associated with the given `option_name` from the `app` using the `get_option` method.
    - It then calls the overloaded [`deprecate_option`](impl/App_inl.hpp.driver.md#CLIdeprecate_option) function, passing the retrieved option and the optional replacement string.
- **Output**: This function does not return a value; it modifies the state of the specified option to indicate that it is deprecated.
- **Functions called**:
    - [`CLI::deprecate_option`](impl/App_inl.hpp.driver.md#CLIdeprecate_option)


---
### App<!-- {{#callable:CLI::App::App}} -->
Constructs an `App` instance with optional description and name.
- **Inputs**:
    - `app_description`: A string that describes the application, defaulting to an empty string.
    - `app_name`: A string that represents the name of the application, defaulting to an empty string.
- **Control Flow**:
    - The constructor initializes the `App` object by calling another constructor with the provided description and name, passing a nullptr for the parent.
    - It sets a help flag using the `set_help_flag` method, which allows users to print a help message and exit the application.
- **Output**: This constructor does not return a value but initializes an `App` object with the specified description and name.


