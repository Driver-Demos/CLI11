# Purpose
This C++ source code file is part of a library designed to handle configuration files, specifically for command-line interface (CLI) applications. The code defines a set of classes and structures within the `CLI` namespace, which are used to convert between application configurations and configuration file formats such as INI and TOML. The primary classes in this file are `Config`, `ConfigBase`, and [`ConfigINI`](#ConfigINIConfigINI), each serving a specific role in managing configuration data. The `Config` class is an abstract base class that outlines the interface for converting applications to and from configuration files, while `ConfigBase` provides a concrete implementation that supports various configuration file features, such as comment characters, array delimiters, and section handling. The [`ConfigINI`](#ConfigINIConfigINI) class extends `ConfigBase` to provide INI-specific configurations.

The file includes several technical components, such as the `ConfigItem` structure, which holds configuration data, and various methods for parsing and generating configuration files. The code is designed to be part of a larger library, as indicated by the use of `#pragma once` for header file inclusion and the inclusion of other headers like "Error.hpp" and "StringTools.hpp". The file defines a public API for handling configuration files, allowing users to customize the parsing and generation of configuration data through various methods and settings. This code is intended to be imported and used in other parts of a CLI application, providing a robust and flexible way to manage configuration files.
# Imports and Dependencies

---
- `algorithm`
- `fstream`
- `iostream`
- `memory`
- `string`
- `vector`
- `Error.hpp`
- `StringTools.hpp`


# Data Structures

---
### ConfigItem<!-- {{#data_structure:CLI::ConfigItem}} -->
- **Type**: `struct`
- **Members**:
    - `parents`: A vector of strings representing the list of parent elements.
    - `name`: A string representing the name of the configuration item.
    - `inputs`: A vector of strings representing the inputs associated with the configuration item.
    - `multiline`: A boolean indicating if a multiline vector separator was inserted.
- **Description**: The `ConfigItem` struct is designed to hold configuration data for an application, specifically within the context of the CLI11 library. It includes a list of parent elements, a name, and a list of inputs, which are all stored as strings. Additionally, it has a boolean flag to indicate if a multiline vector separator was used. The struct provides a method to generate a full name by joining the parents and name with a dot separator, which is useful for hierarchical configuration settings.


---
### Config<!-- {{#data_structure:CLI::Config}} -->
- **Type**: `class`
- **Members**:
    - `items`: A protected vector of ConfigItem objects that stores configuration items.
- **Description**: The `Config` class is an abstract base class designed to provide a framework for converting between application configurations and configuration files. It contains a protected member `items`, which is a vector of `ConfigItem` objects, representing the configuration items. The class declares pure virtual functions `to_config` and `from_config` for converting an application to a configuration and vice versa, respectively. Additionally, it provides a method `to_flag` to retrieve a flag value from a `ConfigItem`. The class is intended to be extended by other classes that implement specific configuration file formats.


---
### ConfigBase<!-- {{#data_structure:ConfigBase}} -->
- **Type**: `class`
- **Members**:
    - `commentChar`: The character used for comments, defaulting to '#'.
    - `arrayStart`: The character used to start an array, defaulting to '['.
    - `arrayEnd`: The character used to end an array, defaulting to ']'.
    - `arraySeparator`: The character used to separate elements in an array, defaulting to ','.
    - `valueDelimiter`: The character used to separate the name from the value, defaulting to '='.
    - `stringQuote`: The character used around strings, defaulting to '"'.
    - `literalQuote`: The character used around single characters and literal strings, defaulting to '\''.
    - `maximumLayers`: The maximum number of layers allowed, defaulting to 255.
    - `parentSeparatorChar`: The separator used to separate parent layers, defaulting to '.'.
    - `commentDefaultsBool`: A boolean indicating whether to comment default values, defaulting to false.
    - `allowMultipleDuplicateFields`: A boolean indicating if the config reader should collapse repeated field names to a single vector, defaulting to false.
    - `configIndex`: The configuration index to use for arrayed sections, defaulting to -1.
    - `configSection`: The configuration section that should be used, defaulting to an empty string.
- **Description**: The `ConfigBase` class is a configuration converter that extends the `Config` class, designed to handle configuration files, particularly in INI/TOML formats. It provides a set of protected member variables that define various characters used in parsing and writing configuration files, such as comment characters, array delimiters, and value separators. The class also includes settings for managing configuration layers and sections, allowing for customization of how configuration data is interpreted and stored. Public methods are provided to modify these settings, enabling flexible configuration management.
- **Member Functions**:
    - [`ConfigBase::comment`](#ConfigBasecomment)
    - [`ConfigBase::arrayBounds`](#ConfigBasearrayBounds)
    - [`ConfigBase::arrayDelimiter`](#ConfigBasearrayDelimiter)
    - [`ConfigBase::valueSeparator`](#ConfigBasevalueSeparator)
    - [`ConfigBase::quoteCharacter`](#ConfigBasequoteCharacter)
    - [`ConfigBase::maxLayers`](#ConfigBasemaxLayers)
    - [`ConfigBase::parentSeparator`](#ConfigBaseparentSeparator)
    - [`ConfigBase::commentDefaults`](#ConfigBasecommentDefaults)
    - [`ConfigBase::sectionRef`](#ConfigBasesectionRef)
    - [`ConfigBase::section`](#ConfigBasesection)
    - [`ConfigBase::indexRef`](#ConfigBaseindexRef)
    - [`ConfigBase::index`](#ConfigBaseindex)
    - [`ConfigBase::index`](#ConfigBaseindex)
    - [`ConfigBase::allowDuplicateFields`](#ConfigBaseallowDuplicateFields)
- **Inherits From**:
    - [`CLI::Config`](#Config)

**Methods**

---
#### ConfigBase::comment<!-- {{#callable:ConfigBase::comment}} -->
The `comment` function sets the character used for comments in the configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `cchar`: A character that will be used to denote comments in the configuration.
- **Control Flow**:
    - Assign the input character `cchar` to the member variable `commentChar`.
    - Return a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::arrayBounds<!-- {{#callable:ConfigBase::arrayBounds}} -->
The `arrayBounds` method sets the start and end characters for arrays in a configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `aStart`: A character representing the start delimiter for an array.
    - `aEnd`: A character representing the end delimiter for an array.
- **Control Flow**:
    - Assigns the value of `aStart` to the `arrayStart` member variable.
    - Assigns the value of `aEnd` to the `arrayEnd` member variable.
    - Returns a pointer to the current `ConfigBase` object (`this`).
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::arrayDelimiter<!-- {{#callable:ConfigBase::arrayDelimiter}} -->
The `arrayDelimiter` function sets the character used to separate elements in an array within a configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `aSep`: A character that will be used as the delimiter for separating elements in an array.
- **Control Flow**:
    - The function assigns the input character `aSep` to the `arraySeparator` member variable of the `ConfigBase` class.
    - The function returns a pointer to the current instance of `ConfigBase` (i.e., `this`).
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::valueSeparator<!-- {{#callable:ConfigBase::valueSeparator}} -->
The `valueSeparator` function sets the character used to separate a name from its value in a configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `vSep`: A character that will be used as the delimiter between a name and its value in the configuration.
- **Control Flow**:
    - Assign the input character `vSep` to the `valueDelimiter` member variable of the `ConfigBase` class.
    - Return a pointer to the current instance of `ConfigBase` (i.e., `this`).
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::quoteCharacter<!-- {{#callable:ConfigBase::quoteCharacter}} -->
The `quoteCharacter` method sets the characters used for quoting strings and literal strings in a configuration.
- **Inputs**:
    - `qString`: A character to be used as the quote character for strings.
    - `literalChar`: A character to be used as the quote character for literal strings.
- **Control Flow**:
    - Assigns the value of `qString` to the `stringQuote` member variable.
    - Assigns the value of `literalChar` to the `literalQuote` member variable.
    - Returns a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current instance of `ConfigBase`, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::maxLayers<!-- {{#callable:ConfigBase::maxLayers}} -->
The `maxLayers` function sets the maximum number of configuration layers allowed and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `layers`: A `uint8_t` value representing the maximum number of layers to be set.
- **Control Flow**:
    - Assign the input `layers` to the `maximumLayers` member variable of the `ConfigBase` class.
    - Return a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::parentSeparator<!-- {{#callable:ConfigBase::parentSeparator}} -->
The `parentSeparator` function sets the character used to separate parent layers in a configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `sep`: A character that will be used as the separator for parent layers in the configuration.
- **Control Flow**:
    - Assign the input character `sep` to the member variable `parentSeparatorChar`.
    - Return a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::commentDefaults<!-- {{#callable:ConfigBase::commentDefaults}} -->
The `commentDefaults` method sets the `commentDefaultsBool` flag to indicate whether default values should be commented in the configuration and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `comDef`: A boolean flag indicating whether default values should be commented in the configuration; defaults to `true`.
- **Control Flow**:
    - The method assigns the value of `comDef` to the `commentDefaultsBool` member variable.
    - The method returns a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::sectionRef<!-- {{#callable:ConfigBase::sectionRef}} -->
The `sectionRef` function returns a reference to the `configSection` string member of the `ConfigBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the `configSection` member variable of the `ConfigBase` class.
- **Output**: A reference to the `configSection` string member variable.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::section<!-- {{#callable:ConfigBase::section}} -->
The `section` method sets the configuration section name and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `sectionName`: A `std::string` representing the name of the configuration section to be set.
- **Control Flow**:
    - Assign the input `sectionName` to the `configSection` member variable of the `ConfigBase` class.
    - Return a pointer to the current instance of `ConfigBase`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::indexRef<!-- {{#callable:ConfigBase::indexRef}} -->
The `indexRef` function returns a reference to the `configIndex` member variable of the `ConfigBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns a reference to the `configIndex` member variable.
- **Output**: A reference to the `configIndex` member variable, which is of type `int16_t`.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::index<!-- {{#callable:ConfigBase::index}} -->
The `index` function returns the current configuration index used for arrayed sections in the `ConfigBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the value of the `configIndex` member variable.
- **Output**: The function returns an `int16_t` representing the configuration index.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::index<!-- {{#callable:ConfigBase::index}} -->
The `index` function sets the configuration index for arrayed sections and returns a pointer to the current `ConfigBase` object.
- **Inputs**:
    - `sectionIndex`: An integer of type `int16_t` representing the index of the section to be set.
- **Control Flow**:
    - The function assigns the value of `sectionIndex` to the member variable `configIndex`.
    - The function returns a pointer to the current instance of `ConfigBase` using `this`.
- **Output**: A pointer to the current `ConfigBase` object, allowing for method chaining.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)


---
#### ConfigBase::allowDuplicateFields<!-- {{#callable:ConfigBase::allowDuplicateFields}} -->
The `allowDuplicateFields` method sets whether multiple duplicate fields in a configuration should be allowed and returns the current object for method chaining.
- **Inputs**:
    - `value`: A boolean value indicating whether to allow multiple duplicate fields; defaults to true if not provided.
- **Control Flow**:
    - The method assigns the input boolean value to the `allowMultipleDuplicateFields` member variable.
    - The method returns a pointer to the current `ConfigBase` object, enabling method chaining.
- **Output**: A pointer to the current `ConfigBase` object.
- **See also**: [`ConfigBase`](#ConfigBase)  (Data Structure)



---
### ConfigINI<!-- {{#data_structure:ConfigINI}} -->
- **Type**: `class`
- **Members**:
    - `commentChar`: Character used for comments, initialized to ';'.
    - `arrayStart`: Character used to start an array, initialized to '\0' (not used).
    - `arrayEnd`: Character used to end an array, initialized to '\0' (not used).
    - `arraySeparator`: Character used to separate elements in an array, initialized to ' ' (space).
    - `valueDelimiter`: Character used to separate the name from the value, initialized to '='.
- **Description**: The `ConfigINI` class is a specialized configuration handler that extends `ConfigTOML` to provide functionality for generating and parsing INI file formats. It customizes certain configuration parameters such as comment characters and delimiters to align with the INI standard, making it suitable for applications that require INI-compliant configuration files. The class sets default values for comment characters, array delimiters, and value separators to match typical INI file conventions.
- **Member Functions**:
    - [`ConfigINI::ConfigINI`](#ConfigINIConfigINI)
- **Inherits From**:
    - `ConfigTOML`

**Methods**

---
#### ConfigINI::ConfigINI<!-- {{#callable:ConfigINI::ConfigINI}} -->
The `ConfigINI` constructor initializes an instance of the `ConfigINI` class with specific character settings for parsing INI files.
- **Inputs**: None
- **Control Flow**:
    - The constructor initializes the `commentChar` to ';'.
    - The `arrayStart` and `arrayEnd` are set to '\0', indicating no specific start or end character for arrays.
    - The `arraySeparator` is set to a space character ' '.
    - The `valueDelimiter` is set to '='.
- **Output**: The function does not return any value as it is a constructor.
- **See also**: [`ConfigINI`](#ConfigINI)  (Data Structure)



# Functions

---
### from\_file<!-- {{#callable:CLI::CLI11_NODISCARD::vector<ConfigItem>::from_file}} -->
The `from_file` function reads a configuration file and converts its contents into a vector of `ConfigItem` objects, throwing an error if the file cannot be opened.
- **Inputs**:
    - `name`: A string representing the name of the configuration file to be read.
- **Control Flow**:
    - Open the file specified by the `name` parameter using an `std::ifstream` object.
    - Check if the file stream is in a good state; if not, throw a `FileError::Missing` exception with the file name.
    - Call the `from_config` method with the file stream to convert the file contents into a vector of `ConfigItem` objects.
- **Output**: Returns a vector of `ConfigItem` objects representing the configuration data read from the file.


---
### \~Config<!-- {{#callable:CLI::~Config}} -->
The `~Config` function is a virtual destructor for the `Config` class, ensuring proper cleanup of derived class objects.
- **Inputs**: None
- **Control Flow**:
    - The function is declared as a virtual destructor, allowing derived classes to override it if necessary.
    - It is defined with `= default`, indicating that the compiler should generate the default implementation for the destructor.
- **Output**: The function does not return any value as it is a destructor.


