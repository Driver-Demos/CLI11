# Purpose
The file defines a sequence of steps for a build pipeline. The first step executes a script to run tests using `ctest`, displaying output on failure, and operates within the `build` directory. The second step publishes the test results, specifying the format as "cTest" and targeting files matching the pattern `**/Test.xml`.
