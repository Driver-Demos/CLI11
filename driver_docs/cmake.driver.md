
## Files
- **[CLI11.pc.in](cmake/CLI11.pc.in.driver.md)**: The `CLI11.pc.in` file is a template for generating a pkg-config file for the CLI11 C++ command line parser, specifying installation paths and compiler flags.
- **[CLI11ConfigVersion.cmake.in](cmake/CLI11ConfigVersion.cmake.in.driver.md)**: The `CLI11ConfigVersion.cmake.in` file is a CMake script that sets compatibility and exactness flags based on the package version for the `CLI11` library.
- **[CLI11GeneratePkgConfig.cmake](cmake/CLI11GeneratePkgConfig.cmake.driver.md)**: The `CLI11GeneratePkgConfig.cmake` file is responsible for generating and installing the `CLI11.pc` pkg-config file based on whether the CLI11 library is precompiled or not.
- **[CLI11precompiled.pc.in](cmake/CLI11precompiled.pc.in.driver.md)**: The `CLI11precompiled.pc.in` file is a template for generating a pkg-config file for the CLI11 C++ command line parser, specifying installation paths and compilation flags.
- **[CLI11Warnings.cmake](cmake/CLI11Warnings.cmake.driver.md)**: The `CLI11Warnings.cmake` file defines a special target for adding compiler warnings to the CLI11 project, with specific configurations for different compilers such as Clang and GCC.
- **[CodeCoverage.cmake](cmake/CodeCoverage.cmake.driver.md)**: The `CodeCoverage.cmake` file in the `CLI11` codebase provides CMake functions and configurations to enable and manage code coverage reporting for C, C++, and Fortran projects, supporting various tools like gcov, lcov, gcovr, and fastcov, with options for generating reports in multiple formats.
