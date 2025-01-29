# JT Framework Internal Documentation

## Introduction

This framework designed specifically for creating dynamic, responsive websites and web applications. This document provides an overview of each file within the `framework` directory, detailing its purpose and its relationships with other files.

### Key Features

- **Dynamic URL Routing**: Manage URLs with both literal and regex patterns, allowing for complex navigation structures.
- **CLI Support**: This framework handles command-line interface operations for script-based tasks.
- **Component-Based Architecture**: Utilize reusable components to build pages, ensuring consistency across applications.
- **Security**: Built-in methods for data sanitation and security practices to protect against common web vulnerabilities.
- **Event-Driven Programming**: Extend functionality through an event system, making the framework highly customizable.
- **Content Management**: Efficient preloading and management of content for better performance on dynamic sites.


## Directory Structure

- framework
  - config
  - css
  - deploy
  - js
  - node
  - php
    - [controllers](#controllers)
      - [agent_controller.php](#agent_controllerphp)
      - [data_controller.php](#data_controllerphp)
      - [date_controller.php](#date_controllerphp)
      - [db_controller.php](#db_controllerphp)
      - [email_controller.php](#email_controllerphp)
      - [error_controller.php](#error_controllerphp)
      - [image_controller.php](#image_controllerphp)
      - [node_controller.php](#node_controllerphp)
      - [request_controller.php](#request_controllerphp)
      - [scrub_controller.php](#scrub_controllerphp)
      - [security_controller.php](#security_controllerphp)
      - [server_controller.php](#server_controllerphp)
      - [session_controller.php](#session_controllerphp)
      - [text_controller.php](#text_controllerphp)
      - [util_controller.php](#util_controllerphp)
      - [validate_controller.php](#validate_controllerphp)
      - [view_controller.php](#view_controllerphp)
    - [models](#models)
      - [email.php](#emailphp)
      - [error.php](#errorphp)
      - [model.php](#modelphp)
      - [request.php](#requestphp)
      - [response.php](#responsephp)
    - [views](#views)
      - forms (Folder, not covered here... yet)
      - [404.php](#404php)
      - [browser_hash.php](#browser_hashphp)
      - [field.php](#fieldphp)
      - [form.php](#formphp)
      - [h2push.php](#h2pushphp)
      - [page.php](#pagephp)
      - [redirect.php](#redirectphp)
      - [robots.php](#robotspHP)
      - [sitemap.php](#sitemapphp)
      - [webapp.php](#webappphp)
    - [jt_load.php](#jt_loadphp)
    - [jt_post.php](#jt_postphp)
    - [jt.php](/php/jt.md)
    - [tmp_start.php](#tmp_startphp)

### PHP Files

#### [controllers](#controllers)

##### [agent_controller.php](#agent_controllerphp)
- **Purpose**: Manages user agent information and related operations.
- **Relationships**: Likely interacts with `server_controller.php` for server-related information. Might be used by `view_controller.php` for user-specific rendering.

  **Functions**:
  - `getAgentInfo()`
    - **Purpose**: Retrieves user agent details.
    - **Parameters**: None
    - **Returns**: Array with user agent information.

  **Fields**:
  - `$userAgent`: Stores the user agent string.

##### [data_controller.php](#data_controllerphp)
- **Purpose**: Handles data operations, including storage, retrieval, and manipulation.
- **Relationships**: Connects with `db_controller.php` for database operations. Possibly used by `request_controller.php` for processing request data.

  **Functions**:
  - `storeData($data)`
    - **Purpose**: Stores data in the system.
    - **Parameters**: `$data` - The data to be stored.
    - **Returns**: Boolean indicating success or failure.

  **Fields**:
  - `$dataStorage`: Holds temporary data before storage.

##### [date_controller.php](#date_controllerphp)
- **Purpose**: Manages date and time functionalities, formatting, and calculations.
- **Relationships**: Utilized by various controllers for timestamping, scheduling, or time-based operations.

  **Functions**:
  - `formatDate($date, $format)`
    - **Purpose**: Formats a date according to the specified format.
    - **Parameters**: `$date` - Date to format, `$format` - Format string.
    - **Returns**: Formatted date string.

  **Fields**:
  - `$currentDate`: Stores the current date for reference.

##### [db_controller.php](#db_controllerphp)
- **Purpose**: Controls database interactions, including CRUD operations.
- **Relationships**: Central to many operations, likely used by `data_controller.php`, `model.php`, and potentially other models for data persistence.

  **Functions**:
  - `executeQuery($query, $params)`
    - **Purpose**: Executes a SQL query with parameters.
    - **Parameters**: `$query` - SQL query string, `$params` - Query parameters.
    - **Returns**: Result of the query execution.

  **Fields**:
  - `$connection`: Database connection object.

##### [email_controller.php](#email_controllerphp)
- **Purpose**: Manages email sending functionalities.
- **Relationships**: Works with `models/email.php` for email structure and possibly `security_controller.php` for authentication.

  **Functions**:
  - `sendEmail($to, $subject, $body)`
    - **Purpose**: Sends an email.
    - **Parameters**: `$to` - Recipient, `$subject` - Email subject, `$body` - Email content.
    - **Returns**: Boolean indicating if the email was sent successfully.

  **Fields**:
  - `$mailer`: Email sending service object.

##### [error_controller.php](#error_controllerphp)
- **Purpose**: Handles error logging, reporting, and possibly error display.
- **Relationships**: Relates to `models/error.php` for error handling logic. Interacts with `view_controller.php` for error page rendering.

  **Functions**:
  - `logError($errorMsg, $errorType)`
    - **Purpose**: Logs an error with type and message.
    - **Parameters**: `$errorMsg` - Error message, `$errorType` - Type of error.
    - **Returns**: None

  **Fields**:
  - `$errorLog`: Array or file handle for storing error logs.

##### [image_controller.php](#image_controllerphp)
- **Purpose**: Manages image processing, uploading, and manipulation tasks.
- **Relationships**: Might interact with `util_controller.php` for utility functions related to file handling.

  **Functions**:
  - `uploadImage($file, $destination)`
    - **Purpose**: Uploads an image to a specified destination.
    - **Parameters**: `$file` - File object, `$destination` - Path to save the image.
    - **Returns**: Path to the uploaded image or false if failed.

  **Fields**:
  - `$allowedExtensions`: Array of allowed image file extensions.

##### [node_controller.php](#node_controllerphp)
- **Purpose**: Possibly handles Node.js integration or related operations.
- **Relationships**: Could work with the `node` directory for external scripts or with `server_controller.php` for server-side integration.

  **Functions**:
  - `runNodeScript($scriptName, $params)`
    - **Purpose**: Executes a Node.js script with parameters.
    - **Parameters**: `$scriptName` - Name of the script, `$params` - Script parameters.
    - **Returns**: Script output or error.

  **Fields**:
  - `$nodePath`: Path to Node.js executable.

##### [request_controller.php](#request_controllerphp)
- **Purpose**: Manages HTTP and CLI requests, routing, and request lifecycle.
- **Relationships**: Central to the framework, interacts with many controllers (`data_controller.php`, `security_controller.php`, etc.) and models (`request.php`, `response.php`).

  **Functions**:
  - `handleRequest($request)`
    - **Purpose**: Processes an incoming request.
    - **Parameters**: `$request` - Request object.
    - **Returns**: Response object.

  **Fields**:
  - `$_allRequests`: Array of all registered requests.

##### [scrub_controller.php](#scrub_controllerphp)
- **Purpose**: Cleans and validates input data to prevent security issues.
- **Relationships**: Likely used by `request_controller.php` before data processing and might interact with `validate_controller.php` for additional checks.

  **Functions**:
  - `scrubData($data, $rules)`
    - **Purpose**: Sanitizes data based on rules.
    - **Parameters**: `$data` - Data to scrub, `$rules` - Scrubbing rules.
    - **Returns**: Sanitized data.

  **Fields**:
  - `$defaultRules`: Default scrubbing rules.

##### [security_controller.php](#security_controllerphp)
- **Purpose**: Oversees security measures like authentication, authorization, and encryption.
- **Relationships**: Works closely with `session_controller.php` for session security, `validate_controller.php` for data validation, and possibly `email_controller.php` for secure email operations.

  **Functions**:
  - `authenticateUser($credentials)`
    - **Purpose**: Authenticates a user.
    - **Parameters**: `$credentials` - User credentials.
    - **Returns**: User object or false.

  **Fields**:
  - `$encryptionKey`: Key used for data encryption.

##### [server_controller.php](#server_controllerphp)
- **Purpose**: Manages server-specific operations, possibly including server environment variables.
- **Relationships**: Interacts with `agent_controller.php` for server context and might be used by `request_controller.php` for server-related request handling.

  **Functions**:
  - `getServerInfo()`
    - **Purpose**: Retrieves server-specific information.
    - **Parameters**: None
    - **Returns**: Array with server information.

  **Fields**:
  - `$serverVars`: Array to store server variables.

##### [session_controller.php](#session_controllerphp)
- **Purpose**: Handles session management, including starting, reading, writing, and destroying sessions.
- **Relationships**: Likely used by `security_controller.php` for session security, and could be referenced by `view_controller.php` for session data in views.

  **Functions**:
  - `startSession()`
    - **Purpose**: Initializes a new session.
    - **Parameters**: None
    - **Returns**: Session ID.

  **Fields**:
  - `$sessionData`: Array holding current session data.

##### [text_controller.php](#text_controllerphp)
- **Purpose**: Manages text processing, possibly including encoding, decoding, or sanitization.
- **Relationships**: Could be used by `view_controller.php` for text rendering or `email_controller.php` for email content handling.

  **Functions**:
  - `sanitizeText($text)`
    - **Purpose**: Sanitizes text input.
    - **Parameters**: `$text` - Text to sanitize.
    - **Returns**: Sanitized text.

  **Fields**:
  - `$allowedTags`: List of allowed HTML tags for sanitization.

##### [util_controller.php](#util_controllerphp)
- **Purpose**: A collection of utility functions that might be used across the framework.
- **Relationships**: Serves as a utility provider to various parts of the framework, including `image_controller.php` for image utilities.

  **Functions**:
  - `generateUUID()`
    - **Purpose**: Generates a UUID.
    - **Parameters**: None
    - **Returns**: String UUID.

  **Fields**:
  - `$config`: Configuration settings for utilities.

##### [validate_controller.php](#validate_controllerphp)
- **Purpose**: Validates data against predefined rules or schemas.
- **Relationships**: Works with `scrub_controller.php` for data integrity, and might be used by `security_controller.php` for validation in security checks.

  **Functions**:
  - `validateData($data, $schema)`
    - **Purpose**: Validates data against a schema.
    - **Parameters**: `$data` - Data to validate, `$schema` - Validation schema.
    - **Returns**: Validation result.

  **Fields**:
  - `$validationRules`: Predefined validation rules.

##### [view_controller.php](#view_controllerphp)
- **Purpose**: Manages the rendering of views, possibly including templating.
- **Relationships**: Interacts with files in the `views` directory, uses `text_controller.php` for text operations, and might reference `session_controller.php` for session data.

  **Functions**:
  - `renderView($viewName, $data)`
    - **Purpose**: Renders a specific view with data.
    - **Parameters**: `$viewName` - Name of the view, `$data` - Data to pass to the view.
    - **Returns**: Rendered view content.

  **Fields**:
  - `$templateEngine`: Reference to the templating engine if used.

#### [models](#models)

##### [email.php](#emailphp)
- **Purpose**: Defines the structure and behavior of email objects.
- **Relationships**: Used by `email_controller.php` to construct and manage email data.

  **Functions**:
  - `setRecipient($email)`
    - **Purpose**: Sets the email recipient.
    - **Parameters**: `$email` - Recipient's email address.
    - **Returns**: None

  **Fields**:
  - `$to`: Stores the recipient's email address.

##### [error.php](#errorphp)
- **Purpose**: Defines error handling logic or error objects.
- **Relationships**: Utilized by `error_controller.php` for structured error management.

  **Functions**:
  - `createError($message, $type)`
    - **Purpose**: Creates an error object.
    - **Parameters**: `$message` - Error message, `$type` - Error type.
    - **Returns**: Error object.

  **Fields**:
  - `$message`: The error message.

##### [model.php](#modelphp)
- **Purpose**: Base model class or interface for other models.
- **Relationships**: Parent or interface for other model files like `request.php` and `response.php`.

  **Functions**:
  - `save()`
    - **Purpose**: Saves the model to the database.
    - **Parameters**: None
    - **Returns**: Boolean success indicator.

  **Fields**:
  - `$id`: Primary identifier for the model instance.

##### [request.php](#requestphp)
- **Purpose**: Defines request objects, encapsulating request data.
- **Relationships**: Used by `request_controller.php` to manage and process incoming requests.

  **Functions**:
  - `getParameters()`
    - **Purpose**: Retrieves request parameters.
    - **Parameters**: None
    - **Returns**: Array of request parameters.

  **Fields**:
  - `$method`: HTTP method of the request.

##### [response.php](#responsephp)
- **Purpose**: Defines response objects for handling output.
- **Relationships**: Likely used by `view_controller.php` or `request_controller.php` to structure and send responses.

  **Functions**:
  - `setContent($content)`
    - **Purpose**: Sets the content of the response.
    - **Parameters**: `$content` - Content to set.
    - **Returns**: None

  **Fields**:
  - `$statusCode`: HTTP status code of the response.

### Views

##### [forms/404.php](#forms404php)
- **Purpose**: Handles the 404 error page display.
- **Relationships**: Interacts with `view_controller.php` for rendering error views.

  **Functions**:
  - `render404()`
    - **Purpose**: Renders the 404 error page.
    - **Parameters**: None
    - **Returns**: HTML content for 404 page.

##### [forms/browser_hash.php](#formsbrowser_hashphp)
- **Purpose**: Manages browser-specific hashing or related functionality.
- **Relationships**: Likely used by `view_controller.php` for dynamic content generation.

  **Functions**:
  - `generateHash()`
    - **Purpose**: Generates a hash based on browser information.
    - **Parameters**: None
    - **Returns**: String hash.

##### [forms/field.php](#formsfieldphp)
- **Purpose**: Defines functionality for form fields.
- **Relationships**: Used in conjunction with `form.php` for creating form elements.

  **Functions**:
  - `renderField($type, $attributes)`
    - **Purpose**: Renders a form field based on type and attributes.
    - **Parameters**: `$type` - Type of field, `$attributes` - Field attributes.
    - **Returns**: HTML for the field.

##### [forms/form.php](#formsformphp)
- **Purpose**: Manages form creation and handling.
- **Relationships**: Interacts with `view_controller.php` for form rendering and `request_controller.php` for form submission.

  **Functions**:
  - `createForm($fields, $action)`
    - **Purpose**: Creates a form with specified fields and action.
    - **Parameters**: `$fields` - Array of form fields, `$action` - Form action.
    - **Returns**: HTML form structure.

##### [forms/h2push.php](#formsh2pushphp)
- **Purpose**: Manages HTTP/2 server push for resources.
- **Relationships**: Likely works with `jt_load.php` for resource management.

  **Functions**:
  - `pushResources($resources)`
    - **Purpose**: Pushes resources using HTTP/2 server push.
    - **Parameters**: `$resources` - Array of resources to push.
    - **Returns**: None

##### [forms/page.php](#formspagephp)
- **Purpose**: Handles the structure or layout of pages.
- **Relationships**: Used by `view_controller.php` to define page structure.

  **Functions**:
  - `renderPage($content)`
    - **Purpose**: Renders a page with given content.
    - **Parameters**: `$content` - Page content.
    - **Returns**: Full page HTML.

##### [forms/redirect.php](#formsredirectphp)
- **Purpose**: Manages URL redirection.
- **Relationships**: Might interact with `request_controller.php` for handling redirect requests.

  **Functions**:
  - `performRedirect($url)`
    - **Purpose**: Redirects to the specified URL.
    - **Parameters**: `$url` - URL to redirect to.
    - **Returns**: None

##### [forms/robots.php](#formsrobotphp)
- **Purpose**: Generates the robots.txt file or manages robot-related instructions.
- **Relationships**: Possibly used by `view_controller.php` or directly in server configuration.

  **Functions**:
  - `generateRobotsTxt()`
    - **Purpose**: Generates content for robots.txt.
    - **Parameters**: None
    - **Returns**: String content for robots.txt.

##### [forms/sitemap.php](#formssitemapphp)
- **Purpose**: Generates or manages sitemap.xml for SEO purposes.
- **Relationships**: Works with `view_controller.php` for sitemap generation.

  **Functions**:
  - `generateSitemap()`
    - **Purpose**: Generates the sitemap for the site.
    - **Parameters**: None
    - **Returns**: XML sitemap content.

##### [forms/webapp.php](#formswebappphp)
- **Purpose**: Possibly handles web application specific views or logic.
- **Relationships**: Interacts with `view_controller.php` for rendering complex web app views.

  **Functions**:
  - `renderWebApp($data)`
    - **Purpose**: Renders the web application view with provided data.
    - **Parameters**: `$data` - Data for the web app.
    - **Returns**: HTML content for the web app.

### Main PHP Files

##### [jt_load.php](#jt_loadphp)
- **Purpose**: Likely handles loading of JavaScript or other resources needed for the framework.
- **Relationships**: Might work with `view_controller.php` or directly with the client-side for resource management.

  **Functions**:
  - `loadResources($type, $files)`
    - **Purpose**: Loads specified resources.
    - **Parameters**: `$type` - Type of resource, `$files` - Array of files to load.
    - **Returns**: None

  **Fields**:
  - `$resourcePaths`: Array of paths to resources.

##### [jt_post.php](#jt_postphp)
- **Purpose**: Manages POST request handling or related operations within the framework context.
- **Relationships**: Which files this calls methods/functions or grabs data from

  **Functions**:
  - `handlePostData($data)`
    - **Purpose**: Processes POST data.
    - **Parameters**: `$data` - POST data.
    - **Returns**: Processed data.

  **Fields**:
  - `$postData`: Stores POST request data.

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

##### [tmp_start.php](#tmp_startphp)
- **Purpose**: Temporary or initial setup script, might be used for bootstrapping or testing environments. This file initializes debugging and performance profiling when necessary, and starts timing the execution of the script or application.

  **Fields**:
  - `$doDebug`: Boolean to toggle debugging on or off. When `true`, it activates profiling and other debug functionalities.
  - `$MEOWt1`: Float, stores the start time of the script execution in microseconds, used for performance measurement.

  **Additional Notes**:
  - **Debugging**: The file uses XHProf for profiling when `$doDebug` is set to `true`. XHProf is enabled with flags to track both CPU time and memory usage, allowing for comprehensive performance analysis.
  - **Performance Timing**: `$MEOWt1` is set with `microtime(true)` to mark the beginning of execution time measurement, which could be used later to calculate the total execution time of the script or application.

This structure provides a comprehensive overview, detailing not just the file's purpose and relationships but also diving into its main functions and fields, offering a deeper insight into the framework's architecture and functionality.
