# Purpose
This C++ source code file is an executable program that utilizes the CLI11 library to create a command-line interface for drawing geometric shapes. The program defines a main function that sets up a CLI application named "load shapes," which supports subcommands for drawing circles, rectangles, and triangles. Each subcommand is associated with specific options that allow users to specify the dimensions of the shapes, such as the radius for circles and edge lengths for rectangles and triangles. The program uses immediate callbacks to execute the drawing logic as soon as a subcommand is invoked, and it outputs the details of the shapes to the console.

The code provides a focused functionality centered around shape drawing through a command-line interface. The most important technical components include the use of the CLI11 library for parsing command-line arguments and managing subcommands, as well as the use of lambda functions for handling the logic associated with each shape. The program defines a public interface for users to interact with via the command line, allowing them to specify parameters for each shape and receive output directly in the console. This file is a standalone executable, as indicated by the presence of the main function, and it does not define any external APIs or interfaces beyond the command-line options it provides.
# Imports and Dependencies

---
- `CLI/CLI.hpp`
- `iostream`
- `vector`


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function initializes a command-line interface application to draw shapes (circle, rectangle, triangle) based on user input, and outputs the details of each shape drawn.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of C-style strings representing the command-line arguments.
- **Control Flow**:
    - Initialize a CLI application with the description 'load shapes'.
    - Set a global help flag '--help-all' for the application.
    - Add a 'circle' subcommand with an immediate callback to draw a circle, requiring a 'radius' option.
    - Define a callback for the 'circle' subcommand that increments a counter and prints the circle's radius.
    - Add a 'rectangle' subcommand with an immediate callback to draw a rectangle, requiring 'edge1' and optionally 'edge2'.
    - Define a callback for the 'rectangle' subcommand that increments a counter, checks if 'edge2' is zero to set it equal to 'edge1', and prints the rectangle's edges.
    - Add a 'triangle' subcommand with an immediate callback to draw a triangle, accepting multiple 'sides'.
    - Define a callback for the 'triangle' subcommand that increments a counter and prints the triangle's sides.
    - Parse the command-line arguments using `CLI11_PARSE` to execute the appropriate subcommand based on user input.
- **Output**: The function returns an integer value of 0, indicating successful execution.


