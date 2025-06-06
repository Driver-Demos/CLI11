# Purpose
This code is a C++ header file, likely part of a library, designed to be included in other projects. It provides narrow functionality related to command-line interface (CLI) processing, specifically handling command-line arguments. The code includes platform-specific functionality for Windows, where it defines a function to decode and return UTF-8 encoded command-line arguments using `GetCommandLineW`. The use of `#pragma once` and conditional compilation directives like `#ifdef _WIN32` and `#ifndef CLI11_COMPILE` suggest that this file is intended to be included multiple times without causing redefinition errors and to conditionally include implementation details. The inclusion of "Macros.hpp" and "impl/Argv_inl.hpp" indicates modular design, separating interface from implementation, which is typical in library development.
# Imports and Dependencies

---
- `string`
- `vector`
- `Macros.hpp`
- `impl/Argv_inl.hpp`


