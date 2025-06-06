# Purpose
This Python script is designed to extract version information from a C++ header file, specifically `Version.hpp`, which is located in a directory structure relative to the script's location. The script uses regular expressions to parse the file for preprocessor directives that define version numbers (`MAJOR`, `MINOR`, `PATCH`) and then prints these numbers in a standard version format. This code provides narrow functionality, focusing solely on reading and interpreting version information from a specific file, making it a utility script for version management in a software project. The script is useful for automating the retrieval of version data, which can be integrated into build processes or documentation generation.
# Imports and Dependencies

---
- `os`
- `re`


# Global Variables

---
### base\_path
- **Type**: `str`
- **Description**: The `base_path` variable is a string that represents the absolute path to the parent directory of the current file's directory. It is constructed using the `os.path.abspath` and `os.path.join` functions to navigate up one directory level from the directory containing the current script file.
- **Use**: This variable is used as a base directory path to construct other file paths, such as `config_h`, which points to a specific header file within the project structure.


---
### config\_h
- **Type**: `str`
- **Description**: The variable `config_h` is a string that represents the file path to the 'Version.hpp' file located within the 'include/CLI' directory relative to the base path of the project. This path is constructed using the `os.path.join` method to ensure compatibility across different operating systems.
- **Use**: This variable is used to open and read the 'Version.hpp' file to extract version information.


---
### data
- **Type**: `dict`
- **Description**: The `data` variable is a dictionary that holds version information with keys 'MAJOR', 'MINOR', and 'PATCH', each initialized to 0. It is used to store version numbers extracted from a configuration file.
- **Use**: This variable is used to store and update the version components of a software package by parsing a specific header file.


---
### reg
- **Type**: `re.Pattern`
- **Description**: The variable `reg` is a compiled regular expression pattern used to match lines in a file that define version components of the CLI11 library. It specifically looks for lines that start with '#define', followed by 'CLI11_VERSION_', a version component name (e.g., MAJOR, MINOR, PATCH), and a numeric value.
- **Use**: This variable is used to extract version information from a header file by matching and capturing the version component names and their corresponding numeric values.


