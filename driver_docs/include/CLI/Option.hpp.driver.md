# Purpose
This C++ header file is part of a library designed to facilitate command-line interface (CLI) parsing, specifically within the CLI11 framework. The file defines classes and enumerations that manage command-line options, their configurations, and behaviors. The primary classes defined are `OptionBase`, [`OptionDefaults`](#OptionDefaultsOptionDefaults), and [`Option`](#OptionOption), which are used to represent and manipulate command-line options. The `OptionBase` class serves as a template base class for [`Option`](#OptionOption) and [`OptionDefaults`](#OptionDefaultsOptionDefaults), providing shared functionality such as setting option groups, required status, and multi-option policies. The [`Option`](#OptionOption) class extends `OptionBase` to include more specific attributes and methods for handling command-line arguments, such as short and long names, descriptions, validators, and callbacks. The [`OptionDefaults`](#OptionDefaultsOptionDefaults) class is a specialized version of `OptionBase` that supports setting default values for options.

The file also defines an enumeration `MultiOptionPolicy` that specifies how multiple arguments for a single option should be handled, such as taking the last argument or joining all arguments into a single string. The use of templates and function pointers allows for flexible and dynamic option handling, making the library suitable for a wide range of command-line applications. The file includes several utility functions and methods for setting and retrieving option properties, validating input, and managing dependencies between options. This header file is intended to be included in other parts of the CLI11 library or user applications to provide a robust and customizable command-line parsing solution.
# Imports and Dependencies

---
- `algorithm`
- `functional`
- `memory`
- `set`
- `string`
- `tuple`
- `utility`
- `vector`
- `Error.hpp`
- `Macros.hpp`
- `Split.hpp`
- `StringTools.hpp`
- `Validators.hpp`
- `impl/Option_inl.hpp`


# Data Structures

---
### MultiOptionPolicy<!-- {{#data_structure:CLI::MultiOptionPolicy}} -->
- **Type**: `enum`
- **Members**:
    - `Throw`: Throw an error if any extra arguments were given.
    - `TakeLast`: Take only the last expected number of arguments.
    - `TakeFirst`: Take only the first expected number of arguments.
    - `Join`: Merge all the arguments together into a single string via the delimiter character, defaulting to '\n'.
    - `TakeAll`: Get all the passed arguments regardless of count.
    - `Sum`: Sum all the arguments together if numerical or concatenate directly without a delimiter.
    - `Reverse`: Take only the last expected number of arguments in reverse order.
- **Description**: The `MultiOptionPolicy` enum defines various strategies for handling multiple arguments in a command-line interface context. Each enumerator specifies a different policy, such as throwing an error for extra arguments, taking only the first or last set of expected arguments, joining all arguments into a single string, summing numerical arguments, or reversing the order of arguments. This enum is used to control how extra command-line arguments are processed beyond the expected number.


---
### OptionBase<!-- {{#data_structure:CLI::OptionBase}} -->
- **Type**: `class`
- **Members**:
    - `group_`: Stores the group membership of the option.
    - `required_`: Indicates if the option is required.
    - `ignore_case_`: Determines if case should be ignored when matching options.
    - `ignore_underscore_`: Determines if underscores should be ignored when matching options.
    - `configurable_`: Indicates if the option can be set in a configuration file.
    - `disable_flag_override_`: Indicates if overriding flag values with '=value' is disabled.
    - `delimiter_`: Specifies a delimiter character for vector arguments.
    - `always_capture_default_`: Indicates if the default value should always be captured.
    - `multi_option_policy_`: Defines the policy for handling multiple arguments beyond the expected maximum.
- **Description**: `OptionBase` is a CRTP (Curiously Recurring Template Pattern) base class designed to provide common functionality for options in a command-line interface application. It encapsulates various properties and behaviors related to command-line options, such as group membership, requirement status, case sensitivity, configurability, and handling of multiple arguments. The class is intended to be inherited by specific option classes, allowing them to share and extend its functionality. It also provides a set of protected member variables that define the characteristics of an option, such as whether it is required, if it should ignore case or underscores, and how it should handle multiple arguments.
- **Member Functions**:
    - [`CLI::OptionBase::group`](#OptionBasegroup)
    - [`CLI::OptionBase::required`](#OptionBaserequired)
    - [`CLI::OptionBase::mandatory`](#OptionBasemandatory)
    - [`CLI::OptionBase::always_capture_default`](#OptionBasealways_capture_default)
    - [`CLI::OptionBase::get_required`](#OptionBaseget_required)
    - [`CLI::OptionBase::get_ignore_case`](#OptionBaseget_ignore_case)
    - [`CLI::OptionBase::get_ignore_underscore`](#OptionBaseget_ignore_underscore)
    - [`CLI::OptionBase::get_configurable`](#OptionBaseget_configurable)
    - [`CLI::OptionBase::get_disable_flag_override`](#OptionBaseget_disable_flag_override)
    - [`CLI::OptionBase::get_delimiter`](#OptionBaseget_delimiter)
    - [`CLI::OptionBase::get_always_capture_default`](#OptionBaseget_always_capture_default)
    - [`CLI::OptionBase::get_multi_option_policy`](#OptionBaseget_multi_option_policy)
    - [`CLI::OptionBase::take_last`](#OptionBasetake_last)
    - [`CLI::OptionBase::take_first`](#OptionBasetake_first)
    - [`CLI::OptionBase::take_all`](#OptionBasetake_all)
    - [`CLI::OptionBase::join`](#OptionBasejoin)
    - [`CLI::OptionBase::join`](#OptionBasejoin)
    - [`CLI::OptionBase::configurable`](#OptionBaseconfigurable)
    - [`CLI::OptionBase::delimiter`](#OptionBasedelimiter)

**Methods**

---
#### OptionBase::group<!-- {{#callable:CLI::OptionBase::group}} -->
The `group` function sets the group membership of an option to a specified name after validating the name for invalid characters.
- **Inputs**:
    - `name`: A constant reference to a `std::string` representing the name of the group to set for the option.
- **Control Flow**:
    - The function first checks if the provided `name` is valid by calling `detail::valid_alias_name_string(name)`.
    - If the name is invalid, it throws an [`IncorrectConstruction`](Error.hpp.driver.md#IncorrectConstruction) exception with a specific error message.
    - If the name is valid, it assigns the `name` to the `group_` member variable.
    - Finally, it returns a pointer to the current object cast to `CRTP *`.
- **Output**: A pointer to the current object cast to `CRTP *`, allowing for method chaining.
- **Functions called**:
    - [`IncorrectConstruction`](Error.hpp.driver.md#IncorrectConstruction)
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::required<!-- {{#callable:CLI::OptionBase::required}} -->
The `required` function sets the `required_` flag of an `OptionBase` object to indicate whether the option is mandatory and returns a pointer to the object itself.
- **Inputs**:
    - `value`: A boolean value indicating whether the option should be marked as required; defaults to `true`.
- **Control Flow**:
    - The function assigns the input `value` to the `required_` member variable of the `OptionBase` class.
    - It then returns a pointer to the current object, cast to the `CRTP` type.
- **Output**: A pointer to the current object, cast to the `CRTP` type, allowing for method chaining.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::mandatory<!-- {{#callable:CLI::OptionBase::mandatory}} -->
The `mandatory` function sets an option as required by calling the [`required`](#OptionBaserequired) method with a specified boolean value.
- **Inputs**:
    - `value`: A boolean value indicating whether the option should be set as required; defaults to true.
- **Control Flow**:
    - The function calls the [`required`](#OptionBaserequired) method with the provided `value` argument.
    - The [`required`](#OptionBaserequired) method sets the `required_` member variable to the given `value`.
    - The [`required`](#OptionBaserequired) method returns a pointer to the current instance cast to the CRTP type.
- **Output**: A pointer to the current instance of the class, cast to the CRTP type.
- **Functions called**:
    - [`CLI::OptionBase::required`](#OptionBaserequired)
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::always\_capture\_default<!-- {{#callable:CLI::OptionBase::always_capture_default}} -->
The `always_capture_default` method sets the `always_capture_default_` flag to the specified boolean value and returns a pointer to the current object cast to the CRTP type.
- **Inputs**:
    - `value`: A boolean value that determines whether the default value should always be captured; defaults to true if not specified.
- **Control Flow**:
    - The method assigns the input boolean value to the `always_capture_default_` member variable.
    - It then returns a pointer to the current object, cast to the CRTP type.
- **Output**: A pointer to the current object, cast to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_required<!-- {{#callable:CLI::OptionBase::get_required}} -->
The `get_required` function returns a boolean indicating whether an option is marked as required in the `OptionBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `required_` member variable, which is a boolean indicating if the option is required.
- **Output**: A boolean value representing whether the option is required (`true`) or not (`false`).
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_ignore\_case<!-- {{#callable:CLI::OptionBase::get_ignore_case}} -->
The `get_ignore_case` function returns the current status of the `ignore_case_` flag, indicating whether case should be ignored when matching options.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `ignore_case_` member variable.
- **Output**: A boolean value indicating whether case is ignored in option matching.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_ignore\_underscore<!-- {{#callable:CLI::OptionBase::get_ignore_underscore}} -->
The `get_ignore_underscore` function returns the current status of whether underscores are ignored when matching options.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `ignore_underscore_` member variable.
- **Output**: A boolean value indicating whether underscores are ignored in option matching.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_configurable<!-- {{#callable:CLI::OptionBase::get_configurable}} -->
The `get_configurable` function returns the status of whether an option can be included in a configuration file.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `configurable_` member variable.
- **Output**: A boolean value indicating if the option is configurable.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_disable\_flag\_override<!-- {{#callable:CLI::OptionBase::get_disable_flag_override}} -->
The `get_disable_flag_override` function returns the current status of the `disable_flag_override_` member variable, indicating whether flag value overriding is disabled.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `disable_flag_override_` member variable.
- **Output**: A boolean value indicating whether the flag override is disabled (`true`) or not (`false`).
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_delimiter<!-- {{#callable:CLI::OptionBase::get_delimiter}} -->
The `get_delimiter` function returns the delimiter character used for vector arguments in the `OptionBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `delimiter_` member variable.
- **Output**: A `char` representing the delimiter character.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_always\_capture\_default<!-- {{#callable:CLI::OptionBase::get_always_capture_default}} -->
The `get_always_capture_default` function returns the status of whether the option is set to automatically capture its default value for help printing.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `always_capture_default_` member variable.
- **Output**: A boolean value indicating if the option is set to automatically capture its default value.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::get\_multi\_option\_policy<!-- {{#callable:CLI::OptionBase::get_multi_option_policy}} -->
The `get_multi_option_policy` function returns the current multi-option policy setting for handling multiple arguments beyond the expected maximum in an `OptionBase` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `multi_option_policy_` member variable, which is of type `MultiOptionPolicy`.
- **Output**: The function returns a `MultiOptionPolicy` enumeration value, indicating the current policy for handling multiple arguments.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::take\_last<!-- {{#callable:CLI::OptionBase::take_last}} -->
The `take_last` function sets the multi-option policy of an option to `TakeLast`, ensuring that only the last of multiple provided arguments is considered.
- **Inputs**: None
- **Control Flow**:
    - The function begins by casting the current object to the CRTP type using `static_cast<CRTP *>(this)`.
    - It then calls the `multi_option_policy` method on the casted object, passing `MultiOptionPolicy::TakeLast` as the argument to set the policy.
    - Finally, the function returns the casted object.
- **Output**: The function returns a pointer to the current object casted to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::take\_first<!-- {{#callable:CLI::OptionBase::take_first}} -->
The `take_first` function sets the multi-option policy of an option to take only the first expected number of arguments and returns a pointer to the current object.
- **Inputs**: None
- **Control Flow**:
    - The function casts the current object to a pointer of type `CRTP`.
    - It calls the `multi_option_policy` method on the casted object with `MultiOptionPolicy::TakeFirst` as the argument.
    - The function returns the casted object.
- **Output**: A pointer to the current object of type `CRTP`. This allows for method chaining.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::take\_all<!-- {{#callable:CLI::OptionBase::take_all}} -->
The `take_all` function sets the multi-option policy of an option to `TakeAll`, allowing all passed arguments to be accepted, and returns a pointer to the current object.
- **Inputs**: None
- **Control Flow**:
    - The function casts the current object to the CRTP type using `static_cast`.
    - It sets the `multi_option_policy` of the object to `MultiOptionPolicy::TakeAll`.
    - The function returns a pointer to the current object.
- **Output**: A pointer to the current object of type `CRTP *`.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::join<!-- {{#callable:CLI::OptionBase::join}} -->
The `join` function sets the multi-option policy of an option to `Join`, allowing multiple arguments to be merged into a single string using a delimiter.
- **Inputs**: None
- **Control Flow**:
    - The function casts the current object to the CRTP type using `static_cast`.
    - It then calls the `multi_option_policy` method on the casted object, passing `MultiOptionPolicy::Join` as the argument.
    - Finally, it returns the casted object.
- **Output**: A pointer to the current object casted to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::join<!-- {{#callable:CLI::OptionBase::join}} -->
The `join` function sets a delimiter character and configures the multi-option policy to join multiple arguments into a single string using the specified delimiter.
- **Inputs**:
    - `delim`: A character that specifies the delimiter to be used when joining multiple arguments.
- **Control Flow**:
    - Cast the current object to the CRTP type using `static_cast`.
    - Set the `delimiter_` member variable of the object to the provided `delim` character.
    - Set the `multi_option_policy_` member variable to `MultiOptionPolicy::Join`.
    - Return the casted object.
- **Output**: A pointer to the current object casted to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::configurable<!-- {{#callable:CLI::OptionBase::configurable}} -->
The `configurable` function sets the `configurable_` member variable to the specified boolean value and returns a pointer to the current object cast to the CRTP type.
- **Inputs**:
    - `value`: A boolean value that determines whether the option is configurable, defaulting to true.
- **Control Flow**:
    - The function assigns the input boolean `value` to the member variable `configurable_`.
    - It then returns a pointer to the current object, cast to the CRTP type.
- **Output**: A pointer to the current object, cast to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)


---
#### OptionBase::delimiter<!-- {{#callable:CLI::OptionBase::delimiter}} -->
The `delimiter` function sets a delimiter character for vector arguments and returns a pointer to the current object.
- **Inputs**:
    - `value`: A character that specifies the delimiter for vector arguments; defaults to '\0' if not provided.
- **Control Flow**:
    - The function assigns the input character `value` to the member variable `delimiter_`.
    - It then returns a pointer to the current object, cast to the CRTP (Curiously Recurring Template Pattern) type.
- **Output**: A pointer to the current object, cast to the CRTP type.
- **See also**: [`CLI::OptionBase`](#OptionBase)  (Data Structure)



---
### OptionDefaults<!-- {{#data_structure:CLI::OptionDefaults}} -->
- **Type**: `class`
- **Members**:
    - `multi_option_policy_`: Stores the policy for handling multiple arguments beyond the expected maximum.
    - `ignore_case_`: Indicates whether the case of the option name should be ignored.
    - `ignore_underscore_`: Indicates whether underscores in the option name should be ignored.
    - `disable_flag_override_`: Indicates whether overriding flag values with an '=<value>' segment is disabled.
    - `delimiter_`: Specifies a delimiter character to split up single arguments to treat as multiple inputs.
- **Description**: The `OptionDefaults` class is a specialized version of the `OptionBase` class designed to handle default settings for command-line options in an application. It provides mechanisms to configure how options are parsed and interpreted, such as ignoring case or underscores in option names, disabling flag overrides, and setting delimiters for splitting arguments. This class is used to define default behaviors that can be applied to options within an application, allowing for consistent handling of command-line arguments.
- **Member Functions**:
    - [`CLI::OptionDefaults::OptionDefaults`](#OptionDefaultsOptionDefaults)
    - [`CLI::OptionDefaults::multi_option_policy`](#OptionDefaultsmulti_option_policy)
    - [`CLI::OptionDefaults::ignore_case`](#OptionDefaultsignore_case)
    - [`CLI::OptionDefaults::ignore_underscore`](#OptionDefaultsignore_underscore)
    - [`CLI::OptionDefaults::disable_flag_override`](#OptionDefaultsdisable_flag_override)
    - [`CLI::OptionDefaults::delimiter`](#OptionDefaultsdelimiter)
- **Inherits From**:
    - [`CLI::OptionBase`](#OptionBase)

**Methods**

---
#### OptionDefaults::OptionDefaults<!-- {{#callable:CLI::OptionDefaults::OptionDefaults}} -->
The `OptionDefaults` constructor initializes an instance of the `OptionDefaults` class with default settings.
- **Inputs**: None
- **Control Flow**:
    - The constructor `OptionDefaults()` is defined as `default`, meaning it uses the compiler-generated default constructor.
    - No additional logic or initialization is performed within this constructor.
- **Output**: An instance of the `OptionDefaults` class is created with default values for its member variables.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)


---
#### OptionDefaults::multi\_option\_policy<!-- {{#callable:CLI::OptionDefaults::multi_option_policy}} -->
The `multi_option_policy` method sets the policy for handling multiple arguments beyond the expected maximum in the `OptionDefaults` class.
- **Inputs**:
    - `value`: An optional parameter of type `MultiOptionPolicy` that specifies the policy to be set, defaulting to `MultiOptionPolicy::Throw`.
- **Control Flow**:
    - The method assigns the provided `value` to the `multi_option_policy_` member variable of the `OptionDefaults` class.
    - The method returns a pointer to the current instance of `OptionDefaults`.
- **Output**: A pointer to the current instance of `OptionDefaults`, allowing for method chaining.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)


---
#### OptionDefaults::ignore\_case<!-- {{#callable:CLI::OptionDefaults::ignore_case}} -->
The `ignore_case` method sets the `ignore_case_` member variable to the specified boolean value and returns the current instance of `OptionDefaults`.
- **Inputs**:
    - `value`: A boolean value indicating whether to ignore case (default is true).
- **Control Flow**:
    - The method assigns the input `value` to the `ignore_case_` member variable.
    - The method returns the current instance of `OptionDefaults` using `this`.
- **Output**: Returns a pointer to the current `OptionDefaults` instance.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)


---
#### OptionDefaults::ignore\_underscore<!-- {{#callable:CLI::OptionDefaults::ignore_underscore}} -->
The `ignore_underscore` method sets the `ignore_underscore_` flag to determine whether underscores in option names should be ignored during option parsing.
- **Inputs**:
    - `value`: A boolean value indicating whether underscores should be ignored (default is true).
- **Control Flow**:
    - The method assigns the input `value` to the `ignore_underscore_` member variable.
    - The method returns a pointer to the current `OptionDefaults` object (`this`).
- **Output**: A pointer to the current `OptionDefaults` object, allowing for method chaining.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)


---
#### OptionDefaults::disable\_flag\_override<!-- {{#callable:CLI::OptionDefaults::disable_flag_override}} -->
The `disable_flag_override` function sets the `disable_flag_override_` member variable to the specified boolean value, which controls whether flag values can be overridden with an '=<value>' segment.
- **Inputs**:
    - `value`: A boolean value that determines whether flag overriding is disabled; defaults to true.
- **Control Flow**:
    - The function assigns the input boolean value to the `disable_flag_override_` member variable.
    - The function returns a pointer to the current `OptionDefaults` object.
- **Output**: A pointer to the current `OptionDefaults` object, allowing for method chaining.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)


---
#### OptionDefaults::delimiter<!-- {{#callable:CLI::OptionDefaults::delimiter}} -->
The `delimiter` function sets a character to be used as a delimiter for splitting single arguments into multiple inputs in the `OptionDefaults` class.
- **Inputs**:
    - `value`: A character that specifies the delimiter to be used for splitting arguments; defaults to '\0' if not provided.
- **Control Flow**:
    - The function assigns the input character `value` to the member variable `delimiter_`.
    - The function returns a pointer to the current instance of `OptionDefaults`.
- **Output**: A pointer to the current instance of `OptionDefaults`, allowing for method chaining.
- **See also**: [`CLI::OptionDefaults`](#OptionDefaults)  (Data Structure)



---
### Option<!-- {{#data_structure:CLI::empty::Option}} -->
- **Type**: `class`
- **Members**:
    - `snames_`: A list of short option names without leading dashes.
    - `lnames_`: A list of long option names without leading dashes.
    - `default_flag_values_`: A list of flag names with their default values.
    - `fnames_`: A list of flag names with specified default values.
    - `pname_`: A positional name for the option.
    - `envname_`: The environment variable name associated with the option.
    - `description_`: The description for help strings.
    - `default_str_`: A human-readable default value string.
    - `option_text_`: Text that describes the option type and usage in help text.
    - `type_name_`: A lambda function returning a human-readable type value.
    - `default_function_`: A function to capture a default value.
    - `type_size_max_`: The maximum number of arguments that make up one option.
    - `type_size_min_`: The minimum number of arguments that make up one option.
    - `expected_min_`: The minimum number of expected values.
    - `expected_max_`: The maximum number of expected values.
    - `validators_`: A list of validators to run on each parsed value.
    - `needs_`: A set of options required with this option.
    - `excludes_`: A set of options excluded with this option.
    - `parent_`: A pointer to the parent App for fallthrough.
    - `callback_`: A callback function to execute for the option.
    - `results_`: Complete results of parsing.
    - `proc_results_`: Results after reduction.
    - `current_option_state_`: The current state of the option in the parsing process.
    - `allow_extra_args_`: Flag to allow extra arguments beyond type_size_max.
    - `flag_like_`: Flag indicating the option should act like a flag.
    - `run_callback_for_default_`: Flag to control running the callback to set the default.
    - `inject_separator_`: Flag indicating a separator needs to be injected after each argument call.
    - `trigger_on_result_`: Flag indicating the option should trigger validation and callback on each result.
    - `force_callback_`: Flag indicating the option should force the callback regardless of results.
- **Description**: The `Option` class is a comprehensive data structure used to define and manage command-line options within an application. It extends the `OptionBase` class and is designed to handle various aspects of option parsing, including short and long names, default values, environment variable checks, and help descriptions. The class supports complex configurations such as validators, dependencies, exclusions, and callback functions to process parsed results. It also maintains state information about the parsing process and provides mechanisms to handle extra arguments, flags, and default value settings. The `Option` class is integral to the CLI11 library, facilitating robust command-line interface creation.
- **Member Functions**:
    - [`CLI::empty::Option::Option`](#OptionOption)
    - [`CLI::empty::Option::Option`](#OptionOption)
    - [`CLI::empty::Option::operator=`](#Optionoperator)
- **Inherits From**:
    - [`CLI::OptionBase`](#OptionBase)

**Methods**

---
#### Option::Option<!-- {{#callable:CLI::empty::Option::Option}} -->
The `Option` constructor initializes an `Option` object with a name, description, callback, parent application, and an optional flag for allowing non-standard names.
- **Inputs**:
    - `option_name`: A string representing the name of the option, which can include both short and long names.
    - `option_description`: A string providing a description of the option, used for help text.
    - `callback`: A callback function of type `callback_t` that is executed when the option is processed.
    - `parent`: A pointer to the parent `App` object that this option is associated with.
    - `allow_non_standard`: A boolean flag indicating whether non-standard option names are allowed, defaulting to false.
- **Control Flow**:
    - The constructor initializes the `description_`, `parent_`, and `callback_` member variables with the provided arguments.
    - It uses `std::move` to efficiently transfer ownership of `option_description` and `callback` to the member variables.
    - The `detail::split_names` function is called with `option_name` to split it into its constituent parts.
    - The `detail::get_names` function is then called with the split names and the `allow_non_standard` flag to populate the `snames_`, `lnames_`, and `pname_` member variables.
- **Output**: The constructor does not return a value; it initializes an `Option` object.
- **See also**: [`CLI::empty::Option`](#Option)  (Data Structure)


---
#### Option::Option<!-- {{#callable:CLI::empty::Option::Option}} -->
The `Option` constructor is deleted to prevent copying and assignment of `Option` objects.
- **Inputs**: None
- **Control Flow**:
    - The constructor `Option(const Option &) = delete;` is defined to delete the copy constructor, preventing the creation of a new `Option` object as a copy of an existing one.
    - The assignment operator `Option &operator=(const Option &) = delete;` is defined to delete the assignment operator, preventing the assignment of one `Option` object to another.
- **Output**: There is no output as this is a constructor and assignment operator deletion.
- **See also**: [`CLI::empty::Option`](#Option)  (Data Structure)


---
#### Option::operator=<!-- {{#callable:CLI::empty::Option::operator=}} -->
The assignment operator for the `Option` class is deleted, preventing assignment of `Option` objects.
- **Inputs**: None
- **Control Flow**:
    - The function is defined as a deleted function, meaning it cannot be used or called.
    - This prevents the assignment of one `Option` object to another, ensuring that `Option` objects are not accidentally copied or assigned.
- **Output**: There is no output as the function is deleted and cannot be used.
- **See also**: [`CLI::empty::Option`](#Option)  (Data Structure)



---
### option\_state<!-- {{#data_structure:CLI::empty::Option::option_state}} -->
- **Type**: `enum`
- **Members**:
    - `parsing`: The option is currently collecting parsed results.
    - `validated`: The results have been validated.
    - `reduced`: A subset of results has been generated.
    - `callback_run`: The callback has been executed.
- **Description**: The `option_state` enum class represents the different states an option can be in during its lifecycle in the parsing process. It is used to track the progress of an option from the initial parsing stage, through validation and reduction, to the execution of a callback function. Each state is associated with a specific character value, indicating its position in the sequence of operations.


# Functions

---
### empty<!-- {{#callable:CLI::empty}} -->
The `empty` method checks if any results have been parsed for the option.
- **Inputs**:
    - `none`: This method does not take any input arguments.
- **Control Flow**:
    - The method checks the size of the `results_` vector.
    - It returns true if the vector is empty, indicating that the option was not passed.
- **Output**: The method returns a boolean value: true if no results were parsed, and false otherwise.


---
### clear<!-- {{#callable:CLI::clear}} -->
Clears the parsed results and resets the current option state to parsing.
- **Inputs**: None
- **Control Flow**:
    - Calls `results_.clear()` to remove all parsed results.
    - Sets `current_option_state_` to `option_state::parsing` to indicate that the option is ready to collect new results.
- **Output**: The function does not return a value; it modifies the internal state of the `Option` object.


---
### allow\_extra\_args<!-- {{#callable:CLI::allow_extra_args}} -->
Sets the `allow_extra_args_` flag to indicate whether extra arguments are permitted.
- **Inputs**:
    - `value`: A boolean flag indicating whether to allow extra arguments; defaults to true.
- **Control Flow**:
    - The function sets the member variable `allow_extra_args_` to the value of the input parameter `value`.
    - It then returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the current instance of the `Option` class, allowing for method chaining.


---
### get\_allow\_extra\_args<!-- {{#callable:CLI::get_allow_extra_args}} -->
Retrieves the current setting of the `allow_extra_args_` flag.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `allow_extra_args_`.
- **Output**: Returns a boolean indicating whether extra arguments are allowed for the option.


---
### trigger\_on\_parse<!-- {{#callable:CLI::trigger_on_parse}} -->
Sets the `trigger_on_result_` flag to the specified boolean value and returns the current `Option` instance.
- **Inputs**:
    - `value`: A boolean value that determines whether the trigger on parse should be enabled (default is true).
- **Control Flow**:
    - The function assigns the input boolean `value` to the member variable `trigger_on_result_`.
    - It then returns the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` instance, allowing for method chaining.


---
### get\_trigger\_on\_parse<!-- {{#callable:CLI::get_trigger_on_parse}} -->
The `get_trigger_on_parse` function retrieves the current state of the `trigger_on_result_` flag.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the member variable `trigger_on_result_`.
- **Output**: The function returns a boolean value indicating whether the option should trigger a callback on parsing.


---
### force\_callback<!-- {{#callable:CLI::force_callback}} -->
Sets the `force_callback_` flag to the specified boolean value and returns a pointer to the current `Option` instance.
- **Inputs**:
    - `value`: A boolean flag that determines whether to force the callback execution; defaults to true.
- **Control Flow**:
    - The function sets the member variable `force_callback_` to the value of the input parameter `value`.
    - It then returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` instance, allowing for method chaining.


---
### get\_force\_callback<!-- {{#callable:CLI::get_force_callback}} -->
The `get_force_callback` function retrieves the current value of the `force_callback_` member variable.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the private member variable `force_callback_`.
    - It returns the value of `force_callback_` without any additional logic or conditions.
- **Output**: The function returns a boolean value indicating whether the callback should be forced.


---
### run\_callback\_for\_default<!-- {{#callable:CLI::run_callback_for_default}} -->
Sets the `run_callback_for_default_` flag to control whether the callback function should be executed to set the default value.
- **Inputs**:
    - `value`: A boolean flag that determines whether the callback for default values should be run; defaults to true.
- **Control Flow**:
    - The function assigns the input boolean `value` to the member variable `run_callback_for_default_`.
    - It then returns a pointer to the current instance of the class (using `this`).
- **Output**: Returns a pointer to the current instance of the class (`this`), allowing for method chaining.


---
### get\_run\_callback\_for\_default<!-- {{#callable:CLI::get_run_callback_for_default}} -->
Retrieves the value of the `run_callback_for_default_` member variable.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the private member variable `run_callback_for_default_`.
    - It returns the boolean value of `run_callback_for_default_` without any additional logic.
- **Output**: Returns a boolean indicating whether the callback for default values should be run.


---
### needs<!-- {{#callable:CLI::needs}} -->
The [`needs`](#needs) function registers multiple dependencies for an `Option` object, ensuring that specified options must be present.
- **Inputs**:
    - `opt`: The first option that is required.
    - `opt1`: The second option that is required.
    - `args`: Additional options that are required, allowing for a variable number of arguments.
- **Control Flow**:
    - The function first calls [`needs`](#needs) with the first option `opt` to register it as a dependency.
    - Then, it recursively calls [`needs`](#needs) with the second option `opt1` and any additional arguments `args...` to register them as dependencies.
- **Output**: Returns a pointer to the `Option` object, allowing for method chaining.
- **Functions called**:
    - [`CLI::needs`](#needs)


---
### excludes<!-- {{#callable:CLI::excludes}} -->
The [`excludes`](impl/Option_inl.hpp.driver.md#Optionexcludes) function adds multiple options to the exclusion list of an `Option`.
- **Inputs**:
    - `A opt`: The first option to be excluded.
    - `B opt1`: The second option to be excluded.
    - `ARG... args`: Additional options to be excluded, allowing for a variable number of arguments.
- **Control Flow**:
    - The function first calls [`excludes`](impl/Option_inl.hpp.driver.md#Optionexcludes) with the first argument `opt` to add it to the exclusion list.
    - Then, it recursively calls [`excludes`](impl/Option_inl.hpp.driver.md#Optionexcludes) with the second argument `opt1` and any additional arguments `args...` to continue adding to the exclusion list.
- **Output**: The function returns a pointer to the `Option` instance after adding all specified options to the exclusion list.
- **Functions called**:
    - [`CLI::Option::excludes`](impl/Option_inl.hpp.driver.md#Optionexcludes)


---
### envname<!-- {{#callable:CLI::envname}} -->
Sets the environment variable name for an option.
- **Inputs**:
    - `name`: A `std::string` representing the name of the environment variable to associate with the option.
- **Control Flow**:
    - The function takes a string input and moves it into the member variable `envname_`.
    - It returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` instance, allowing for method chaining.


---
### disable\_flag\_override<!-- {{#callable:CLI::disable_flag_override}} -->
Sets the `disable_flag_override_` member variable to the specified boolean value and returns a pointer to the current instance.
- **Inputs**:
    - `value`: A boolean value that determines whether flag value overriding is disabled; defaults to true.
- **Control Flow**:
    - The function sets the member variable `disable_flag_override_` to the value of the input parameter `value`.
    - It then returns a pointer to the current instance of the class.
- **Output**: Returns a pointer to the current instance of the class, allowing for method chaining.


---
### get\_type\_size<!-- {{#callable:CLI::get_type_size}} -->
The `get_type_size` function returns the minimum number of arguments expected for an option.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly accesses the member variable `type_size_min_`.
    - It returns the value of `type_size_min_` without any additional processing.
- **Output**: The output is an integer representing the minimum number of arguments that the option expects.


---
### get\_type\_size\_min<!-- {{#callable:CLI::get_type_size_min}} -->
The `get_type_size_min` function retrieves the minimum number of arguments expected by an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `type_size_min_`.
    - It returns the value of `type_size_min_` without any additional logic or conditions.
- **Output**: The function returns an integer representing the minimum number of arguments that the option expects.


---
### get\_type\_size\_max<!-- {{#callable:CLI::get_type_size_max}} -->
Returns the maximum size of the type expected by the option.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `type_size_max_`.
    - It returns the value of `type_size_max_` without any additional logic or conditions.
- **Output**: An integer representing the maximum size of the type expected by the option.


---
### get\_inject\_separator<!-- {{#callable:CLI::get_inject_separator}} -->
The `get_inject_separator` function retrieves the value of the `inject_separator_` flag.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the private member variable `inject_separator_`.
    - It returns the boolean value of `inject_separator_` without any additional logic or conditions.
- **Output**: The function returns a boolean indicating whether the separator injection is enabled (true) or not (false).


---
### get\_envname<!-- {{#callable:CLI::std::string::get_envname}} -->
Retrieves the environment variable name associated with the option.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the value of the member variable `envname_`.
- **Output**: Returns a `std::string` representing the environment variable name associated with the option.


---
### get\_needs<!-- {{#callable:CLI::std::set<Option *>::get_needs}} -->
The `get_needs` function retrieves a set of options that are required by the current option.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the `needs_` member variable, which is a set of pointers to `Option` objects.
- **Output**: The output is a `std::set<Option *>` containing pointers to the options that are required by the current option.


---
### get\_excludes<!-- {{#callable:CLI::std::set<Option *>::get_excludes}} -->
The `get_excludes` function retrieves the set of options that are excluded from the current option.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `excludes_`, which is a set of pointers to `Option` objects.
    - It returns the current state of the `excludes_` set without any modifications.
- **Output**: The output is a `std::set<Option *>` containing pointers to the options that are excluded from the current option.


---
### get\_default\_str<!-- {{#callable:CLI::std::string::get_default_str}} -->
Retrieves the default string representation of an option.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the member variable `default_str_` and returns its value.
- **Output**: Returns a `std::string` that represents the default value of the option.


---
### get\_callback<!-- {{#callable:CLI::get_callback}} -->
The `get_callback` function retrieves the stored callback function associated with an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `callback_` of the class instance.
    - It returns the value of `callback_` without any additional processing or conditions.
- **Output**: The function returns a `callback_t`, which is a `std::function` that takes a `const results_t&` and returns a `bool`, representing the callback function associated with the option.


---
### get\_lnames<!-- {{#callable:CLI::std::get_lnames}} -->
Returns a constant reference to the vector of long names associated with the option.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the member variable `lnames_` which is a vector of strings.
- **Output**: A constant reference to a vector of strings containing the long names of the option.


---
### get\_snames<!-- {{#callable:CLI::std::get_snames}} -->
The `get_snames` function returns a constant reference to the vector of short names associated with an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `snames_` which holds the short names.
    - It returns a constant reference to `snames_`, ensuring that the original data cannot be modified.
- **Output**: The output is a constant reference to a `std::vector<std::string>`, which contains the short names of the option.


---
### get\_fnames<!-- {{#callable:CLI::std::get_fnames}} -->
The `get_fnames` function retrieves a constant reference to the vector of flag names associated with an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly returns the member variable `fnames_`, which is a vector of strings.
- **Output**: The output is a constant reference to a vector of strings containing the flag names associated with the option.


---
### get\_single\_name<!-- {{#callable:CLI::get_single_name}} -->
Retrieves the first available name from a list of option names.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - Checks if the `lnames_` vector is not empty and returns the first element if true.
    - If `lnames_` is empty, checks if the `snames_` vector is not empty and returns the first element if true.
    - If both `lnames_` and `snames_` are empty, checks if `pname_` is not empty and returns it if true.
    - If all previous checks fail, returns the `envname_` string.
- **Output**: Returns a constant reference to a string representing the first available name from the option's names.


---
### get\_expected<!-- {{#callable:CLI::get_expected}} -->
The `get_expected` function retrieves the minimum number of expected values for an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `expected_min_`.
    - It returns the value of `expected_min_` without any additional logic or conditions.
- **Output**: The function returns an integer representing the minimum number of expected values for the option.


---
### get\_expected\_min<!-- {{#callable:CLI::get_expected_min}} -->
Retrieves the minimum number of expected values for an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `expected_min_`.
    - No conditional logic or loops are present; it simply returns the value of `expected_min_`.
- **Output**: Returns an integer representing the minimum number of expected values for the option.


---
### get\_expected\_max<!-- {{#callable:CLI::get_expected_max}} -->
The `get_expected_max` function retrieves the maximum number of expected values for an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function directly accesses the member variable `expected_max_` of the class instance.
    - It returns the value of `expected_max_` without any additional logic or conditions.
- **Output**: The function returns an integer representing the maximum number of expected values for the option.


---
### get\_items\_expected\_min<!-- {{#callable:CLI::get_items_expected_min}} -->
Calculates the minimum number of items expected based on type size and expected minimum.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly computes the product of `type_size_min_` and `expected_min_`.
    - No conditional statements or loops are present in the function.
- **Output**: Returns an integer representing the minimum number of items expected.


---
### get\_items\_expected\_max<!-- {{#callable:CLI::get_items_expected_max}} -->
Calculates the maximum number of items expected based on type size and expected maximum.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function initializes a local variable `t` with the value of `type_size_max_`.
    - It then calls `detail::checked_multiply` with `t` and `expected_max_` to check if the multiplication is valid.
    - If the multiplication is valid, it returns `t`; otherwise, it returns `detail::expected_max_vector_size`.
- **Output**: Returns an integer representing the maximum number of items expected, either the calculated value or a predefined maximum size.


---
### get\_items\_expected<!-- {{#callable:CLI::get_items_expected}} -->
The `get_items_expected` function returns the minimum number of expected items for an option.
- **Inputs**: None
- **Control Flow**:
    - The function directly calls another function, `get_items_expected_min()`, to retrieve the minimum expected items.
- **Output**: The output is an integer representing the minimum number of expected items.
- **Functions called**:
    - [`CLI::get_items_expected_min`](#get_items_expected_min)


---
### get\_positional<!-- {{#callable:CLI::get_positional}} -->
The `get_positional` function checks if the positional name of an option is set.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, allowing access to its member variables.
- **Control Flow**:
    - The function evaluates the `pname_` member variable to determine if it is empty.
    - It returns `true` if `pname_` is not empty, indicating that a positional name is set, otherwise it returns `false`.
- **Output**: The function returns a boolean value indicating whether the positional name is set (true) or not (false).


---
### nonpositional<!-- {{#callable:CLI::nonpositional}} -->
The `nonpositional` function checks if there are any non-positional names defined for an option.
- **Inputs**:
    - `this`: A constant reference to the current instance of the class, used to access member variables.
- **Control Flow**:
    - The function evaluates the condition of whether the `lnames_` vector (long names) is not empty or the `snames_` vector (short names) is not empty.
    - If either vector contains elements, the function returns true, indicating that there are non-positional names defined.
- **Output**: The function returns a boolean value: true if there are non-positional names defined, otherwise false.


---
### has\_description<!-- {{#callable:CLI::has_description}} -->
Checks if the `description_` member variable of the `Option` class is non-empty.
- **Inputs**:
    - `this`: A constant reference to the current instance of the `Option` class.
- **Control Flow**:
    - The function evaluates the condition of whether the `description_` string is empty.
    - It returns the negation of the result of the `empty()` method called on `description_`.
- **Output**: Returns a boolean value indicating whether the `description_` is non-empty.


---
### get\_description<!-- {{#callable:CLI::get_description}} -->
Returns a constant reference to the description of the option.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function directly returns the member variable `description_`.
    - No conditional logic or loops are present in this function.
- **Output**: Returns a constant reference to a `std::string` that contains the description of the option.


---
### description<!-- {{#callable:CLI::description}} -->
Sets the description of an `Option` and returns a pointer to the `Option` instance.
- **Inputs**:
    - `option_description`: A `std::string` representing the description to be assigned to the `Option`.
- **Control Flow**:
    - The function takes the input string `option_description` and moves its content into the member variable `description_`.
    - It then returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the `Option` instance, allowing for method chaining.


---
### option\_text<!-- {{#callable:CLI::option_text}} -->
Sets the text description for an `Option` and returns a pointer to the current `Option` instance.
- **Inputs**:
    - `text`: A `std::string` representing the text description to be set for the `Option`.
- **Control Flow**:
    - The function takes the input string `text` and moves its content into the member variable `option_text_`.
    - It then returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` instance, allowing for method chaining.


---
### get\_option\_text<!-- {{#callable:CLI::get_option_text}} -->
The `get_option_text` function returns a constant reference to the `option_text_` member variable.
- **Inputs**: None
- **Control Flow**:
    - The function directly accesses the `option_text_` member variable.
    - It returns the value without any modification or additional logic.
- **Output**: The output is a constant reference to a `std::string` that contains the text associated with the option.


---
### operator==<!-- {{#callable:CLI::operator==}} -->
Compares two `Option` objects for equality based on shared names.
- **Inputs**:
    - `other`: An `Option` object to compare against the current instance.
- **Control Flow**:
    - Calls the [`matching_name`](impl/Option_inl.hpp.driver.md#Optionmatching_name) method to find any common names between the current `Option` and the `other` `Option`.
    - Checks if the result of [`matching_name`](impl/Option_inl.hpp.driver.md#Optionmatching_name) is not empty to determine equality.
- **Output**: Returns a boolean value indicating whether the two `Option` objects are considered equal.
- **Functions called**:
    - [`CLI::Option::matching_name`](impl/Option_inl.hpp.driver.md#Optionmatching_name)


---
### check\_sname<!-- {{#callable:CLI::check_sname}} -->
Checks if a given short name exists in the list of short names.
- **Inputs**:
    - `name`: A `std::string` representing the short name to check against the list of short names.
- **Control Flow**:
    - The function uses `std::move` to efficiently transfer the `name` string into the `detail::find_member` function.
    - It calls `detail::find_member`, passing the moved `name`, the list of short names (`snames_`), and the `ignore_case_` flag.
    - The result of `find_member` is checked to see if it is greater than or equal to 0, indicating that the name exists.
- **Output**: Returns a boolean value indicating whether the short name exists in the list of short names.


---
### check\_lname<!-- {{#callable:CLI::check_lname}} -->
The `check_lname` function checks if a given long name exists in the list of long names.
- **Inputs**:
    - `name`: A `std::string` representing the long name to be checked.
- **Control Flow**:
    - The function calls `detail::find_member` with the provided `name`, moving it to avoid unnecessary copies.
    - It checks if the result of `find_member` is greater than or equal to 0, indicating that the name was found in the `lnames_` vector.
- **Output**: Returns a boolean value indicating whether the long name exists in the `lnames_` vector.


---
### check\_fname<!-- {{#callable:CLI::check_fname}} -->
Checks if a given filename exists in the list of valid filenames.
- **Inputs**:
    - `name`: A `std::string` representing the filename to check against the list of valid filenames.
- **Control Flow**:
    - The function first checks if the `fnames_` vector is empty; if it is, the function returns false.
    - If `fnames_` is not empty, it calls `detail::find_member` with the provided `name`, moving it to avoid unnecessary copies, and checks if the result is greater than or equal to 0, indicating a match.
- **Output**: Returns a boolean value: true if the filename exists in the list, false otherwise.


---
### results<!-- {{#callable:CLI::results}} -->
The `results` function retrieves and converts the results of an option into a specified output type.
- **Inputs**:
    - `output`: A reference to a variable of type T where the results will be stored after conversion.
- **Control Flow**:
    - The function first checks if the current option state is 'reduced' or if there is only one result with no validators.
    - If the above condition is true, it assigns either the processed results or the original results to a local variable `res`.
    - If the results are empty, it checks if a default string is provided; if so, it adds this default string to the results and validates them.
    - If there are results, it retrieves the reduced results.
    - The function then attempts to convert the results to the specified output type using `detail::lexical_conversion`.
    - If the conversion fails, it throws a [`ConversionError`](Error.hpp.driver.md#ConversionErrorConversionError) with the name of the option and the results.
- **Output**: The function does not return a value directly; instead, it populates the `output` reference with the converted results or throws an error if the conversion fails.
- **Functions called**:
    - [`CLI::Option::_add_result`](impl/Option_inl.hpp.driver.md#Option_add_result)
    - [`CLI::Option::_validate_results`](impl/Option_inl.hpp.driver.md#Option_validate_results)
    - [`CLI::Option::_reduce_results`](impl/Option_inl.hpp.driver.md#Option_reduce_results)
    - [`CLI::CLI11_INLINE::reduced_results`](impl/Option_inl.hpp.driver.md#11_INLINEreduced_results)
    - [`ConversionError::ConversionError`](Error.hpp.driver.md#ConversionErrorConversionError)
    - [`CLI::get_name`](Validators.hpp.driver.md#get_name)


---
### as<!-- {{#callable:CLI::as}} -->
Converts the results of an option into a specified type.
- **Inputs**:
    - `T`: The type to which the results will be converted.
- **Control Flow**:
    - Declares a variable `output` of type `T`.
    - Calls the [`results`](#results) method with `output` as an argument to populate it with the parsed results.
    - Returns the populated `output` variable.
- **Output**: Returns an object of type `T` that contains the converted results from the option.
- **Functions called**:
    - [`CLI::results`](#results)


---
### get\_callback\_run<!-- {{#callable:CLI::get_callback_run}} -->
Checks if the current option state indicates that the callback has been executed.
- **Inputs**:
    - `none`: This function does not take any input arguments.
- **Control Flow**:
    - The function evaluates the `current_option_state_` member variable.
    - It compares `current_option_state_` with the `option_state::callback_run` enumeration value.
    - The result of the comparison determines the return value.
- **Output**: Returns a boolean value indicating whether the callback has been run (true) or not (false).


---
### type\_name\_fn<!-- {{#callable:CLI::type_name_fn}} -->
Sets a function to determine the type name of an option.
- **Inputs**:
    - `typefun`: A `std::function` that returns a `std::string`, representing the function to determine the type name.
- **Control Flow**:
    - The function takes the input `typefun` and moves it into the member variable `type_name_`.
    - It returns a pointer to the current instance of the `Option` class.
- **Output**: Returns a pointer to the current instance of the `Option` class.


---
### type\_name<!-- {{#callable:CLI::type_name}} -->
The `type_name` function sets a custom type name for an option using a provided string.
- **Inputs**:
    - `typeval`: A string representing the custom type name to be set for the option.
- **Control Flow**:
    - The function calls [`type_name_fn`](#type_name_fn) with a lambda that captures `typeval` and returns it.
    - The function then returns the current instance of the `Option` class.
- **Output**: Returns a pointer to the current `Option` instance.
- **Functions called**:
    - [`CLI::type_name_fn`](#type_name_fn)


---
### inject\_separator<!-- {{#callable:CLI::inject_separator}} -->
Sets the `inject_separator_` flag to control whether a separator should be injected after each argument.
- **Inputs**:
    - `value`: A boolean flag that determines whether to enable or disable the injection of a separator; defaults to true.
- **Control Flow**:
    - The function directly assigns the input boolean value to the member variable `inject_separator_`.
- **Output**: This function does not return a value; it modifies the internal state of the object by setting the `inject_separator_` flag.


---
### default\_function<!-- {{#callable:CLI::default_function}} -->
Sets a default function for an `Option` object.
- **Inputs**:
    - `func`: A callable object (function or lambda) that returns a `std::string`.
- **Control Flow**:
    - The function assigns the provided callable `func` to the member variable `default_function_`.
    - It then returns a pointer to the current `Option` object.
- **Output**: Returns a pointer to the current `Option` instance.


---
### capture\_default\_str<!-- {{#callable:CLI::capture_default_str}} -->
Captures a default string value by invoking a callback function if it is defined.
- **Inputs**:
    - `this`: A pointer to the current instance of the `Option` class.
- **Control Flow**:
    - Checks if the `default_function_` member is set (not null).
    - If `default_function_` is set, it calls the function and assigns the returned value to `default_str_`.
- **Output**: Returns a pointer to the current instance of the `Option` class.


---
### default\_str<!-- {{#callable:CLI::default_str}} -->
Sets the default string value for an option and returns a pointer to the current `Option` instance.
- **Inputs**:
    - `val`: A `std::string` representing the default value to be set for the option.
- **Control Flow**:
    - The function uses `std::move` to transfer the contents of `val` into the member variable `default_str_`, which stores the default string value.
    - It then returns a pointer to the current instance of the `Option` class, allowing for method chaining.
- **Output**: Returns a pointer to the current `Option` instance, enabling further configuration through method chaining.


---
### default\_val<!-- {{#callable:CLI::default_val}} -->
Sets a default value for an option and validates it.
- **Inputs**:
    - `val`: The value to be set as the default, which can be of any type.
- **Control Flow**:
    - Converts the input value `val` to a string representation using `detail::to_string`.
    - Stores the current state of the option and clears previous results.
    - Attempts to add the string representation of the value to the results.
    - If `run_callback_for_default_` is true and `trigger_on_result_` is false, it runs the callback function.
    - If the callback is not run, it validates the results.
    - If any exceptions occur during the process, it restores the previous state and results, and throws an error.
- **Output**: Returns a pointer to the current `Option` instance.
- **Functions called**:
    - [`CLI::Option::add_result`](impl/Option_inl.hpp.driver.md#Optionadd_result)
    - [`CLI::Option::run_callback`](impl/Option_inl.hpp.driver.md#Optionrun_callback)
    - [`CLI::Option::_validate_results`](impl/Option_inl.hpp.driver.md#Option_validate_results)
    - [`ConversionError::ConversionError`](Error.hpp.driver.md#ConversionErrorConversionError)
    - [`CLI::get_name`](Validators.hpp.driver.md#get_name)


