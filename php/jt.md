##### [jt.php](#jtphp)
- **Purpose**: The main entry point for framework initialization or core operations, managing the overall flow. This file defines the core functionality of the framework, including initialization, configuration, and utility methods.
- **Relationships**: 
  - Calls methods from:
    - [jt_util_controller.php](#jt_util_controllerphp) for utility functions.
    - [jt_db_controller.php](#jt_db_controllerphp) for database operations.
    - [jt_text_controller.php](#jt_text_controllerphp) for text processing.
    - [jt_server_controller.php](#jt_server_controllerphp) for server-related operations.
    - [jt_email_controller.php](#jt_email_controllerphp) for email functionalities.
    - [jt_error_controller.php](#jt_error_controllerphp) for error handling.
    - [jt_session_controller.php](#jt_session_controllerphp) for session management.
    - [jt_data_controller.php](#jt_data_controllerphp) for data operations.
    - [jt_validate_controller.php](#jt_validate_controllerphp) for data validation.
    - [jt_scrub_controller.php](#jt_scrub_controllerphp) for data sanitization.
    - [jt_date_controller.php](#jt_date_controllerphp) for date-related operations.
    - [jt_request_controller.php](#jt_request_controllerphp) for request handling.
    - [jt_security_controller.php](#jt_security_controllerphp) for security features.
    - [jt_image_controller.php](#jt_image_controllerphp) for image processing.
    - [jt_agent_controller.php](#jt_agent_controllerphp) for user agent information.
    - [jt_view_controller.php](#jt_view_controllerphp) for view rendering.
    - [jt_node_controller.php](#jt_node_controllerphp) for Node.js integration.

  **Functions**:
  - `init()`
    - **Purpose**: Initializes the framework by setting up the environment, configuring various controllers, and initializing the request cycle.
    - **Parameters**: None
    - **Returns**: None
    - **Details**: This method sets up timestamp information, determines the environment (CLI or web), configures debugging and flags, sets up the database connection, initializes various controllers, sets up UTF-8 encoding, and triggers framework events. It also handles CLI-specific configurations and sets HTTP headers when not in CLI mode.

  - `setConfig($env, $key, $value, $merge = false)`
    - **Purpose**: Sets configuration values for different environments.
    - **Parameters**: 
      - `$env` - Environment to set the config for (can be an array).
      - `$key` - Configuration key.
      - `$value` - Value to set.
      - `$merge` - Whether to merge the value with existing configuration.
    - **Returns**: None
    - **Details**: Allows setting or merging configuration values for specified environments.

  - `getSiteUrl($input, $toReq = null, $replaceToReq = false)`
    - **Purpose**: Generates the full site URL.
    - **Parameters**: 
      - `$input` - The URL part to append.
      - `$toReq` - Optional request to replace or append to.
      - `$replaceToReq` - Whether to replace or append the request.
    - **Returns**: String - The constructed site URL.

  - `getUrl($input, $toReq = null, $replaceToReq = false)`
    - **Purpose**: Generates a URL within the site based on the input.
    - **Parameters**: 
      - `$input` - The URL part to generate.
      - `$toReq` - Optional request to replace or append to.
      - `$replaceToReq` - Whether to replace or append the request.
    - **Returns**: String - The constructed URL within the site.

  - `setUrl($input, $toReq = null, $replaceToReq = false)`
    - **Purpose**: Sets the URI for the current request.
    - **Parameters**: 
      - `$input` - The URL part to set.
      - `$toReq` - Optional request to replace or append to.
      - `$replaceToReq` - Whether to replace or append the request.
    - **Returns**: None

  - `getUrlEncoded($input, $toReq = null, $replaceToReq = false)`
    - **Purpose**: Encodes a generated URL.
    - **Parameters**: 
      - `$input` - The URL part to encode.
      - `$toReq` - Optional request to replace or append to.
      - `$replaceToReq` - Whether to replace or append the request.
    - **Returns**: String - The encoded URL.

  - `setEcho($value)`
    - **Purpose**: Sets whether the framework should echo output.
    - **Parameters**: `$value` - Boolean to set echo state.
    - **Returns**: None

  - `process()`
    - **Purpose**: Processes view responses.
    - **Parameters**: None
    - **Returns**: None

  - `wrapup()`
    - **Purpose**: Performs wrap-up operations for the framework, triggering events at the end of the request cycle.
    - **Parameters**: None
    - **Returns**: None

  - `form($fields, $options, &$data = null, &$aData = null)`
    - **Purpose**: Creates a form view object.
    - **Parameters**: 
      - `$fields` - Array of form fields.
      - `$options` - Form options.
      - `&$data` - Reference to data for the form.
      - `&$aData` - Reference to additional data.
    - **Returns**: Object - A form view object.

  - `debug($input = null, $email = false, $subject = false)`
    - **Purpose**: Outputs debug information, optionally via email.
    - **Parameters**: 
      - `$input` - Data to debug.
      - `$email` - Email address to send debug info to or boolean to toggle.
      - `$subject` - Email subject if sending via email.
    - **Returns**: None

  - `jsonEncode($input, $options = [])`
    - **Purpose**: Encodes data to JSON format.
    - **Parameters**: 
      - `$input` - Data to encode.
      - `$options` - Encoding options.
    - **Returns**: String - JSON encoded string.

  - `jsonDecode($input, $options = [])`
    - **Purpose**: Decodes JSON data.
    - **Parameters**: 
      - `$input` - JSON string to decode.
      - `$options` - Decoding options.
    - **Returns**: Array - Decoded JSON data.

  - `empty($input)`
    - **Purpose**: Checks if the input is considered empty by the framework's standards.
    - **Parameters**: `$input` - Data to check.
    - **Returns**: Boolean - Whether the input is considered empty.

  - `hasFilter($filterName)`
    - **Purpose**: Checks if a filter exists.
    - **Parameters**: `$filterName` - Name of the filter to check.
    - **Returns**: Boolean - True if the filter exists, false otherwise.

  - `hasEvent($eventName)`
    - **Purpose**: Checks if an event exists.
    - **Parameters**: `$eventName` - Name of the event to check.
    - **Returns**: Boolean - True if the event exists, false otherwise.

  - `regFilter($filterName, $func, $options = [])`
    - **Purpose**: Registers a new filter.
    - **Parameters**: 
      - `$filterName` - Name of the filter.
      - `$func` - Function to be called by the filter.
      - `$options` - Options for the filter registration.
    - **Returns**: None

  - `applyFilter($filterName, $value, $extra = null)`
    - **Purpose**: Applies a filter to a value.
    - **Parameters**: 
      - `$filterName` - Name of the filter to apply.
      - `$value` - Value to filter.
      - `$extra` - Additional data for the filter function.
    - **Returns**: Mixed - The filtered value.

  - `regEvent($eventName, $func, $options = [])`
    - **Purpose**: Registers a new event.
    - **Parameters**: 
      - `$eventName` - Name of the event.
      - `$func` - Function to be triggered by the event.
      - `$options` - Options for the event registration.
    - **Returns**: None

  - `triggerEvent($eventName, $extra = null, $options = [])`
    - **Purpose**: Triggers an event, calling all registered functions for that event.
    - **Parameters**: 
      - `$eventName` - Name of the event to trigger.
      - `$extra` - Additional data for the event functions.
      - `$options` - Options for how to handle the event's output.
    - **Returns**: Array - Output from event functions.

   - `appendResponseGroup($responseGroup, $outputs, $options = [])`
    - **Purpose**: Appends a single response group to outputs with type conversion options.
    - **Parameters**: 
      - `$responseGroup`: The response group to append.
      - `$outputs`: The outputs to which the response group will be appended.
      - `$options`: An array of options for how the response should be appended, like type conversion settings.
    - **Returns**: None
    - **Details**: This function processes each response within the provided `$responseGroup`, converting JavaScript or JSON-LD responses to HTML if specified in the `$options`. It then appends these responses to the corresponding type in `$outputs`, managing meta, HTML, and JavaScript content appropriately. If response options are provided, they are merged into the outputs.

  - `updateRequestFromResponseGroup(&$request, $responseGroup)`
    - **Purpose**: Updates a request based on responses within a response group.
    - **Parameters**: 
      - `&$request`: Reference to the request object that needs updating.
      - `$responseGroup`: The response group from which updates are sourced.
    - **Returns**: None
    - **Details**: Iterates through the `$responseGroup` to find a response of type 'request'. If found, it updates the `$request` reference with the content of that response. This can be used to dynamically alter the request based on previous response data.

  - `createResponseGroup(&$data)`
    - **Purpose**: Creates a response group from data, including various response types.
    - **Parameters**: 
      - `&$data`: Reference to an array containing structured data for building the response group.
    - **Returns**: Array, constructed response group
    - **Details**: This function constructs a response group by interpreting different keys in the `$data` array. It handles pre-JS, HTML, JS, meta data (including title, keywords, description, etc.), raw content, request updates, and error responses. Each type of response is encapsulated into a `jt_response` object and added to the response group array.

  - `get404ResponseGroup()`
    - **Purpose**: Retrieves the response group for a 404 error.
    - **Parameters**: None
    - **Returns**: Response group for 404
    - **Details**: This method calls the view controller to get the response group associated with a 404 error request, which would have been pre-registered in the request controller. It's used to handle 404 errors by providing a structured response group.

  - `setContentAlt($key, $content)`
    - **Purpose**: Sets alternative content in the database with a key.
    - **Parameters**: 
      - `$key`: The key under which the content will be stored.
      - `$content`: The content to store, which might be JSON encoded if it's not a string.
    - **Returns**: Result of database operation
    - **Details**: Uses the database controller to insert or update a row in the `jt_content_alt` table. If the content isn't a string, it's JSON encoded before storage. This function is useful for storing alternative versions or variations of content.

  - `getContentAlt($key, $force = false)`
    - **Purpose**: Retrieves alternative content from the database or cache.
    - **Parameters**: 
      - `$key`: The key used to retrieve the content.
      - `$force`: If true, forces a database query instead of using cached content.
    - **Returns**: Retrieved content or false
    - **Details**: Checks the cache first unless `$force` is true. If not in cache or forced, it queries the database. If the content is encrypted, it decrypts it before returning. The result is cached for future use.

  - `getContent($key, $force = false)`
    - **Purpose**: Retrieves content from the database or cache.
    - **Parameters**: Same as `getContentAlt`
    - **Returns**: Retrieved content or false
    - **Details**: Similar to `getContentAlt`, but retrieves content from the `jt_content` table. It uses caching to improve performance unless `$
   
  **Fields**

- `public static $util`
  - **Purpose**: Instance of `jt_util_controller`, provides utility functions across the framework.
  - **Details**: This field holds an instance of the utility controller, which likely contains various helper methods used throughout the framework for miscellaneous operations.

- `public static $db`
  - **Purpose**: Instance of `jt_db_controller`, manages database interactions.
  - **Details**: This field is initialized with the database controller, which is responsible for handling all database operations, including CRUD actions, based on the framework's configuration.

- `public static $data`
  - **Purpose**: Instance of `jt_data_controller`, handles data operations.
  - **Details**: Manages data manipulation, storage, and retrieval within the framework, possibly serving as an abstraction layer over direct database interactions.

- `public static $error`
  - **Purpose**: Instance of `jt_error_controller`, manages error handling and logging.
  - **Details**: This controller deals with error reporting, logging, and possibly the display of errors, ensuring consistent error management across the application.

- `public static $email`
  - **Purpose**: Instance of `jt_email_controller`, manages email functionalities.
  - **Details**: Responsible for sending emails, likely including functionalities for constructing, sending, and possibly managing email queues or templates.

- `public static $validate`
  - **Purpose**: Instance of `jt_validate_controller`, validates data against rules or schemas.
  - **Details**: This controller is used for validating user input or other data against predefined rules, ensuring data integrity before processing.

- `public static $scrub`
  - **Purpose**: Instance of `jt_scrub_controller`, cleans and sanitizes input data.
  - **Details**: Provides methods to scrub or sanitize data, preventing security vulnerabilities like XSS or SQL injection by cleaning input before it's used or stored.

- `public static $request`
  - **Purpose**: Instance of `jt_request_controller`, manages HTTP and CLI requests.
  - **Details**: Central to routing and handling the lifecycle of requests, this controller processes incoming requests, whether from web or command line interfaces.

- `public static $session`
  - **Purpose**: Instance of `jt_session_controller`, handles session management.
  - **Details**: Manages session creation, reading, writing, and destruction, crucial for maintaining user state across requests.

- `public static $security`
  - **Purpose**: Instance of `jt_security_controller`, oversees security-related operations.
  - **Details**: Deals with authentication, authorization, encryption, and other security measures to protect the application and its users.

- `public static $image`
  - **Purpose**: Instance of `jt_image_controller`, manages image operations.
  - **Details**: Handles image processing tasks like uploading, resizing, or manipulating images within the framework.

- `public static $agent`
  - **Purpose**: Instance of `jt_agent_controller`, manages user agent information.
  - **Details**: Likely used to gather and process information about the user's browser or device, aiding in responsive design or user-specific functionality.

- `public static $config`
  - **Purpose**: Stores framework configuration settings.
  - **Details**: This field holds configuration data specific to the current environment, allowing dynamic configuration based on where the application is running.

- `public static $server`
  - **Purpose**: Instance of `jt_server_controller`, manages server-specific operations.
  - **Details**: Handles server-related tasks, possibly including server environment setup, server variable management, or server-side logic.

- `public static $text`
  - **Purpose**: Instance of `jt_text_controller`, manages text processing.
  - **Details**: Provides methods for text manipulation, encoding, decoding, or sanitization, useful for content management or user input processing.

- `public static $date`
  - **Purpose**: Instance of `jt_date_controller`, manages date and time functionalities.
  - **Details**: Deals with date formatting, calculations, and possibly time zone management, ensuring consistent handling of temporal data.

- `public static $view`
  - **Purpose**: Instance of `jt_view_controller`, manages view rendering.
  - **Details**: Responsible for rendering views, possibly including templating engine integration, to display data to the user.

- `public static $node`
  - **Purpose**: Instance of `jt_node_controller`, likely for Node.js integration.
  - **Details**: This might handle integration or interaction with Node.js scripts or services, providing a bridge between PHP and Node.js environments.

- `public static $flags`
  - **Purpose**: Stores framework-specific flags or settings.
  - **Details**: Used to hold various flags or settings that might affect the behavior of the framework, potentially set via CLI or environment variables.

- `public static $_echo = true`
  - **Purpose**: Controls whether the framework should output content.
  - **Details**: A boolean flag that determines if the framework should echo output directly. Useful for controlling output in different contexts or testing scenarios.

- `public static $_version = 3.1`
  - **Purpose**: Stores the current version of the framework.
  - **Details**: This field keeps track of the framework's version, which can be useful for logging, compatibility checks, or displaying to users.

- `public static $_env`
  - **Purpose**: Stores the current environment setting.
  - **Details**: Holds the environment in which the framework is running (like 'dev', 'staging', 'live'), affecting configuration and behavior.

- `public static $_cliParams = []`
  - **Purpose**: Array to store CLI command-line parameters.
  - **Details**: Contains parameters passed via the command line when running in CLI mode, used for customizing script behavior or passing data into the framework. This array is populated by parsing CLI arguments during initialization.

- `public static $_cliOptions = []`
  - **Purpose**: Array to store CLI command-line options.
  - **Details**: Stores options passed via the command line in CLI mode, which can affect the framework's operation or configuration. Options are typically key-value pairs or flags, set during the CLI parsing process.

- `public static $_date`
  - **Purpose**: Stores the current date.
  - **Details**: This field holds the date in 'Y-m-d' format, derived from the current timestamp during initialization. It's used for date-specific operations or logging within the framework.

- `public static $_datetime`
  - **Purpose**: Stores the current date and time.
  - **Details**: Contains the current date and time in 'Y-m-d H:i:s' format, set at the start of the framework's execution. Useful for timestamping actions, logging, or any time-sensitive operations.

- `public static $_timestamp`
  - **Purpose**: Stores the current Unix timestamp.
  - **Details**: This field is set to the current Unix timestamp (`time()`) during initialization. It serves as a reference for all time-based operations within the framework, allowing for precise timing and logging.

- `private static $_config = []`
  - **Purpose**: Private array to store configuration settings.
  - **Details**: Contains all configuration settings for the framework, organized by environment. This private field ensures that configuration data is not directly accessible outside the class, maintaining encapsulation.

- `private static $_events = []`
  - **Purpose**: Private array to store event handlers.
  - **Details**: Holds all registered event handlers, organized by event name and priority. This allows the framework to trigger events at various points, facilitating modular and extensible code architecture.

- `private static $_filters = []`
  - **Purpose**: Private array to store filter functions.
  - **Details**: Stores filter functions registered within the framework, used to modify or process data at runtime. Filters are organized by filter name and priority, enabling dynamic data manipulation.

- `private static $_content = []`
  - **Purpose**: Private array to cache content.
  - **Details**: Used to cache content retrieved from the database to avoid repeated queries. This improves performance by storing frequently accessed content in memory.

- `private static $_contentAlt = []`
  - **Purpose**: Private array to cache alternative content.
  - **Details**: Similar to `$_content`, this field caches alternative content, which might be used for different versions or variations of content, enhancing performance by reducing database hits.

- `private static $_init = false`
  - **Purpose**: Boolean to track if initialization has occurred.
  - **Details**: A flag that indicates whether the framework has been initialized. Set to `true` after the `init()` method completes, ensuring that initialization processes are not repeated unnecessarily.
