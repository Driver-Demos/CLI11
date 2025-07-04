# Purpose
This C++ source code file defines a utility for timing operations, encapsulated within the `CLI` namespace. The primary class, [`Timer`](#TimerTimer), provides functionality to measure elapsed time and format it into a human-readable string. It uses the `std::chrono` library to track time intervals and offers customizable output through user-defined formatting functions. The [`Timer`](#TimerTimer) class includes methods to start timing upon instantiation, measure the duration of a function execution, and format the elapsed time in various units (nanoseconds, microseconds, milliseconds, or seconds) based on the duration. Additionally, the file defines an [`AutoTimer`](#AutoTimerAutoTimer) class, which inherits from [`Timer`](#TimerTimer) and automatically prints the elapsed time upon destruction, making it useful for scope-based timing.

The file is structured as a C++ header file, intended to be included in other projects that require timing functionality. It provides a public API through the [`Timer`](#TimerTimer) and [`AutoTimer`](#AutoTimerAutoTimer) classes, allowing users to instantiate timers, measure execution times, and output formatted timing results. The file also includes a custom stream insertion operator for the [`Timer`](#TimerTimer) class, enabling easy integration with standard output streams like `std::cout`. The code is designed to be portable and compatible with older versions of GCC by conditionally defining missing macros, ensuring broader usability across different compiler environments.
# Imports and Dependencies

---
- `cmath`
- `array`
- `chrono`
- `cstdio`
- `functional`
- `iostream`
- `string`
- `utility`


# Data Structures

---
### Timer<!-- {{#data_structure:CLI::Timer}} -->
- **Type**: `class`
- **Members**:
    - `title_`: This is the title of the timer.
    - `time_print_`: This is the function that is used to format most of the timing message.
    - `start_`: This is the starting point (when the timer was created).
    - `cycles`: This is the number of times cycles (print divides by this number).
- **Description**: The `Timer` class is a utility for measuring and formatting time intervals in a program. It uses the `std::chrono::steady_clock` to track time and provides customizable output formatting through a function pointer `time_print_t`. The class includes a default constructor that initializes the timer with a title and a print function, and it offers methods to time a function execution, format the elapsed time into a string, and output the timing information. The class also supports division of the timing result by a specified number of cycles, allowing for averaged timing results.
- **Member Functions**:
    - [`CLI::Timer::Simple`](#TimerSimple)
    - [`CLI::Timer::Big`](#TimerBig)
    - [`CLI::Timer::Timer`](#TimerTimer)
    - [`CLI::Timer::time_it`](#Timertime_it)
    - [`CLI::Timer::make_time_str`](#Timermake_time_str)
    - [`CLI::Timer::make_time_str`](#Timermake_time_str)
    - [`CLI::Timer::to_string`](#Timerto_string)
    - [`CLI::Timer::operator/`](#Timeroperator/)

**Methods**

---
#### Timer::Simple<!-- {{#callable:CLI::Timer::Simple}} -->
The `Simple` function concatenates a title and a time string with a colon separator.
- **Inputs**:
    - `title`: A string representing the title to be used in the output.
    - `time`: A string representing the time to be used in the output.
- **Control Flow**:
    - The function takes two string inputs, `title` and `time`.
    - It concatenates these two strings with a colon and a space in between.
- **Output**: A single string that combines the title and time with a colon and space separator.
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::Big<!-- {{#callable:CLI::Timer::Big}} -->
The `Big` function formats a title and time string into a visually distinct block with header and footer lines for emphasis.
- **Inputs**:
    - `title`: A string representing the title to be included in the formatted output.
    - `time`: A string representing the time to be included in the formatted output.
- **Control Flow**:
    - The function constructs a string by concatenating a header line, the title and time formatted within a bordered line, and a footer line.
    - The header and footer lines consist of a series of dashes to create a visual block around the title and time.
- **Output**: A formatted string that includes the title and time within a bordered block of text.
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::Timer<!-- {{#callable:CLI::Timer::Timer}} -->
The `Timer` constructor initializes a timer object with a specified title and a function for formatting the timing message, starting the timer upon creation.
- **Inputs**:
    - `title`: A string representing the title of the timer, defaulting to "Timer".
    - `time_print`: A function of type `time_print_t` used to format the timing message, defaulting to the `Simple` function.
- **Control Flow**:
    - The constructor initializes the `title_` member with the provided title, using `std::move` to efficiently transfer ownership.
    - The `time_print_` member is initialized with the provided `time_print` function, also using `std::move`.
    - The `start_` member is set to the current time using `clock::now()`, marking the start of the timer.
- **Output**: The constructor does not return any value as it is used to initialize an instance of the `Timer` class.
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::time\_it<!-- {{#callable:CLI::Timer::time_it}} -->
The `time_it` function measures the execution time of a given function by running it multiple times until a specified target time is reached or a maximum of 100 iterations is completed, and returns a formatted string of the average execution time and the number of tries.
- **Inputs**:
    - `f`: A `std::function<void()>` representing the function to be timed.
    - `target_time`: A `double` representing the target time in seconds for which the function should be run; defaults to 1 second.
- **Control Flow**:
    - Initialize `start` with the current value of `start_` and `total_time` with `NAN`.
    - Set `start_` to the current time using `clock::now()`.
    - Initialize a counter `n` to 0.
    - Enter a do-while loop that runs the function `f` and calculates the elapsed time since `start_`.
    - Increment the counter `n` and update `total_time` with the elapsed time.
    - Continue the loop until `n` reaches 100 or `total_time` exceeds `target_time`.
    - Calculate the average time per execution by dividing `total_time` by `n`.
    - Format the average time into a string using [`make_time_str`](#Timermake_time_str) and append the number of tries.
    - Restore `start_` to its original value `start`.
    - Return the formatted string.
- **Output**: A `std::string` containing the average execution time per run and the number of tries.
- **Functions called**:
    - [`CLI::Timer::make_time_str`](#Timermake_time_str)
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::make\_time\_str<!-- {{#callable:CLI::Timer::make_time_str}} -->
The [`make_time_str`](#Timermake_time_str) function calculates the elapsed time since the timer started, divides it by the number of cycles, and returns a formatted time string.
- **Inputs**: None
- **Control Flow**:
    - Capture the current time using `clock::now()` and store it in `stop`.
    - Calculate the elapsed time as the difference between `stop` and `start_`.
    - Divide the elapsed time by the number of `cycles` to get the average time per cycle.
    - Call the overloaded `make_time_str(double time)` function with the calculated average time to get a formatted time string.
- **Output**: A formatted string representing the average elapsed time per cycle.
- **Functions called**:
    - [`CLI::Timer::make_time_str`](#Timermake_time_str)
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::make\_time\_str<!-- {{#callable:CLI::Timer::make_time_str}} -->
The `make_time_str` function formats a given time in seconds into a human-readable string with appropriate time units (ns, us, ms, s).
- **Inputs**:
    - `time`: A double representing the time in seconds to be formatted.
- **Control Flow**:
    - Define a lambda function `print_it` that formats a double value with a unit into a string.
    - Check if `time` is less than 0.000001; if true, convert `time` to nanoseconds and return the formatted string using `print_it`.
    - Check if `time` is less than 0.001; if true, convert `time` to microseconds and return the formatted string using `print_it`.
    - Check if `time` is less than 1; if true, convert `time` to milliseconds and return the formatted string using `print_it`.
    - If none of the above conditions are met, return the formatted string using `print_it` with seconds as the unit.
- **Output**: A string representing the formatted time with the appropriate unit.
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::to\_string<!-- {{#callable:CLI::Timer::to_string}} -->
The `to_string` method generates a formatted string representation of the timer's title and elapsed time.
- **Inputs**: None
- **Control Flow**:
    - The method calls `make_time_str()` to get the formatted elapsed time as a string.
    - It then uses the `time_print_` function, which is a user-defined or default formatting function, to combine the `title_` and the formatted time string into a single output string.
- **Output**: A `std::string` that contains the formatted title and elapsed time of the timer.
- **Functions called**:
    - [`CLI::Timer::make_time_str`](#Timermake_time_str)
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)


---
#### Timer::operator/<!-- {{#callable:CLI::Timer::operator/}} -->
The `operator/` function sets the number of cycles for a `Timer` object, which is used to divide the elapsed time for reporting purposes.
- **Inputs**:
    - `val`: A `std::size_t` value representing the number of cycles to set for the `Timer` object.
- **Control Flow**:
    - The function assigns the input value `val` to the `cycles` member variable of the `Timer` object.
    - The function returns a reference to the current `Timer` object (`*this`).
- **Output**: A reference to the current `Timer` object, allowing for method chaining.
- **See also**: [`CLI::Timer`](#Timer)  (Data Structure)



---
### AutoTimer<!-- {{#data_structure:CLI::AutoTimer}} -->
- **Type**: `class`
- **Description**: The `AutoTimer` class is a specialized timer that inherits from the `Timer` class and is designed to automatically print the elapsed time when an instance of the class is destroyed. It reimplements the constructor to accommodate GCC 4.7 limitations and uses the `Timer` class's functionality to manage timing and formatting. The primary feature of `AutoTimer` is its destructor, which outputs the timing information to the standard output, making it useful for timing code blocks without explicit stop calls.
- **Member Functions**:
    - [`CLI::AutoTimer::AutoTimer`](#AutoTimerAutoTimer)
    - [`CLI::AutoTimer::~AutoTimer`](#AutoTimerAutoTimer)
- **Inherits From**:
    - [`CLI::Timer::Timer`](#TimerTimer)

**Methods**

---
#### AutoTimer::AutoTimer<!-- {{#callable:CLI::AutoTimer::AutoTimer}} -->
The `AutoTimer` constructor initializes an `AutoTimer` object with a title and a time printing function, inheriting from the `Timer` class.
- **Inputs**:
    - `title`: A string representing the title of the timer, defaulting to "Timer".
    - `time_print`: A function of type `time_print_t` used to format the timing message, defaulting to the `Simple` function.
- **Control Flow**:
    - The constructor is explicitly defined to handle compatibility with GCC 4.7, which does not support inheriting constructors.
    - It calls the base class `Timer` constructor with the provided `title` and `time_print` arguments.
- **Output**: An `AutoTimer` object is created and initialized with the specified title and time printing function.
- **See also**: [`CLI::AutoTimer`](#AutoTimer)  (Data Structure)


---
#### AutoTimer::\~AutoTimer<!-- {{#callable:CLI::AutoTimer::~AutoTimer}} -->
The destructor of the `AutoTimer` class outputs the formatted timing string to the standard output when an `AutoTimer` object is destroyed.
- **Inputs**: None
- **Control Flow**:
    - The destructor `~AutoTimer()` is called when an `AutoTimer` object goes out of scope or is explicitly deleted.
    - Inside the destructor, the `to_string()` method of the `Timer` class is called to generate a formatted string representing the elapsed time.
    - The formatted string is then output to the standard output stream using `std::cout`.
- **Output**: The function outputs a formatted string representing the elapsed time to the standard output.
- **Functions called**:
    - [`CLI::Timer::to_string`](#Timerto_string)
- **See also**: [`CLI::AutoTimer`](#AutoTimer)  (Data Structure)



# Functions

---
### operator<<<!-- {{#callable:operator<<}} -->
The `operator<<` function overloads the insertion operator to output a `CLI::Timer` object to a stream by converting it to a string.
- **Inputs**:
    - `in`: A reference to an output stream (e.g., `std::cout`) where the timer's string representation will be inserted.
    - `timer`: A constant reference to a `CLI::Timer` object whose string representation is to be output to the stream.
- **Control Flow**:
    - The function takes an output stream and a `CLI::Timer` object as parameters.
    - It calls the `to_string()` method on the `timer` object to get its string representation.
    - The resulting string is inserted into the output stream `in`.
    - The function returns the modified output stream.
- **Output**: A reference to the output stream `in` after the timer's string representation has been inserted.


---
### Timer<!-- {{#callable:CLI::Timer::Timer}} -->
The `Timer` constructor initializes a timer object with a specified title and a function for formatting the time output, starting the timer upon creation.
- **Inputs**:
    - `title`: A string representing the title of the timer, defaulting to "Timer".
    - `time_print`: A function of type `time_print_t` used to format the timing message, defaulting to the `Simple` function.
- **Control Flow**:
    - The constructor initializes the `title_` member with the provided title, using `std::move` for efficient string handling.
    - The `time_print_` member is initialized with the provided time formatting function, also using `std::move`.
    - The `start_` member is set to the current time using `clock::now()`, marking the start of the timer.
- **Output**: The constructor does not return a value; it initializes the `Timer` object.


