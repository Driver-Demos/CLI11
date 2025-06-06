# Purpose
This C++ header file is part of the CLI11 library, which is designed to facilitate command-line interface (CLI) parsing. The file primarily defines a comprehensive set of error classes that are used to handle various exceptions and errors that may occur during the construction and parsing of command-line arguments. These error classes are organized hierarchically, with a base class [`Error`](#ErrorError) from which more specific error types inherit. The file includes definitions for errors related to incorrect construction, parsing issues, and specific command-line argument errors, such as `IncorrectConstruction`, `BadNameString`, [`OptionAlreadyAdded`](#OptionAlreadyAddedOptionAlreadyAdded), `FileError`, [`ConversionError`](#ConversionErrorConversionError), [`ValidationError`](#ValidationErrorValidationError), and others. Each error class is associated with an `ExitCodes` enumeration, which provides standardized exit codes for different error scenarios.

The file is structured to provide a robust error-handling mechanism for the CLI11 library, ensuring that users can effectively manage and respond to various command-line parsing errors. It includes macros to simplify the definition of error classes and constructors, allowing for consistent error message formatting and exit code assignment. The file is intended to be included in other parts of the CLI11 library, as indicated by the `#pragma once` directive and the inclusion of other library-specific headers like "Macros.hpp" and "StringTools.hpp". This header file does not define a public API directly but rather supports the internal workings of the CLI11 library by providing a standardized way to handle errors and exceptions.
# Imports and Dependencies

---
- `exception`
- `stdexcept`
- `string`
- `utility`
- `vector`
- `Macros.hpp`
- `StringTools.hpp`


# Data Structures

---
### ExitCodes<!-- {{#data_structure:ExitCodes}} -->
- **Type**: `enum`
- **Members**:
    - `Success`: Indicates successful completion with an exit code of 0.
    - `IncorrectConstruction`: Represents an error due to incorrect construction with an exit code of 100.
    - `BadNameString`: Indicates an error related to a bad name string.
    - `OptionAlreadyAdded`: Represents an error when an option is added more than once.
    - `FileError`: Indicates an error related to file operations.
    - `ConversionError`: Represents an error during data conversion.
    - `ValidationError`: Indicates an error during validation.
    - `RequiredError`: Represents an error when a required option is missing.
    - `RequiresError`: Indicates an error when a required option is not present.
    - `ExcludesError`: Represents an error when an excluded option is present.
    - `ExtrasError`: Indicates an error due to extra unexpected arguments.
    - `ConfigError`: Represents an error related to configuration.
    - `InvalidError`: Indicates an error due to invalid input or state.
    - `HorribleError`: Represents a severe error that should not occur.
    - `OptionNotFound`: Indicates an error when an option is not found.
    - `ArgumentMismatch`: Represents an error due to mismatched arguments.
    - `BaseClass`: Serves as a base class with an exit code of 127.
- **Description**: The `ExitCodes` enum class defines a set of integer-based exit codes used to represent various error and success states within the CLI library. Each enumerator corresponds to a specific type of error or success condition, such as `Success` for successful completion, `IncorrectConstruction` for construction errors, and `FileError` for file-related issues. These codes are integral to error handling in the library, allowing for consistent and clear communication of error states.


---
### Error<!-- {{#data_structure:Error}} -->
- **Type**: `class`
- **Members**:
    - `actual_exit_code`: Stores the exit code associated with the error.
    - `error_name`: Holds the name of the error as a string.
- **Description**: The `Error` class is a custom exception type that extends `std::runtime_error` to represent errors in the CLI11 library. It encapsulates an error name and an exit code, providing methods to retrieve these values. The class is designed to be the base class for more specific error types within the library, allowing for structured error handling and reporting.
- **Member Functions**:
    - [`Error::get_exit_code`](#Errorget_exit_code)
    - [`Error::Error`](#ErrorError)
- **Inherits From**:
    - `std::runtime_error`

**Methods**

---
#### Error::get\_exit\_code<!-- {{#callable:Error::get_exit_code}} -->
The `get_exit_code` function returns the exit code associated with an `Error` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `actual_exit_code` member variable of the `Error` class.
- **Output**: An integer representing the exit code of the error.
- **See also**: [`Error`](#Error)  (Data Structure)


---
#### Error::Error<!-- {{#callable:Error::Error}} -->
The `Error` constructor initializes an error object with a name, message, and exit code, either as an integer or an `ExitCodes` enum.
- **Inputs**:
    - `name`: A string representing the name of the error.
    - `msg`: A string containing the error message.
    - `exit_code`: An `ExitCodes` enum value representing the exit code for the error.
- **Control Flow**:
    - The constructor is called with a name, message, and an `ExitCodes` enum value.
    - The `ExitCodes` enum value is cast to an integer and passed to another `Error` constructor.
    - The other `Error` constructor initializes the base `runtime_error` with the message, sets the `actual_exit_code` to the integer exit code, and assigns the `error_name` to the provided name.
- **Output**: An `Error` object initialized with the specified name, message, and exit code.
- **See also**: [`Error`](#Error)  (Data Structure)



---
### IncorrectConstruction<!-- {{#data_structure:IncorrectConstruction}} -->
- **Type**: `class`
- **Description**: The `IncorrectConstruction` class is a specialized error class derived from `ConstructionError`, which itself inherits from the `Error` class. It is used to represent various construction-related errors in the CLI11 library, specifically when options are set to conflicting values or when certain constraints are violated during the construction of command-line options. The class provides several static methods to create specific error messages for different types of incorrect constructions, such as positional flags, setting zero expected options, and changing expected arguments for non-vector options.
- **Member Functions**:
    - [`IncorrectConstruction::PositionalFlag`](#IncorrectConstructionPositionalFlag)
    - [`IncorrectConstruction::Set0Opt`](#IncorrectConstructionSet0Opt)
    - [`IncorrectConstruction::SetFlag`](#IncorrectConstructionSetFlag)
    - [`IncorrectConstruction::ChangeNotVector`](#IncorrectConstructionChangeNotVector)
    - [`IncorrectConstruction::AfterMultiOpt`](#IncorrectConstructionAfterMultiOpt)
    - [`IncorrectConstruction::MissingOption`](#IncorrectConstructionMissingOption)
    - [`IncorrectConstruction::MultiOptionPolicy`](#IncorrectConstructionMultiOptionPolicy)
- **Inherits From**:
    - `ConstructionError`

**Methods**

---
#### IncorrectConstruction::PositionalFlag<!-- {{#callable:IncorrectConstruction::PositionalFlag}} -->
The `PositionalFlag` function creates an `IncorrectConstruction` error indicating that flags cannot be positional.
- **Inputs**:
    - `name`: A string representing the name of the flag that is incorrectly being used as positional.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the string ": Flags cannot be positional" to the `name`.
    - It returns an `IncorrectConstruction` object initialized with the concatenated string.
- **Output**: An `IncorrectConstruction` object with a message indicating the error of using a flag as positional.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::Set0Opt<!-- {{#callable:IncorrectConstruction::Set0Opt}} -->
The `Set0Opt` function creates an `IncorrectConstruction` error indicating that setting an expected value of 0 is not allowed and suggests using a flag instead.
- **Inputs**:
    - `name`: A string representing the name of the option or context in which the error occurred.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the `name` with a specific error message string ": Cannot set 0 expected, use a flag instead".
    - It returns an `IncorrectConstruction` object initialized with the concatenated error message.
- **Output**: An `IncorrectConstruction` object initialized with a specific error message.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::SetFlag<!-- {{#callable:IncorrectConstruction::SetFlag}} -->
The `SetFlag` function creates an `IncorrectConstruction` error indicating that an expected number cannot be set for flags.
- **Inputs**:
    - `name`: A string representing the name or identifier related to the error context.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the `name` with a specific error message string ": Cannot set an expected number for flags".
    - It returns an `IncorrectConstruction` object initialized with the concatenated error message.
- **Output**: An `IncorrectConstruction` object initialized with a specific error message related to setting an expected number for flags.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::ChangeNotVector<!-- {{#callable:IncorrectConstruction::ChangeNotVector}} -->
The `ChangeNotVector` function creates an `IncorrectConstruction` error indicating that only vector arguments can have their expected arguments changed.
- **Inputs**:
    - `name`: A string representing the name of the option or argument that caused the error.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the `name` with a specific error message indicating the restriction on changing expected arguments for non-vector types.
    - The function returns an `IncorrectConstruction` object initialized with the constructed error message.
- **Output**: An `IncorrectConstruction` object with a message indicating the error related to changing expected arguments for non-vector types.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::AfterMultiOpt<!-- {{#callable:IncorrectConstruction::AfterMultiOpt}} -->
The `AfterMultiOpt` function creates an `IncorrectConstruction` error indicating that expected arguments cannot be changed after modifying the multi-option policy.
- **Inputs**:
    - `name`: A string representing the name of the option or context in which the error occurred.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs an error message by appending a specific error description to the `name`.
    - The function returns an `IncorrectConstruction` object initialized with the constructed error message.
- **Output**: An `IncorrectConstruction` object with a message indicating the error related to changing expected arguments after altering the multi-option policy.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::MissingOption<!-- {{#callable:IncorrectConstruction::MissingOption}} -->
The `MissingOption` function creates an `IncorrectConstruction` error indicating that a specified option is not defined.
- **Inputs**:
    - `name`: A string representing the name of the option that is missing.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs an error message by concatenating the string 'Option ' with the `name` and the string ' is not defined'.
    - It returns an `IncorrectConstruction` object initialized with the constructed error message.
- **Output**: An `IncorrectConstruction` object with a message indicating the specified option is not defined.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)


---
#### IncorrectConstruction::MultiOptionPolicy<!-- {{#callable:IncorrectConstruction::MultiOptionPolicy}} -->
The `MultiOptionPolicy` function creates an `IncorrectConstruction` error indicating that the multi-option policy is only applicable to flags and exact value options.
- **Inputs**:
    - `name`: A string representing the name of the option or context in which the error occurred.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs an error message by appending a specific message to the `name`.
    - The function returns an `IncorrectConstruction` object initialized with the constructed error message.
- **Output**: An `IncorrectConstruction` object with a message indicating the misuse of multi-option policy.
- **See also**: [`IncorrectConstruction`](#IncorrectConstruction)  (Data Structure)



---
### BadNameString<!-- {{#data_structure:BadNameString}} -->
- **Type**: `class`
- **Description**: The `BadNameString` class is a specialized error class that inherits from `ConstructionError`, designed to handle specific naming errors in the CLI11 library. It provides several static methods to create instances of `BadNameString` with predefined error messages for various naming issues, such as invalid one-character names, missing dashes in long names, reserved names, and multiple positional names. This class is part of a hierarchy of error classes used to manage and report errors related to command-line interface construction and parsing.
- **Member Functions**:
    - [`BadNameString::OneCharName`](#BadNameStringOneCharName)
    - [`BadNameString::MissingDash`](#BadNameStringMissingDash)
    - [`BadNameString::BadLongName`](#BadNameStringBadLongName)
    - [`BadNameString::BadPositionalName`](#BadNameStringBadPositionalName)
    - [`BadNameString::ReservedName`](#BadNameStringReservedName)
    - [`BadNameString::MultiPositionalNames`](#BadNameStringMultiPositionalNames)
- **Inherits From**:
    - `ConstructionError`

**Methods**

---
#### BadNameString::OneCharName<!-- {{#callable:BadNameString::OneCharName}} -->
The `OneCharName` function constructs a `BadNameString` error message indicating an invalid single-character name.
- **Inputs**:
    - `name`: A string representing the name that is being checked for validity.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `BadNameString` object with a message indicating that the provided name is invalid because it is only one character long.
    - The constructed `BadNameString` object is returned.
- **Output**: A `BadNameString` object containing an error message about the invalid one-character name.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)


---
#### BadNameString::MissingDash<!-- {{#callable:BadNameString::MissingDash}} -->
The `MissingDash` function creates a `BadNameString` error indicating that a long name string requires two dashes.
- **Inputs**:
    - `name`: A string representing the name that is being checked for the required dashes.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `BadNameString` object with a message indicating the requirement for two dashes in long name strings, appending the provided `name` to the message.
    - The constructed `BadNameString` object is returned.
- **Output**: A `BadNameString` object containing an error message about the missing dashes in the provided name.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)


---
#### BadNameString::BadLongName<!-- {{#callable:BadNameString::BadLongName}} -->
The `BadLongName` function constructs a `BadNameString` object with a message indicating a bad long name error.
- **Inputs**:
    - `name`: A `std::string` representing the name that is considered a bad long name.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the string "Bad long name: " with the provided `name`.
    - It returns a new `BadNameString` object initialized with the concatenated message.
- **Output**: A `BadNameString` object containing the error message for a bad long name.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)


---
#### BadNameString::BadPositionalName<!-- {{#callable:BadNameString::BadPositionalName}} -->
The `BadPositionalName` function creates a `BadNameString` object with a message indicating an invalid positional name.
- **Inputs**:
    - `name`: A string representing the name that is considered invalid as a positional name.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `BadNameString` object with a message that includes the provided `name`.
    - The message is formatted as 'Invalid positional Name: ' followed by the `name`.
    - The constructed `BadNameString` object is returned.
- **Output**: A `BadNameString` object containing an error message about an invalid positional name.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)


---
#### BadNameString::ReservedName<!-- {{#callable:BadNameString::ReservedName}} -->
The `ReservedName` function generates a `BadNameString` error message indicating that certain option names are reserved and not allowed.
- **Inputs**:
    - `name`: A string representing the name that is being checked against reserved option names.
- **Control Flow**:
    - The function takes a single string input `name`.
    - It constructs a `BadNameString` object with a specific error message indicating that the names '-', '--', and '++' are reserved and not allowed as option names, appending the provided `name` to this message.
    - The constructed `BadNameString` object is returned.
- **Output**: A `BadNameString` object containing an error message about reserved option names.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)


---
#### BadNameString::MultiPositionalNames<!-- {{#callable:BadNameString::MultiPositionalNames}} -->
The `MultiPositionalNames` function creates a `BadNameString` error message indicating that only one positional name is allowed and suggests removing the provided name.
- **Inputs**:
    - `name`: A string representing the name that is causing the error due to multiple positional names being used.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `BadNameString` object with a specific error message concatenating the input `name`.
    - The constructed `BadNameString` object is returned.
- **Output**: A `BadNameString` object containing an error message about multiple positional names.
- **See also**: [`BadNameString`](#BadNameString)  (Data Structure)



---
### OptionAlreadyAdded<!-- {{#data_structure:OptionAlreadyAdded}} -->
- **Type**: `class`
- **Description**: The `OptionAlreadyAdded` class is a specialized error class derived from `ConstructionError`, used within the CLI11 library to indicate that an option has been added more than once. It provides constructors to create error messages indicating the specific option that was redundantly added, and includes static methods `Requires` and `Excludes` to generate error messages for options that have dependencies or exclusions with other options. This class is part of a hierarchy of error classes designed to handle various command-line interface construction and parsing errors.
- **Member Functions**:
    - [`OptionAlreadyAdded::OptionAlreadyAdded`](#OptionAlreadyAddedOptionAlreadyAdded)
    - [`OptionAlreadyAdded::Requires`](#OptionAlreadyAddedRequires)
    - [`OptionAlreadyAdded::Excludes`](#OptionAlreadyAddedExcludes)
- **Inherits From**:
    - `ConstructionError`

**Methods**

---
#### OptionAlreadyAdded::OptionAlreadyAdded<!-- {{#callable:OptionAlreadyAdded::OptionAlreadyAdded}} -->
The `OptionAlreadyAdded` constructor initializes an error indicating that an option has already been added, while the `Requires` static method creates an error indicating that one option requires another.
- **Inputs**:
    - `name`: A string representing the name of the option that is already added or requires another option.
    - `other`: A string representing the name of the other option that is required by the first option (only applicable for the `Requires` method).
- **Control Flow**:
    - The constructor `OptionAlreadyAdded` is called with a single string argument `name`, which is used to create an error message indicating that the option is already added.
    - The constructor calls another constructor of the same class with a message and an exit code `ExitCodes::OptionAlreadyAdded`.
    - The static method `Requires` takes two string arguments, `name` and `other`, and returns an `OptionAlreadyAdded` object with a message indicating that `name` requires `other`.
- **Output**: The constructor initializes an `OptionAlreadyAdded` object, and the `Requires` method returns an `OptionAlreadyAdded` object with a specific error message and exit code.
- **See also**: [`OptionAlreadyAdded`](#OptionAlreadyAdded)  (Data Structure)


---
#### OptionAlreadyAdded::Requires<!-- {{#callable:OptionAlreadyAdded::Requires}} -->
The `Requires` function creates an `OptionAlreadyAdded` error indicating that one option requires another.
- **Inputs**:
    - `name`: The name of the option that has a requirement.
    - `other`: The name of the option that is required by the first option.
- **Control Flow**:
    - The function takes two string arguments, `name` and `other`.
    - It constructs a string message in the format "<name> requires <other>".
    - It returns an `OptionAlreadyAdded` object initialized with the constructed message and the `ExitCodes::OptionAlreadyAdded` exit code.
- **Output**: An `OptionAlreadyAdded` object with a message indicating the requirement relationship between two options and an exit code of `OptionAlreadyAdded`.
- **See also**: [`OptionAlreadyAdded`](#OptionAlreadyAdded)  (Data Structure)


---
#### OptionAlreadyAdded::Excludes<!-- {{#callable:OptionAlreadyAdded::Excludes}} -->
The `Excludes` function creates an `OptionAlreadyAdded` error indicating that one option excludes another.
- **Inputs**:
    - `name`: A string representing the name of the option that is excluding another option.
    - `other`: A string representing the name of the option that is being excluded by the first option.
- **Control Flow**:
    - The function takes two string arguments, `name` and `other`.
    - It constructs a message in the format "<name> excludes <other>".
    - It returns an `OptionAlreadyAdded` object initialized with the constructed message and the `ExitCodes::OptionAlreadyAdded` exit code.
- **Output**: An `OptionAlreadyAdded` object with a message indicating exclusion and an exit code of `OptionAlreadyAdded`.
- **See also**: [`OptionAlreadyAdded`](#OptionAlreadyAdded)  (Data Structure)



---
### Success<!-- {{#data_structure:Success}} -->
- **Type**: `class`
- **Description**: The `Success` class is a specialized type of `ParseError` that represents a successful completion of a parsing operation in the CLI11 library. It is designed to be caught and handled to indicate that the parsing was successful and should result in the program exiting gracefully. The class uses a macro `CLI11_ERROR_DEF` to define its constructor, which initializes the `Success` object with a default message and an exit code indicating success.
- **Member Functions**:
    - [`Success::Success`](#SuccessSuccess)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### Success::Success<!-- {{#callable:Success::Success}} -->
The `Success` constructor initializes a `Success` object with a default success message and exit code.
- **Inputs**: None
- **Control Flow**:
    - The `Success` constructor is called with no arguments.
    - It delegates to another `Success` constructor with a default message and the `ExitCodes::Success` exit code.
- **Output**: A `Success` object initialized with a default message and exit code.
- **See also**: [`Success`](#Success)  (Data Structure)



---
### CallForHelp<!-- {{#data_structure:CallForHelp}} -->
- **Type**: `class`
- **Description**: The `CallForHelp` class is a specialized error class derived from the `Success` class within the CLI11 library. It represents a successful parsing event triggered by a help request, such as when a user inputs `-h` or `--help` on the command line. This class is designed to be caught in the main function to provide help information to the user, and it uses the `CLI11_ERROR_DEF` macro to define its constructors, ensuring it carries a message and an exit code indicating success.
- **Member Functions**:
    - [`CallForHelp::CallForHelp`](#CallForHelpCallForHelp)
- **Inherits From**:
    - [`Success::Success`](#SuccessSuccess)

**Methods**

---
#### CallForHelp::CallForHelp<!-- {{#callable:CallForHelp::CallForHelp}} -->
The `CallForHelp` constructor initializes an instance of the `CallForHelp` class with a default message and exit code, indicating a successful completion that should be caught in the main function.
- **Inputs**: None
- **Control Flow**:
    - The constructor `CallForHelp()` is called without any arguments.
    - It delegates to another constructor of the same class, passing a default message and the `ExitCodes::Success` as arguments.
    - The delegated constructor initializes the base class `Success` with these arguments.
- **Output**: An instance of the `CallForHelp` class is created, which is a type of `Success` indicating a successful operation that should trigger a help message.
- **See also**: [`CallForHelp`](#CallForHelp)  (Data Structure)



---
### CallForAllHelp<!-- {{#data_structure:CallForAllHelp}} -->
- **Type**: `class`
- **Description**: The `CallForAllHelp` class is a specialized error class derived from the `Success` class within the CLI11 library. It represents a successful completion of a command-line parsing operation, specifically triggered by a command-line option like `--help-all`. This class is designed to be caught in the main function of a program to handle help requests for all available commands or options, and it uses the `ExitCodes::Success` exit code to indicate successful execution.
- **Member Functions**:
    - [`CallForAllHelp::CallForAllHelp`](#CallForAllHelpCallForAllHelp)
- **Inherits From**:
    - [`Success::Success`](#SuccessSuccess)

**Methods**

---
#### CallForAllHelp::CallForAllHelp<!-- {{#callable:CallForAllHelp::CallForAllHelp}} -->
The `CallForAllHelp` constructor initializes an instance of the `CallForAllHelp` class with a default message and success exit code.
- **Inputs**: None
- **Control Flow**:
    - The constructor `CallForAllHelp()` is called without any arguments.
    - It delegates to another constructor of the same class, passing a default message and the `ExitCodes::Success` as arguments.
- **Output**: An instance of the `CallForAllHelp` class is created, initialized with a default message and an exit code indicating success.
- **See also**: [`CallForAllHelp`](#CallForAllHelp)  (Data Structure)



---
### CallForVersion<!-- {{#data_structure:CallForVersion}} -->
- **Type**: `class`
- **Description**: The `CallForVersion` class is a specialized error class derived from the `Success` class within the CLI11 library. It represents a successful completion of a command-line parsing operation specifically triggered by a version request, such as using `-v` or `--version` on the command line. This class is designed to be caught in the main function of a program to handle version display logic, and it uses the `CLI11_ERROR_DEF` macro to define its constructors, inheriting behavior from its parent class.
- **Member Functions**:
    - [`CallForVersion::CallForVersion`](#CallForVersionCallForVersion)
- **Inherits From**:
    - [`Success::Success`](#SuccessSuccess)

**Methods**

---
#### CallForVersion::CallForVersion<!-- {{#callable:CallForVersion::CallForVersion}} -->
The `CallForVersion` constructor initializes an instance of the `CallForVersion` class with a default message and success exit code.
- **Inputs**: None
- **Control Flow**:
    - The constructor `CallForVersion()` is called without any arguments.
    - It delegates to another constructor of the same class with a default message and the `ExitCodes::Success` exit code.
- **Output**: An instance of the `CallForVersion` class is created, initialized with a default message and a success exit code.
- **See also**: [`CallForVersion`](#CallForVersion)  (Data Structure)



---
### RuntimeError<!-- {{#data_structure:RuntimeError}} -->
- **Type**: `class`
- **Description**: The `RuntimeError` class is a specialized error class that inherits from `ParseError`, which itself is derived from the `Error` class. It is part of the CLI11 library's error handling mechanism, specifically designed to represent runtime errors that occur during the parsing process. The class uses a macro `CLI11_ERROR_DEF` to define its constructors, allowing it to be initialized with a custom exit code and message. By default, it initializes with an exit code of 1 and a message indicating a runtime error. This class does not define any additional members beyond those inherited from its parent classes.
- **Member Functions**:
    - [`RuntimeError::RuntimeError`](#RuntimeErrorRuntimeError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### RuntimeError::RuntimeError<!-- {{#callable:RuntimeError::RuntimeError}} -->
The `RuntimeError` constructor initializes a `RuntimeError` object with a default exit code and message.
- **Inputs**:
    - `exit_code`: An integer representing the exit code for the error, defaulting to 1.
- **Control Flow**:
    - The constructor is called with an optional integer parameter `exit_code`.
    - If `exit_code` is not provided, it defaults to 1.
    - The constructor delegates to another `RuntimeError` constructor with the message "Runtime error" and the provided or default `exit_code`.
- **Output**: An instance of the `RuntimeError` class, initialized with a specific exit code and a default error message.
- **See also**: [`RuntimeError`](#RuntimeError)  (Data Structure)



---
### FileError<!-- {{#data_structure:FileError}} -->
- **Type**: `class`
- **Description**: The `FileError` class is a specialized error class that inherits from `ParseError`, designed to handle errors related to file operations within the CLI11 library. It provides a mechanism to create an error instance when a file is missing or unreadable, using a static method `Missing` that constructs a `FileError` with a specific message indicating the file's unreadability or absence. This class is part of a hierarchy of error classes used to manage and report various error conditions encountered during command-line parsing and execution.
- **Member Functions**:
    - [`FileError::Missing`](#FileErrorMissing)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### FileError::Missing<!-- {{#callable:FileError::Missing}} -->
The `Missing` function creates a `FileError` object indicating that a specified file was not readable, possibly because it is missing.
- **Inputs**:
    - `name`: A string representing the name of the file that could not be read.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the string ' was not readable (missing?)' to the `name`.
    - It returns a `FileError` object initialized with the concatenated string.
- **Output**: A `FileError` object with a message indicating the file was not readable and may be missing.
- **See also**: [`FileError`](#FileError)  (Data Structure)



---
### ConversionError<!-- {{#data_structure:ConversionError}} -->
- **Type**: `class`
- **Description**: The `ConversionError` class is a specialized error class that inherits from `ParseError` and is used to handle errors related to conversion failures in the CLI11 library. It provides constructors for creating error messages when a value cannot be converted to an expected type or when there are too many inputs for a flag. The class also includes static methods for generating specific conversion error messages, such as when a flag receives too many inputs or when a value should be true/false or a number.
- **Member Functions**:
    - [`ConversionError::ConversionError`](#ConversionErrorConversionError)
    - [`ConversionError::ConversionError`](#ConversionErrorConversionError)
    - [`ConversionError::TooManyInputsFlag`](#ConversionErrorTooManyInputsFlag)
    - [`ConversionError::TrueFalse`](#ConversionErrorTrueFalse)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ConversionError::ConversionError<!-- {{#callable:ConversionError::ConversionError}} -->
The `ConversionError` constructor initializes an error message indicating a conversion failure for a given member or a list of results.
- **Inputs**:
    - `member`: A string representing the member value that failed conversion.
    - `name`: A string representing the name associated with the conversion error.
    - `results`: A vector of strings representing the results that could not be converted.
- **Control Flow**:
    - The constructor `ConversionError(std::string member, std::string name)` is called with two string arguments, concatenates them into an error message, and passes it to another `ConversionError` constructor.
    - The constructor `ConversionError(std::string name, std::vector<std::string> results)` is called with a string and a vector of strings, joins the vector into a single string, concatenates it with the name into an error message, and passes it to another `ConversionError` constructor.
- **Output**: An instance of `ConversionError` with a descriptive error message about the conversion failure.
- **See also**: [`ConversionError`](#ConversionError)  (Data Structure)


---
#### ConversionError::ConversionError<!-- {{#callable:ConversionError::ConversionError}} -->
The `ConversionError` constructor creates an error message indicating a failure to convert a given name and its associated results.
- **Inputs**:
    - `name`: A string representing the name of the entity that failed to convert.
    - `results`: A vector of strings containing the results or values that were attempted to be converted.
- **Control Flow**:
    - The constructor initializes a `ConversionError` object by calling another constructor with a formatted error message.
    - The error message is constructed by concatenating the name with the joined results using a helper function `detail::join`.
- **Output**: An instance of `ConversionError` with a specific error message indicating the conversion failure.
- **See also**: [`ConversionError`](#ConversionError)  (Data Structure)


---
#### ConversionError::TooManyInputsFlag<!-- {{#callable:ConversionError::TooManyInputsFlag}} -->
The `TooManyInputsFlag` function creates a `ConversionError` indicating that too many inputs were provided for a flag.
- **Inputs**:
    - `name`: A string representing the name of the flag that received too many inputs.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `ConversionError` object with a message indicating that the flag identified by `name` received too many inputs.
    - The constructed `ConversionError` is returned.
- **Output**: A `ConversionError` object with a message indicating the error of too many inputs for a flag.
- **See also**: [`ConversionError`](#ConversionError)  (Data Structure)


---
#### ConversionError::TrueFalse<!-- {{#callable:ConversionError::TrueFalse}} -->
The `TrueFalse` function creates a `ConversionError` indicating that a value should be either true/false or a number.
- **Inputs**:
    - `name`: A string representing the name of the value that caused the error.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It constructs a `ConversionError` object with a message indicating that the value should be true/false or a number, appending the `name` to the message.
- **Output**: A `ConversionError` object with a specific error message.
- **See also**: [`ConversionError`](#ConversionError)  (Data Structure)



---
### ValidationError<!-- {{#data_structure:ValidationError}} -->
- **Type**: `class`
- **Description**: The `ValidationError` class is a specialized error class that inherits from `ParseError`, which itself is derived from the `Error` class. It is used to represent errors that occur during the validation phase of parsing in the CLI11 library. The class is constructed using macros that define its constructors, allowing it to be initialized with a message and an exit code. The `ValidationError` class is part of a hierarchy of error classes designed to handle various error scenarios in command-line parsing.
- **Member Functions**:
    - [`ValidationError::ValidationError`](#ValidationErrorValidationError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ValidationError::ValidationError<!-- {{#callable:ValidationError::ValidationError}} -->
The `ValidationError` constructor creates a `ValidationError` object by concatenating a name and message into a single string and passing it to another constructor.
- **Inputs**:
    - `name`: A string representing the name associated with the validation error.
    - `msg`: A string containing the message or description of the validation error.
- **Control Flow**:
    - The constructor takes two string parameters, `name` and `msg`.
    - It concatenates these two strings with a colon and a space in between.
    - The concatenated string is then passed to another constructor of `ValidationError`.
- **Output**: An instance of the `ValidationError` class initialized with a combined error message.
- **See also**: [`ValidationError`](#ValidationError)  (Data Structure)



---
### RequiredError<!-- {{#data_structure:RequiredError}} -->
- **Type**: `class`
- **Description**: The `RequiredError` class is a specialized error class derived from `ParseError` within the CLI11 library, designed to handle situations where a required command-line option or subcommand is missing. It provides constructors and static methods to generate error messages specific to missing subcommands or options, with detailed messages indicating the number of required and provided options. This class is part of a hierarchy of error classes used to manage and report errors during command-line parsing.
- **Member Functions**:
    - [`RequiredError::RequiredError`](#RequiredErrorRequiredError)
    - [`RequiredError::Subcommand`](#RequiredErrorSubcommand)
    - [`RequiredError::Option`](#RequiredErrorOption)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### RequiredError::RequiredError<!-- {{#callable:RequiredError::RequiredError}} -->
The `RequiredError` constructor initializes a `RequiredError` object with a specific error message indicating a required element and an associated exit code.
- **Inputs**:
    - `name`: A string representing the name of the required element that is missing.
- **Control Flow**:
    - The constructor takes a single string argument `name`.
    - It calls another constructor of `RequiredError` with a message constructed by appending ' is required' to the `name` and the exit code `ExitCodes::RequiredError`.
- **Output**: An instance of the `RequiredError` class initialized with a specific error message and exit code.
- **See also**: [`RequiredError`](#RequiredError)  (Data Structure)


---
#### RequiredError::Subcommand<!-- {{#callable:RequiredError::Subcommand}} -->
The `Subcommand` function generates a [`RequiredError`](#RequiredErrorRequiredError) indicating the minimum number of subcommands required.
- **Inputs**:
    - `min_subcom`: A size_t value representing the minimum number of subcommands required.
- **Control Flow**:
    - Check if `min_subcom` is equal to 1.
    - If true, return a [`RequiredError`](#RequiredErrorRequiredError) with the message 'A subcommand'.
    - If false, return a [`RequiredError`](#RequiredErrorRequiredError) with a message indicating the required number of subcommands and the `ExitCodes::RequiredError` code.
- **Output**: A [`RequiredError`](#RequiredErrorRequiredError) object with a message about the required number of subcommands.
- **Functions called**:
    - [`RequiredError::RequiredError`](#RequiredErrorRequiredError)
- **See also**: [`RequiredError`](#RequiredError)  (Data Structure)


---
#### RequiredError::Option<!-- {{#callable:RequiredError::Option}} -->
The `Option` function checks the number of options used against specified minimum and maximum constraints and returns a [`RequiredError`](#RequiredErrorRequiredError) if the constraints are not met.
- **Inputs**:
    - `min_option`: The minimum number of options that must be used.
    - `max_option`: The maximum number of options that can be used.
    - `used`: The actual number of options that have been used.
    - `option_list`: A string representation of the list of options available.
- **Control Flow**:
    - Check if exactly one option is required and none are used, returning an error message if true.
    - Check if exactly one option is required and more than one is used, returning an error message if true.
    - Check if at least one option is required and none are used, returning an error message if true.
    - Check if the number of used options is less than the minimum required, returning an error message if true.
    - Check if only one option is allowed and more than one is used, returning an error message if true.
    - Return an error message if the number of used options exceeds the maximum allowed.
- **Output**: A [`RequiredError`](#RequiredErrorRequiredError) object containing an error message and an exit code if the option constraints are violated.
- **Functions called**:
    - [`RequiredError::RequiredError`](#RequiredErrorRequiredError)
- **See also**: [`RequiredError`](#RequiredError)  (Data Structure)



---
### ArgumentMismatch<!-- {{#data_structure:ArgumentMismatch}} -->
- **Type**: `class`
- **Description**: The `ArgumentMismatch` class is a specialized error class derived from `ParseError` within the CLI11 library, designed to handle situations where the number of arguments provided does not match the expected count during command-line parsing. It provides constructors and static methods to create error messages for various mismatch scenarios, such as expecting at least or at most a certain number of arguments, or handling specific types of argument mismatches. This class is part of a broader error handling framework in CLI11, which uses custom error codes to facilitate robust command-line interface development.
- **Member Functions**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
    - [`ArgumentMismatch::AtLeast`](#ArgumentMismatchAtLeast)
    - [`ArgumentMismatch::AtMost`](#ArgumentMismatchAtMost)
    - [`ArgumentMismatch::TypedAtLeast`](#ArgumentMismatchTypedAtLeast)
    - [`ArgumentMismatch::FlagOverride`](#ArgumentMismatchFlagOverride)
    - [`ArgumentMismatch::PartialType`](#ArgumentMismatchPartialType)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ArgumentMismatch::ArgumentMismatch<!-- {{#callable:ArgumentMismatch::ArgumentMismatch}} -->
The `ArgumentMismatch` constructor initializes an error message indicating a mismatch between expected and received argument counts for a given command.
- **Inputs**:
    - `name`: The name of the command or function where the argument mismatch occurred.
    - `expected`: An integer representing the expected number of arguments; a positive value indicates an exact number, while a negative value indicates a minimum number.
    - `received`: A size_t representing the actual number of arguments received.
- **Control Flow**:
    - The constructor checks if the 'expected' value is greater than zero to determine if an exact number of arguments is expected.
    - If 'expected' is greater than zero, it constructs an error message indicating the exact number of arguments expected and the number received.
    - If 'expected' is less than or equal to zero, it constructs an error message indicating the minimum number of arguments expected and the number received.
    - The constructed error message and the exit code 'ExitCodes::ArgumentMismatch' are passed to the base class constructor.
- **Output**: An instance of the `ArgumentMismatch` class, which is a type of `ParseError`, initialized with a specific error message and exit code.
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)


---
#### ArgumentMismatch::AtLeast<!-- {{#callable:ArgumentMismatch::AtLeast}} -->
The `AtLeast` function creates an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) error indicating that a minimum number of arguments was not met.
- **Inputs**:
    - `name`: A string representing the name of the argument or command that is being checked.
    - `num`: An integer specifying the minimum number of arguments required.
    - `received`: A size_t value representing the number of arguments actually received.
- **Control Flow**:
    - The function constructs an error message string by concatenating the name, the required minimum number of arguments, and the number of arguments received.
    - It then returns an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with this error message.
- **Output**: An [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object containing an error message about the insufficient number of arguments received.
- **Functions called**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)


---
#### ArgumentMismatch::AtMost<!-- {{#callable:ArgumentMismatch::AtMost}} -->
The `AtMost` function creates an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) error indicating that a maximum number of arguments was expected but more were received.
- **Inputs**:
    - `name`: A string representing the name of the argument or command that is being checked.
    - `num`: An integer representing the maximum number of arguments expected.
    - `received`: A size_t value representing the number of arguments actually received.
- **Control Flow**:
    - The function constructs an error message string by concatenating the name, the expected maximum number of arguments, and the number of arguments received.
    - It then returns an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with this error message.
- **Output**: An [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with a message indicating the discrepancy between the expected and received number of arguments.
- **Functions called**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)


---
#### ArgumentMismatch::TypedAtLeast<!-- {{#callable:ArgumentMismatch::TypedAtLeast}} -->
The `TypedAtLeast` function creates an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) error message indicating that a specified number of arguments of a certain type are missing for a given command or option.
- **Inputs**:
    - `name`: A string representing the name of the command or option that is missing arguments.
    - `num`: An integer representing the number of required arguments that are missing.
    - `type`: A string representing the type of arguments that are required.
- **Control Flow**:
    - The function constructs an error message by concatenating the name, number of required arguments, and type into a formatted string.
    - It then returns an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with this error message.
- **Output**: An [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object containing a formatted error message about missing typed arguments.
- **Functions called**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)


---
#### ArgumentMismatch::FlagOverride<!-- {{#callable:ArgumentMismatch::FlagOverride}} -->
The `FlagOverride` function creates an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) error indicating that a disallowed flag override was given for a specified name.
- **Inputs**:
    - `name`: A string representing the name associated with the flag override error.
- **Control Flow**:
    - The function takes a single string argument `name`.
    - It concatenates the `name` with a specific error message indicating a disallowed flag override.
    - The function returns an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with the constructed error message.
- **Output**: An [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with a message indicating a disallowed flag override for the given name.
- **Functions called**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)


---
#### ArgumentMismatch::PartialType<!-- {{#callable:ArgumentMismatch::PartialType}} -->
The `PartialType` function creates an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) error indicating that a specified type is only partially defined, requiring a certain number of elements.
- **Inputs**:
    - `name`: A string representing the name of the argument or option that is partially specified.
    - `num`: An integer representing the number of elements required for each specified type.
    - `type`: A string representing the type that is only partially specified.
- **Control Flow**:
    - The function constructs an error message by concatenating the name, type, and the number of required elements into a descriptive string.
    - It then returns an [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with this error message.
- **Output**: An [`ArgumentMismatch`](#ArgumentMismatchArgumentMismatch) object initialized with a message indicating the partial specification of a type and the number of required elements.
- **Functions called**:
    - [`ArgumentMismatch::ArgumentMismatch`](#ArgumentMismatchArgumentMismatch)
- **See also**: [`ArgumentMismatch`](#ArgumentMismatch)  (Data Structure)



---
### RequiresError<!-- {{#data_structure:RequiresError}} -->
- **Type**: `class`
- **Description**: The `RequiresError` class is a specialized error class that inherits from `ParseError` within the CLI11 library. It is used to represent an error condition where a required option is missing during command-line parsing. The constructor of `RequiresError` takes two string parameters, `curname` and `subname`, and constructs an error message indicating that `curname` requires `subname`. This class is part of a hierarchy of error classes designed to handle various parsing and construction errors in a command-line interface context.
- **Member Functions**:
    - [`RequiresError::RequiresError`](#RequiresErrorRequiresError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### RequiresError::RequiresError<!-- {{#callable:RequiresError::RequiresError}} -->
The `RequiresError` constructor initializes an error indicating that a specific option requires another option to be present.
- **Inputs**:
    - `curname`: The name of the current option that has a requirement.
    - `subname`: The name of the required option that must be present.
- **Control Flow**:
    - The constructor is called with two string arguments, `curname` and `subname`.
    - It concatenates these strings with the phrase ' requires ' to form a complete error message.
    - The constructor then calls another `RequiresError` constructor with this message and the `ExitCodes::RequiresError` exit code.
- **Output**: An instance of `RequiresError` is created, representing an error where a required option is missing.
- **See also**: [`RequiresError`](#RequiresError)  (Data Structure)



---
### ExcludesError<!-- {{#data_structure:ExcludesError}} -->
- **Type**: `class`
- **Description**: The `ExcludesError` class is a specialized error type that inherits from the `ParseError` class within the CLI11 library. It is used to represent an error condition where a particular command-line option excludes another, meaning that both options cannot be used together. The constructor of `ExcludesError` takes two string parameters, `curname` and `subname`, and constructs an error message indicating that the current option excludes the specified sub-option. This class is part of a hierarchy of error classes designed to handle various command-line parsing errors in a structured manner.
- **Member Functions**:
    - [`ExcludesError::ExcludesError`](#ExcludesErrorExcludesError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ExcludesError::ExcludesError<!-- {{#callable:ExcludesError::ExcludesError}} -->
The `ExcludesError` constructor initializes an error indicating that one option excludes another in a command-line interface.
- **Inputs**:
    - `curname`: The name of the current option that is excluding another option.
    - `subname`: The name of the option that is being excluded by the current option.
- **Control Flow**:
    - The constructor is called with two string arguments, `curname` and `subname`.
    - It constructs a message by concatenating `curname`, the string ' excludes ', and `subname`.
    - The constructor then calls another `ExcludesError` constructor with the constructed message and the `ExitCodes::ExcludesError` enumeration value.
- **Output**: An instance of the `ExcludesError` class, initialized with a specific error message and exit code.
- **See also**: [`ExcludesError`](#ExcludesError)  (Data Structure)



---
### ExtrasError<!-- {{#data_structure:ExtrasError}} -->
- **Type**: `class`
- **Description**: The `ExtrasError` class is a specialized error class derived from `ParseError` within the CLI11 library, designed to handle situations where unexpected arguments are encountered during command-line parsing. It constructs error messages based on the number of unexpected arguments and associates them with a specific exit code, `ExitCodes::ExtrasError`. This class is part of a hierarchy of error classes used to manage various parsing and construction errors in the CLI11 library.
- **Member Functions**:
    - [`ExtrasError::ExtrasError`](#ExtrasErrorExtrasError)
    - [`ExtrasError::ExtrasError`](#ExtrasErrorExtrasError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ExtrasError::ExtrasError<!-- {{#callable:ExtrasError::ExtrasError}} -->
The `ExtrasError` constructor initializes an error object for unexpected command-line arguments, providing a descriptive message and an exit code.
- **Inputs**:
    - `args`: A vector of strings representing the unexpected command-line arguments.
- **Control Flow**:
    - The constructor checks if the size of `args` is greater than 1 to determine the appropriate error message prefix ('arguments' vs 'argument').
    - It uses the `detail::join` function to concatenate the elements of `args` into a single string, separated by spaces.
    - The constructor then calls another `ExtrasError` constructor with the constructed message and the `ExitCodes::ExtrasError` as parameters.
- **Output**: An `ExtrasError` object is created, which is a type of `ParseError`, containing a message about unexpected arguments and an associated exit code.
- **See also**: [`ExtrasError`](#ExtrasError)  (Data Structure)


---
#### ExtrasError::ExtrasError<!-- {{#callable:ExtrasError::ExtrasError}} -->
The `ExtrasError` constructor initializes an error object for unexpected command-line arguments, providing a descriptive message and an exit code.
- **Inputs**:
    - `name`: A string representing the name of the error.
    - `args`: A vector of strings containing the unexpected arguments.
- **Control Flow**:
    - The constructor checks the size of the `args` vector to determine whether to use a singular or plural form in the error message.
    - It constructs an error message by joining the `args` vector into a single string, prefixed by a message indicating unexpected arguments.
    - The constructor calls another `ExtrasError` constructor with the constructed message and a predefined exit code `ExitCodes::ExtrasError`.
- **Output**: An `ExtrasError` object initialized with a specific error message and exit code.
- **See also**: [`ExtrasError`](#ExtrasError)  (Data Structure)



---
### ConfigError<!-- {{#data_structure:ConfigError}} -->
- **Type**: `class`
- **Description**: The `ConfigError` class is a specialized error class that inherits from `ParseError` within the CLI namespace. It is designed to handle errors related to configuration file parsing in the CLI11 library. The class provides static methods to generate specific error messages, such as when extra values are found in an INI file or when an option is not allowed in a configuration file. It utilizes macros to define constructors and simplify error message creation.
- **Member Functions**:
    - [`ConfigError::Extras`](#ConfigErrorExtras)
    - [`ConfigError::NotConfigurable`](#ConfigErrorNotConfigurable)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### ConfigError::Extras<!-- {{#callable:ConfigError::Extras}} -->
The `Extras` function creates a `ConfigError` object indicating that an item could not be parsed from an INI file.
- **Inputs**:
    - `item`: A string representing the item that could not be parsed from the INI file.
- **Control Flow**:
    - The function takes a single string argument `item`.
    - It constructs a `ConfigError` object with a message indicating the inability to parse the given item.
    - The constructed `ConfigError` object is returned.
- **Output**: A `ConfigError` object with a message indicating the parsing failure of the specified item.
- **See also**: [`ConfigError`](#ConfigError)  (Data Structure)


---
#### ConfigError::NotConfigurable<!-- {{#callable:ConfigError::NotConfigurable}} -->
The `NotConfigurable` function creates a `ConfigError` indicating that a specific option is not allowed in a configuration file.
- **Inputs**:
    - `item`: A string representing the name of the configuration option that is not allowed.
- **Control Flow**:
    - The function takes a single string argument `item`.
    - It concatenates the `item` with a predefined error message string ": This option is not allowed in a configuration file".
    - It returns a `ConfigError` object initialized with the concatenated error message.
- **Output**: A `ConfigError` object with a message indicating the specified option is not allowed in a configuration file.
- **See also**: [`ConfigError`](#ConfigError)  (Data Structure)



---
### InvalidError<!-- {{#data_structure:InvalidError}} -->
- **Type**: `class`
- **Description**: The `InvalidError` class is a specialized error class that inherits from `ParseError`, designed to handle validation failures before parsing in the CLI11 library. It is constructed with a message indicating that there are too many positional arguments when unlimited expected arguments are specified, and it uses the `ExitCodes::InvalidError` exit code to signify this specific error condition. This class is part of a hierarchy of error classes used to manage and report different types of errors encountered during command-line parsing and validation.
- **Member Functions**:
    - [`InvalidError::InvalidError`](#InvalidErrorInvalidError)
- **Inherits From**:
    - `ParseError`

**Methods**

---
#### InvalidError::InvalidError<!-- {{#callable:InvalidError::InvalidError}} -->
The `InvalidError` constructor initializes an error indicating too many positional arguments were provided when unlimited arguments were expected.
- **Inputs**:
    - `name`: A string representing the name or context of the error.
- **Control Flow**:
    - The constructor takes a single string argument `name`.
    - It constructs an error message by appending ": Too many positional arguments with unlimited expected args" to the `name`.
    - It calls another constructor of `InvalidError` with the constructed message and the `ExitCodes::InvalidError` as arguments.
- **Output**: An instance of `InvalidError` is created, which is a type of `ParseError`.
- **See also**: [`InvalidError`](#InvalidError)  (Data Structure)



---
### HorribleError<!-- {{#data_structure:HorribleError}} -->
- **Type**: `class`
- **Description**: The `HorribleError` class is a custom exception type derived from the `ParseError` class within the CLI namespace. It is designed to handle unexpected or critical errors that occur during the parsing process, serving as a safety check to ensure that selection and parsing operations match correctly. The class uses macros to define its constructors, which are intended to simplify the creation of error messages and exit codes associated with this type of error.
- **Inherits From**:
    - `ParseError`


---
### OptionNotFound<!-- {{#data_structure:HorribleError::OptionNotFound}} -->
- **Type**: `class`
- **Description**: The `OptionNotFound` class is a specialized error class derived from the `Error` class within the CLI namespace. It is used to represent an error condition where a specified option is not found during the parsing or processing of command-line arguments. This class utilizes a macro `CLI11_ERROR_DEF` to define its constructors, which initialize the error with a message indicating the option was not found and an associated exit code from the `ExitCodes` enum, specifically `ExitCodes::OptionNotFound`. The class is part of a larger error handling framework in the CLI11 library, which provides structured error reporting for command-line interface applications.
- **Member Functions**:
    - [`HorribleError::OptionNotFound::OptionNotFound`](#OptionNotFoundOptionNotFound)
- **Inherits From**:
    - [`Error::Error`](#ErrorError)

**Methods**

---
#### OptionNotFound::OptionNotFound<!-- {{#callable:HorribleError::OptionNotFound::OptionNotFound}} -->
The `OptionNotFound` constructor initializes an error object indicating that a specified option was not found.
- **Inputs**:
    - `name`: A string representing the name of the option that was not found.
- **Control Flow**:
    - The constructor takes a single string argument `name`.
    - It calls another constructor of the same class with a message constructed by appending ' not found' to the `name` and an exit code `ExitCodes::OptionNotFound`.
- **Output**: An `OptionNotFound` object is created, which is a type of error indicating that a specified option was not found.
- **See also**: [`HorribleError::OptionNotFound`](#OptionNotFound)  (Data Structure)



# Functions

---
### Success<!-- {{#callable:Success::Success}} -->
The `Success` constructor initializes a `Success` object with a default success message and exit code.
- **Inputs**: None
- **Control Flow**:
    - The constructor is called with no arguments.
    - It delegates to another constructor of the `Success` class, passing a default message and the `ExitCodes::Success` value.
- **Output**: A `Success` object is created with a predefined message and exit code indicating successful completion.


---
### Error<!-- {{#callable:Error::Error}} -->
The `Error` constructor initializes an `Error` object with a name, message, and exit code, converting the exit code from an `ExitCodes` enum to an integer if necessary.
- **Inputs**:
    - `name`: A string representing the name of the error.
    - `msg`: A string containing the error message.
    - `exit_code`: An `ExitCodes` enum value representing the exit code for the error.
- **Control Flow**:
    - The constructor is called with three parameters: `name`, `msg`, and `exit_code` of type `ExitCodes`.
    - The constructor delegates to another `Error` constructor by calling it with `name`, `msg`, and the integer representation of `exit_code`.
- **Output**: An `Error` object is constructed and initialized with the provided name, message, and exit code.


