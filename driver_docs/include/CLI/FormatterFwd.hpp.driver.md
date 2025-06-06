# Purpose
This C++ header file is part of the CLI11 library, which is designed to facilitate the creation of command-line interfaces. The file primarily defines classes and enumerations related to formatting help messages for command-line applications. The key components include the [`FormatterBase`](#FormatterBaseFormatterBase) class, which provides a base structure for formatting help output, and the [`Formatter`](#FormatterFormatter) class, which extends [`FormatterBase`](#FormatterBaseFormatterBase) to offer a customizable and detailed help message generation. The [`FormatterLambda`](#FormatterLambdaFormatterLambda) class is a specialized version of [`FormatterBase`](#FormatterBaseFormatterBase) that allows users to define custom formatting logic using lambda functions. The `AppFormatMode` enumeration specifies different modes of help output, such as normal, fully expanded, or subcommand-specific help.

The file is structured to provide a flexible and extensible framework for generating help messages, with various methods that can be overridden to customize the output. It includes setters and getters for configuring the layout of help messages, such as column widths and paragraph formatting. The file is intended to be included in other parts of the CLI11 library or user applications, as indicated by the `#pragma once` directive and the inclusion of other headers like "StringTools.hpp". This header does not define a public API directly but provides essential components for building user-facing command-line interfaces with customizable help documentation.
# Imports and Dependencies

---
- `functional`
- `map`
- `string`
- `utility`
- `vector`
- `StringTools.hpp`


# Data Structures

---
### AppFormatMode<!-- {{#data_structure:CLI::AppFormatMode}} -->
- **Type**: `enum`
- **Members**:
    - `Normal`: Represents the normal, detailed help format.
    - `All`: Represents a fully expanded help format.
    - `Sub`: Used when printed as part of expanded subcommand help.
- **Description**: The `AppFormatMode` enum is used to specify the type of help format requested in the CLI11 library. It is an enumeration of type `std::uint8_t` and includes three modes: `Normal`, `All`, and `Sub`. These modes determine how help information is displayed, with `Normal` providing detailed help, `All` offering a fully expanded help, and `Sub` being used for expanded subcommand help. This enum is passed by the `App` class and must be accepted by user classes as the second argument.


---
### FormatterBase<!-- {{#data_structure:CLI::FormatterBase}} -->
- **Type**: `class`
- **Members**:
    - `column_width_`: The width of the left column for options, flags, or subcommands.
    - `right_column_width_`: The width of the right column for descriptions of options, flags, or subcommands.
    - `description_paragraph_width_`: The width of the description paragraph at the top of the help output.
    - `footer_paragraph_width_`: The width of the footer paragraph in the help output.
    - `enable_description_formatting_`: A boolean flag to enable or disable formatting for the description paragraph.
    - `enable_footer_formatting_`: A boolean flag to enable or disable formatting for the footer paragraph.
    - `labels_`: A map storing user-changeable labels for help printout, such as 'REQUIRED' or 'EXCLUDES'.
- **Description**: The `FormatterBase` class serves as a base class for formatting help output in a command-line interface application. It provides configurable options for setting the widths of various sections of the help output, such as columns and paragraphs, and includes flags to enable or disable formatting for specific sections. Additionally, it maintains a map of labels that can be customized by the user to modify the help printout. The class is designed to be subclassed, allowing for further customization of the help formatting process.
- **Member Functions**:
    - [`CLI::FormatterBase::FormatterBase`](#FormatterBaseFormatterBase)
    - [`CLI::FormatterBase::FormatterBase`](#FormatterBaseFormatterBase)
    - [`CLI::FormatterBase::FormatterBase`](#FormatterBaseFormatterBase)
    - [`CLI::FormatterBase::operator=`](#FormatterBaseoperator=)
    - [`CLI::FormatterBase::operator=`](#FormatterBaseoperator=)
    - [`CLI::FormatterBase::~FormatterBase`](#FormatterBaseFormatterBase)
    - [`CLI::FormatterBase::label`](#FormatterBaselabel)
    - [`CLI::FormatterBase::column_width`](#FormatterBasecolumn_width)
    - [`CLI::FormatterBase::right_column_width`](#FormatterBaseright_column_width)
    - [`CLI::FormatterBase::description_paragraph_width`](#FormatterBasedescription_paragraph_width)
    - [`CLI::FormatterBase::footer_paragraph_width`](#FormatterBasefooter_paragraph_width)
    - [`CLI::FormatterBase::enable_description_formatting`](#FormatterBaseenable_description_formatting)
    - [`CLI::FormatterBase::enable_footer_formatting`](#FormatterBaseenable_footer_formatting)

**Methods**

---
#### FormatterBase::FormatterBase<!-- {{#callable:CLI::FormatterBase::FormatterBase}} -->
The `FormatterBase` class provides a base structure for formatting help output in a command-line interface application, with customizable column widths, paragraph formatting, and label settings.
- **Inputs**: None
- **Control Flow**:
    - The class defines several protected member variables for column widths, paragraph widths, and formatting options, which are initialized with default values.
    - The class provides a default constructor, copy constructor, move constructor, copy assignment operator, and move assignment operator, all of which are defaulted.
    - A virtual destructor is defined to handle a specific GCC bug, ensuring proper cleanup of derived classes.
    - The class declares a pure virtual method `make_help` that must be implemented by derived classes to generate help text.
    - Several setter methods are provided to customize the column widths, paragraph widths, and formatting options.
    - A method `label` is provided to set custom labels for help printout.
    - Getter methods are available to retrieve the current settings for column widths, paragraph widths, and formatting options.
- **Output**: The class itself does not produce any output directly, but it provides the structure and methods for derived classes to generate formatted help text.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::FormatterBase<!-- {{#callable:CLI::FormatterBase::FormatterBase}} -->
The `FormatterBase` class provides a base structure for formatting help output in a command-line interface application, with customizable column widths, paragraph formatting, and label settings.
- **Inputs**: None
- **Control Flow**:
    - The class defines several protected member variables to store formatting options such as column widths and paragraph formatting flags.
    - It provides a default constructor, copy constructor, move constructor, copy assignment operator, and move assignment operator, all of which are defaulted.
    - A virtual destructor is defined to ensure proper cleanup in derived classes, addressing a specific GCC bug.
    - The class declares a pure virtual function `make_help` that must be implemented by derived classes to generate help text.
    - Several setter methods are provided to adjust formatting options, such as column widths and label settings.
    - Getter methods are available to retrieve current formatting settings and label values.
- **Output**: The class itself does not produce any direct output but provides a framework for derived classes to generate formatted help text.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::FormatterBase<!-- {{#callable:CLI::FormatterBase::FormatterBase}} -->
The `FormatterBase` class provides a base structure for formatting help output in a command-line interface application, with customizable column widths and formatting options.
- **Inputs**: None
- **Control Flow**:
    - The class defines several protected member variables to control the formatting of help output, such as column widths and formatting flags.
    - It provides a default constructor, copy constructor, move constructor, copy assignment operator, and move assignment operator, all of which are defaulted.
    - A virtual destructor is defined to ensure proper cleanup in derived classes, especially to address a specific GCC bug.
    - The class declares a pure virtual function `make_help` that must be implemented by derived classes to generate help text.
    - Several setter methods are provided to adjust the formatting options, such as column widths and enabling/disabling formatting for descriptions and footers.
    - Getter methods are available to retrieve the current settings of the formatting options and labels.
- **Output**: The class itself does not produce any direct output but provides a framework for derived classes to generate formatted help text.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::operator=<!-- {{#callable:CLI::FormatterBase::operator=}} -->
The `operator=` function in the `FormatterBase` class provides default copy and move assignment operations.
- **Inputs**: None
- **Control Flow**:
    - The function is defined as a defaulted assignment operator, meaning it uses the compiler-generated default behavior for both copy and move assignments.
    - There is no explicit logic or control flow within the function itself as it relies on the default behavior provided by the compiler.
- **Output**: The function returns a reference to the `FormatterBase` object that has been assigned.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::operator=<!-- {{#callable:CLI::FormatterBase::operator=}} -->
The `operator=` function is a default move assignment operator for the `FormatterBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function is defined as a default move assignment operator, meaning it will automatically handle the move assignment of `FormatterBase` objects by transferring ownership of resources from the source object to the target object.
    - Since it is marked as `default`, the compiler will generate the move assignment operator implementation, which typically involves moving each member of the class from the source to the target.
- **Output**: The function returns a reference to the `FormatterBase` object that has been assigned the values from the source object.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::\~FormatterBase<!-- {{#callable:CLI::FormatterBase::~FormatterBase}} -->
The `~FormatterBase` function is a virtual destructor for the `FormatterBase` class, ensuring proper cleanup of derived class objects.
- **Inputs**: None
- **Control Flow**:
    - The destructor is declared as virtual to allow derived class destructors to be called when an object is deleted through a base class pointer.
    - The destructor is marked with `noexcept` to indicate that it does not throw exceptions, which is a good practice for destructors.
    - The destructor is defined as an empty body, indicating no specific cleanup is required for the `FormatterBase` class itself.
- **Output**: The function does not produce any output as it is a destructor.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::label<!-- {{#callable:CLI::FormatterBase::label}} -->
The `label` function sets a key-value pair in the `labels_` map to customize help printout labels in the `FormatterBase` class.
- **Inputs**:
    - `key`: A `std::string` representing the key for the label to be set or updated in the `labels_` map.
    - `val`: A `std::string` representing the value associated with the key in the `labels_` map.
- **Control Flow**:
    - The function takes two string parameters, `key` and `val`.
    - It assigns the value `val` to the key `key` in the `labels_` map, effectively setting or updating the label.
- **Output**: The function does not return any value; it modifies the `labels_` map in place.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::column\_width<!-- {{#callable:CLI::FormatterBase::column_width}} -->
The `column_width` function sets the width of the left column for options, flags, or subcommands in the `FormatterBase` class.
- **Inputs**:
    - `val`: A `std::size_t` value representing the new width for the left column.
- **Control Flow**:
    - The function takes a single input parameter `val`.
    - It assigns the value of `val` to the `column_width_` member variable of the `FormatterBase` class.
- **Output**: The function does not return any value; it modifies the `column_width_` member variable in place.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::right\_column\_width<!-- {{#callable:CLI::FormatterBase::right_column_width}} -->
The `right_column_width` function sets the width of the right column, which is used for the description of options, flags, and subcommands, in the `FormatterBase` class.
- **Inputs**:
    - `val`: A `std::size_t` value representing the new width for the right column.
- **Control Flow**:
    - The function takes a single input parameter `val`.
    - It assigns the value of `val` to the member variable `right_column_width_`.
- **Output**: The function does not return any value; it modifies the internal state of the `FormatterBase` object by setting the `right_column_width_` member variable.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::description\_paragraph\_width<!-- {{#callable:CLI::FormatterBase::description_paragraph_width}} -->
The `description_paragraph_width` function sets the width of the description paragraph at the top of the help documentation in the `FormatterBase` class.
- **Inputs**:
    - `val`: A `std::size_t` value representing the new width for the description paragraph.
- **Control Flow**:
    - The function takes a single input parameter `val`.
    - It assigns the value of `val` to the member variable `description_paragraph_width_`.
- **Output**: This function does not return any value; it modifies the internal state of the `FormatterBase` object by setting the `description_paragraph_width_` member variable.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::footer\_paragraph\_width<!-- {{#callable:CLI::FormatterBase::footer_paragraph_width}} -->
The `footer_paragraph_width` function sets the width of the footer paragraph in the help output of a command-line interface.
- **Inputs**:
    - `val`: A `std::size_t` value representing the desired width of the footer paragraph.
- **Control Flow**:
    - The function assigns the input value `val` to the member variable `footer_paragraph_width_`.
- **Output**: This function does not return any value.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::enable\_description\_formatting<!-- {{#callable:CLI::FormatterBase::enable_description_formatting}} -->
The `enable_description_formatting` function sets the state of the `enable_description_formatting_` flag, which controls whether description paragraph formatting is enabled in the `FormatterBase` class.
- **Inputs**:
    - `value`: A boolean value that determines whether description formatting should be enabled (default is true).
- **Control Flow**:
    - The function takes a boolean input `value`, which defaults to true if not provided.
    - It assigns the input `value` to the `enable_description_formatting_` member variable of the `FormatterBase` class.
- **Output**: The function does not return any value; it modifies the state of the `enable_description_formatting_` member variable.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)


---
#### FormatterBase::enable\_footer\_formatting<!-- {{#callable:CLI::FormatterBase::enable_footer_formatting}} -->
The `enable_footer_formatting` function sets the state of footer formatting in the `FormatterBase` class.
- **Inputs**:
    - `value`: A boolean value that determines whether footer formatting should be enabled or disabled; defaults to `true` if not provided.
- **Control Flow**:
    - The function assigns the input boolean value to the `enable_footer_formatting_` member variable of the `FormatterBase` class.
- **Output**: This function does not return any value.
- **See also**: [`CLI::FormatterBase`](#CLIFormatterBase)  (Data Structure)



---
### FormatterLambda<!-- {{#data_structure:FormatterLambda}} -->
- **Type**: `class`
- **Members**:
    - `lambda_`: A function object (lambda) that is stored and executed by the class.
- **Description**: The `FormatterLambda` class is a specialized formatter class that inherits from `FormatterBase` and is designed to hold and execute a lambda function for generating help text. It encapsulates a lambda function, defined as `funct_t`, which takes a pointer to an `App`, a `std::string`, and an `AppFormatMode` as parameters, and returns a `std::string`. This class provides a constructor to initialize the lambda function and overrides the `make_help` method to execute the stored lambda, allowing for custom help formatting logic to be easily integrated into the CLI application.
- **Member Functions**:
    - [`FormatterLambda::FormatterLambda`](#FormatterLambdaFormatterLambda)
    - [`FormatterLambda::~FormatterLambda`](#FormatterLambdaFormatterLambda)
    - [`FormatterLambda::make_help`](#FormatterLambdamake_help)
- **Inherits From**:
    - [`CLI::FormatterBase::FormatterBase`](#FormatterBaseFormatterBase)

**Methods**

---
#### FormatterLambda::FormatterLambda<!-- {{#callable:FormatterLambda::FormatterLambda}} -->
The `FormatterLambda` constructor initializes an instance with a lambda function that formats help text for a CLI application.
- **Inputs**:
    - `funct`: A lambda function of type `funct_t`, which is a `std::function` that takes a pointer to an `App`, a `std::string`, and an `AppFormatMode`, and returns a `std::string`.
- **Control Flow**:
    - The constructor takes a lambda function as an argument.
    - It initializes the member variable `lambda_` by moving the provided lambda function into it.
- **Output**: An instance of `FormatterLambda` with the provided lambda function stored for later use in formatting help text.
- **See also**: [`FormatterLambda`](#FormatterLambda)  (Data Structure)


---
#### FormatterLambda::\~FormatterLambda<!-- {{#callable:FormatterLambda::~FormatterLambda}} -->
The `~FormatterLambda` function is a destructor for the `FormatterLambda` class, ensuring proper cleanup of resources when an object of this class is destroyed.
- **Inputs**: None
- **Control Flow**:
    - The destructor `~FormatterLambda` is defined as `noexcept`, indicating it will not throw exceptions during its execution.
    - The destructor overrides the base class `FormatterBase` destructor, ensuring that any specific cleanup logic for `FormatterLambda` is executed when an object of this class is destroyed.
    - The destructor is explicitly defined, although it is empty, primarily to address compatibility issues with GCC 4.7.
- **Output**: The destructor does not return any value, as is typical for destructors in C++.
- **See also**: [`FormatterLambda`](#FormatterLambda)  (Data Structure)


---
#### FormatterLambda::make\_help<!-- {{#callable:FormatterLambda::make_help}} -->
The `make_help` function calls a stored lambda function to generate help text for a given application, name, and format mode.
- **Inputs**:
    - `app`: A pointer to an `App` object representing the application for which help is being generated.
    - `name`: A `std::string` representing the name associated with the help request.
    - `mode`: An `AppFormatMode` enum value indicating the format mode for the help output.
- **Control Flow**:
    - The function directly calls the stored lambda function `lambda_` with the provided `app`, `name`, and `mode` arguments.
    - The lambda function is expected to return a `std::string` which is then returned by `make_help`.
- **Output**: A `std::string` containing the help text generated by the lambda function.
- **See also**: [`FormatterLambda`](#FormatterLambda)  (Data Structure)



---
### Formatter<!-- {{#data_structure:Formatter}} -->
- **Type**: `class`
- **Description**: The `Formatter` class is a specialized class within the CLI namespace that extends the `FormatterBase` class, providing a customizable way to format and display help information for command-line applications. It includes a variety of virtual methods that can be overridden to customize the output of groups, subcommands, options, and other help-related text. The class is designed to be flexible and allows for detailed formatting of command-line interface help, making it easier for users to understand the available commands and options.
- **Member Functions**:
    - [`Formatter::Formatter`](#FormatterFormatter)
    - [`Formatter::Formatter`](#FormatterFormatter)
    - [`Formatter::Formatter`](#FormatterFormatter)
    - [`Formatter::operator=`](#Formatteroperator=)
    - [`Formatter::operator=`](#Formatteroperator=)
- **Inherits From**:
    - [`CLI::FormatterBase::FormatterBase`](#FormatterBaseFormatterBase)

**Methods**

---
#### Formatter::Formatter<!-- {{#callable:Formatter::Formatter}} -->
The `Formatter` class is a default constructor and copy constructor for a class that extends `FormatterBase`, providing a customizable interface for formatting help output in a command-line interface application.
- **Inputs**: None
- **Control Flow**:
    - The `Formatter` class is defined as a subclass of `FormatterBase`.
    - The class provides a default constructor and a copy constructor, both of which are defaulted, meaning they use the compiler-generated versions.
    - The class also provides a move constructor and assignment operators, all of which are defaulted.
    - The class includes several virtual methods that can be overridden to customize the formatting of help output, such as `make_group`, `make_positionals`, `make_groups`, `make_subcommands`, `make_subcommand`, `make_expanded`, `make_footer`, `make_description`, `make_usage`, `make_help`, `make_option`, `make_option_name`, `make_option_opts`, `make_option_desc`, and `make_option_usage`.
- **Output**: The `Formatter` class itself does not produce any output directly, but its methods are designed to return formatted strings representing various parts of a command-line interface help output.
- **See also**: [`Formatter`](#Formatter)  (Data Structure)


---
#### Formatter::Formatter<!-- {{#callable:Formatter::Formatter}} -->
The `Formatter` class provides a default implementation for formatting help output in a command-line interface, with various methods to customize the display of options, subcommands, and descriptions.
- **Inputs**: None
- **Control Flow**:
    - The `Formatter` class is derived from `FormatterBase` and inherits its properties and methods.
    - It provides default implementations for copy and move constructors, as well as copy and move assignment operators.
    - The class contains several virtual methods that can be overridden to customize the formatting of help output, such as `make_group`, `make_positionals`, `make_subcommands`, and others.
    - The `make_help` method is overridden to provide a complete help message by assembling various components like groups, subcommands, and options.
- **Output**: The `Formatter` class outputs formatted strings representing help information for command-line applications, including options, subcommands, and descriptions.
- **See also**: [`Formatter`](#Formatter)  (Data Structure)


---
#### Formatter::Formatter<!-- {{#callable:Formatter::Formatter}} -->
The `Formatter` class provides default move constructor and move assignment operator implementations for handling move semantics.
- **Inputs**:
    - `Formatter &&`: A rvalue reference to a `Formatter` object, used in the move constructor.
- **Control Flow**:
    - The move constructor `Formatter(Formatter &&) = default;` is defined, which allows the creation of a new `Formatter` object by transferring resources from an existing rvalue `Formatter` object.
    - The move assignment operator `Formatter &operator=(Formatter &&) = default;` is defined, which allows an existing `Formatter` object to take ownership of resources from an rvalue `Formatter` object.
- **Output**: The function does not produce any output as it is a constructor and assignment operator, but it results in a `Formatter` object being moved.
- **See also**: [`Formatter`](#Formatter)  (Data Structure)


---
#### Formatter::operator=<!-- {{#callable:Formatter::operator=}} -->
The `operator=` function in the `Formatter` class is a default assignment operator that allows for both copy and move assignment of `Formatter` objects.
- **Inputs**:
    - `const Formatter &`: A constant reference to another `Formatter` object for copy assignment.
    - `Formatter &&`: An rvalue reference to another `Formatter` object for move assignment.
- **Control Flow**:
    - The function is defined as `default`, meaning it uses the compiler-generated default behavior for assignment operators.
    - It allows the `Formatter` class to be assigned from another `Formatter` object, either by copying or moving, depending on the context.
- **Output**: The function returns a reference to the current `Formatter` object after assignment.
- **See also**: [`Formatter`](#Formatter)  (Data Structure)


---
#### Formatter::operator=<!-- {{#callable:Formatter::operator=}} -->
The `operator=` function is a default move assignment operator for the `Formatter` class, allowing for efficient transfer of resources from a temporary `Formatter` object to another `Formatter` instance.
- **Inputs**:
    - `Formatter &&`: A temporary `Formatter` object from which resources will be moved.
- **Control Flow**:
    - The function is defined as `default`, meaning it uses the compiler-generated move assignment operator.
    - The function transfers resources from the temporary `Formatter` object to the current instance, leaving the temporary object in a valid but unspecified state.
- **Output**: A reference to the current `Formatter` instance after the move assignment.
- **See also**: [`Formatter`](#Formatter)  (Data Structure)



# Functions

---
### get\_column\_width<!-- {{#callable:CLI::CLI11_NODISCARD::size_t::get_column_width}} -->
The `get_column_width` function retrieves the current width of the left column used for options, flags, or subcommands in a formatted help output.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `column_width_` member variable, which represents the width of the left column.
- **Output**: The function returns a `std::size_t` representing the current width of the left column.


---
### get\_right\_column\_width<!-- {{#callable:CLI::std::size_t::get_right_column_width}} -->
The `get_right_column_width` function returns the current width of the right column used for descriptions in the help formatter.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the `right_column_width_` member variable.
- **Output**: The function outputs a `std::size_t` representing the width of the right column for descriptions.


---
### get\_description\_paragraph\_width<!-- {{#callable:CLI::std::size_t::get_description_paragraph_width}} -->
The `get_description_paragraph_width` function returns the current width setting for the description paragraph in the help output.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `description_paragraph_width_`.
- **Output**: The function outputs a `std::size_t` representing the width of the description paragraph.


---
### get\_footer\_paragraph\_width<!-- {{#callable:CLI::std::size_t::get_footer_paragraph_width}} -->
The `get_footer_paragraph_width` function returns the current width setting for the footer paragraph in the help formatter.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `footer_paragraph_width_`.
- **Output**: The function outputs a `std::size_t` representing the width of the footer paragraph.


---
### is\_description\_paragraph\_formatting\_enabled<!-- {{#callable:CLI::is_description_paragraph_formatting_enabled}} -->
The function `is_description_paragraph_formatting_enabled` checks if the description paragraph formatting is enabled in the `FormatterBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `enable_description_formatting_`.
- **Output**: A boolean value indicating whether description paragraph formatting is enabled.


---
### is\_footer\_paragraph\_formatting\_enabled<!-- {{#callable:CLI::is_footer_paragraph_formatting_enabled}} -->
The function `is_footer_paragraph_formatting_enabled` checks if footer paragraph formatting is enabled in the `FormatterBase` class.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter method that returns the value of the private member variable `enable_footer_formatting_`.
- **Output**: A boolean value indicating whether footer paragraph formatting is enabled.


---
### FormatterBase<!-- {{#callable:CLI::FormatterBase::FormatterBase}} -->
The `FormatterBase` class provides a base interface for creating custom formatters for help messages in the CLI11 library.
- **Inputs**: None
- **Control Flow**:
    - The default constructor `FormatterBase()` is defined, which initializes an instance of the class with default values.
    - The copy constructor `FormatterBase(const FormatterBase &)` is defined, allowing for the creation of a new `FormatterBase` object as a copy of an existing one.
- **Output**: The constructors do not return any value as they are used to initialize objects of the `FormatterBase` class.


