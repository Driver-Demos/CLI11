# Purpose
This C++ source code file is designed to facilitate testing and utility functions for applications using the CLI11 library, a command-line interface parser. The file includes several components that serve distinct purposes, such as the `TApp` class, which encapsulates a CLI11 application for testing purposes. This class allows for the parsing of command-line arguments, demonstrating the use of CLI11's parsing capabilities. Additionally, the file provides utility functions for environment variable manipulation ([`put_env`](#put_env) and [`unset_env`](#unset_env)), which are platform-specific to accommodate both Windows and Unix-like systems. These functions are crucial for setting up and tearing down test environments.

The file also includes a [`TempFile`](#TempFileTempFile) class, which manages temporary files by ensuring they are deleted upon destruction, thus aiding in resource management during tests. Furthermore, the file contains functions for compatibility with C++20's `char8_t` type, ensuring smooth string conversions. A notable feature is the [`check_identical_files`](#check_identical_files) function, which compares two files byte-by-byte to verify their identical nature, a useful utility in testing scenarios where file integrity is crucial. Overall, this file provides a collection of utilities and test support functions centered around the CLI11 library, enhancing the testing and development process for command-line applications.
# Imports and Dependencies

---
- `CLI11.hpp`
- `CLI/CLI.hpp`
- `catch.hpp`
- `array`
- `fstream`
- `iomanip`
- `iostream`
- `string`
- `utility`
- `vector`


# Data Structures

---
### TApp<!-- {{#data_structure:TApp}} -->
- **Type**: `class`
- **Members**:
    - `app`: An instance of CLI::App initialized with the description 'My Test Program'.
    - `args`: A vector of strings used to store input arguments.
- **Description**: The TApp class is designed to encapsulate a command-line interface application using the CLI11 library. It contains an instance of CLI::App to manage the application's command-line options and arguments, and a vector of strings to hold the input arguments. The class provides a run method that reverses the input arguments and parses them using the CLI::App instance, allowing for flexible command-line argument handling.
- **Member Functions**:
    - [`TApp::~TApp`](#TAppTApp)
    - [`TApp::run`](#TApprun)

**Methods**

---
#### TApp::\~TApp<!-- {{#callable:TApp::~TApp}} -->
The destructor `~TApp` is a virtual default destructor for the `TApp` class, ensuring proper cleanup in derived classes.
- **Inputs**: None
- **Control Flow**:
    - The destructor is declared as virtual to allow derived class destructors to be called correctly.
    - The destructor is defined as default, indicating that the compiler should generate the default implementation.
- **Output**: There is no explicit output from the destructor; it ensures proper resource cleanup when an object of `TApp` or its derived class is destroyed.
- **See also**: [`TApp`](#TApp)  (Data Structure)


---
#### TApp::run<!-- {{#callable:TApp::run}} -->
The `run` function reverses the order of command-line arguments and parses them using the CLI11 library.
- **Inputs**: None
- **Control Flow**:
    - The function begins by creating a copy of the `args` member variable into a local variable `newargs`.
    - It then reverses the order of elements in `newargs` using `std::reverse`.
    - Finally, it calls the `parse` method on the `app` object, passing the reversed `newargs` as an argument.
- **Output**: The function does not return any value; it performs operations on the `app` object.
- **See also**: [`TApp`](#TApp)  (Data Structure)



---
### TempFile<!-- {{#data_structure:TempFile}} -->
- **Type**: `class`
- **Members**:
    - `_name`: A private member variable that stores the name of the temporary file as a string.
- **Description**: The `TempFile` class is designed to manage temporary files by storing the file's name and ensuring its deletion upon object destruction. It takes a file name as a parameter during construction and checks if the path is nonexistent, throwing an exception if it is not. The destructor automatically removes the file, and the class provides conversion to a `std::string` reference and a method to get the C-style string representation of the file name.
- **Member Functions**:
    - [`TempFile::TempFile`](#TempFileTempFile)
    - [`TempFile::~TempFile`](#TempFileTempFile)
    - [`TempFile::c_str`](#TempFilec_str)

**Methods**

---
#### TempFile::TempFile<!-- {{#callable:TempFile::TempFile}} -->
The `TempFile` constructor initializes a temporary file object with a given name and ensures the file does not already exist, throwing an exception if it does.
- **Inputs**:
    - `name`: A string representing the name of the temporary file to be created.
- **Control Flow**:
    - The constructor initializes the `_name` member variable with the provided `name` argument using `std::move`.
    - It checks if the path specified by `_name` already exists using `CLI::NonexistentPath`.
    - If the path is not empty (indicating the file already exists), it throws a `std::runtime_error` with the file name.
- **Output**: The constructor does not return a value, but it initializes the `TempFile` object and may throw an exception if the file already exists.
- **See also**: [`TempFile`](#TempFile)  (Data Structure)


---
#### TempFile::\~TempFile<!-- {{#callable:TempFile::~TempFile}} -->
The destructor `~TempFile` removes the temporary file associated with the `TempFile` object upon its destruction.
- **Inputs**: None
- **Control Flow**:
    - The destructor is called when a `TempFile` object goes out of scope or is explicitly deleted.
    - The `std::remove` function is invoked with the file name stored in `_name` to delete the file from the filesystem.
    - The return value of `std::remove` is ignored, meaning any error in file deletion is not handled.
- **Output**: There is no output from this function as it is a destructor.
- **See also**: [`TempFile`](#TempFile)  (Data Structure)


---
#### TempFile::c\_str<!-- {{#callable:TempFile::c_str}} -->
The `c_str` function returns a C-style string representation of the `_name` member variable of the `TempFile` class.
- **Inputs**: None
- **Control Flow**:
    - The function directly calls the `c_str()` method on the `_name` member variable, which is a `std::string`, to obtain a C-style string pointer.
    - The function then returns this C-style string pointer.
- **Output**: A `const char*` pointer to the C-style string representation of the `_name` member variable.
- **See also**: [`TempFile`](#TempFile)  (Data Structure)



# Functions

---
### fileClear<!-- {{#callable:fileClear}} -->
The `fileClear` function attempts to delete a file specified by its name.
- **Inputs**:
    - `name`: A constant reference to a `std::string` representing the name of the file to be deleted.
- **Control Flow**:
    - The function calls `std::remove` with the C-style string representation of the file name to attempt to delete the file.
- **Output**: An integer value is returned, which is the result of the `std::remove` function; typically, 0 indicates success, and a non-zero value indicates failure.


---
### put\_env<!-- {{#callable:put_env}} -->
The `put_env` function sets an environment variable to a specified value, with platform-specific implementations for Windows and other systems.
- **Inputs**:
    - `name`: A string representing the name of the environment variable to set.
    - `value`: A string representing the value to assign to the environment variable.
- **Control Flow**:
    - The function checks if the code is being compiled on a Windows platform using the `_WIN32` preprocessor directive.
    - If on Windows, it uses the `_putenv_s` function to set the environment variable with the given name and value.
    - If not on Windows, it uses the `setenv` function to set the environment variable, with the overwrite flag set to 1 to allow overwriting existing values.
- **Output**: The function does not return any value.


---
### unset\_env<!-- {{#callable:unset_env}} -->
The `unset_env` function removes an environment variable by name, with platform-specific implementations for Windows and other systems.
- **Inputs**:
    - `name`: A string representing the name of the environment variable to be removed.
- **Control Flow**:
    - The function checks if the code is being compiled on a Windows platform using the `_WIN32` preprocessor directive.
    - If on Windows, it uses the `_putenv_s` function to set the environment variable to an empty string, effectively removing it.
    - If not on Windows, it uses the `unsetenv` function to remove the environment variable.
- **Output**: The function does not return any value.


---
### from\_u8string<!-- {{#callable:std::string::from_u8string}} -->
The function `from_u8string` converts a C++20 `char8_t` string to a standard `std::string` by reinterpret casting the input pointer to a `const char *`.
- **Inputs**:
    - `s`: A pointer to a `char8_t` string that needs to be converted to a `std::string`.
- **Control Flow**:
    - The function takes a `char8_t` pointer as input.
    - It uses `reinterpret_cast` to cast the `char8_t` pointer to a `const char *` pointer.
    - A `std::string` is constructed using the casted `const char *` pointer.
    - The constructed `std::string` is returned.
- **Output**: A `std::string` that represents the same sequence of characters as the input `char8_t` string.


---
### check\_identical\_files<!-- {{#callable:check_identical_files}} -->
The `check_identical_files` function compares two files byte-by-byte to ensure they are identical, failing if any discrepancies are found.
- **Inputs**:
    - `path1`: A C-style string representing the path to the first file to be compared.
    - `path2`: A C-style string representing the path to the second file to be compared.
- **Control Flow**:
    - Check if the first file exists using `CLI::ExistingFile` and fail if it doesn't.
    - Check if the second file exists using `CLI::ExistingFile` and fail if it doesn't.
    - Open both files in binary mode and position the read pointer at the end to compare their sizes.
    - Fail if either file is corrupted or if their sizes differ.
    - Rewind both files to the beginning for byte-by-byte comparison.
    - Read both files in chunks of 10240 bytes into buffers and compare each byte.
    - Fail if any byte differs between the two files, indicating the position and differing byte values.
- **Output**: The function does not return a value; it uses the `FAIL` macro to indicate errors or discrepancies.


