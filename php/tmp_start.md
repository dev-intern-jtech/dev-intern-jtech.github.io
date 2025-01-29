##### [tmp_start.php](#tmp_startphp)
- **Purpose**: Temporary or initial setup script, might be used for bootstrapping or testing environments. This file initializes debugging and performance profiling when necessary, and starts timing the execution of the script or application.

  **Fields**:
  - `$doDebug`: Boolean to toggle debugging on or off. When `true`, it activates profiling and other debug functionalities.
  - `$MEOWt1`: Float, stores the start time of the script execution in microseconds, used for performance measurement.

  **Additional Notes**:
  - **Debugging**: The file uses XHProf for profiling when `$doDebug` is set to `true`. XHProf is enabled with flags to track both CPU time and memory usage, allowing for comprehensive performance analysis.
  - **Performance Timing**: `$MEOWt1` is set with `microtime(true)` to mark the beginning of execution time measurement, which could be used later to calculate the total execution time of the script or application.
