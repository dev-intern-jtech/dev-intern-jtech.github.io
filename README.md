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
  - [php](#PHP_FILES)
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
    - [jt.php](#jtphp)
    - [tmp_start.php](#tmp_startphp)

### [PHP Files](#PHP_Files)

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
- **Relationships**: Interacts with `request_controller.php` for processing POST data.

  **Functions**:
  - `handlePostData($data)`
    - **Purpose**: Processes POST data.
    - **Parameters**: `$data` - POST data.
    - **Returns**: Processed data.

  **Fields**:
  - `$postData`: Stores POST request data.

##### [jt.php](#jtphp)
- **Purpose**: Likely the main entry point for framework initialization or core operations, managing the overall flow.
- **Relationships**: Central file, connects to all other parts of the framework, especially `view_controller.php`.

  **Functions**:
  - `init()`
    - **Purpose**: Initializes the framework.
    - **Parameters**: None
    - **Returns**: None

  **Fields**:
  - `$_version`: Framework version.

##### [tmp_start.php](#tmp_startphp)
- **Purpose**: Temporary or initial setup script, might be used for bootstrapping or testing environments.
- **Relationships**: Could be an entry point or setup file for development or specific scenarios, might interact with various controllers or models during setup.

  **Functions**:
  - `setupEnvironment()`
    - **Purpose**: Sets up the environment for development or testing.
    - **Parameters**: None
    - **Returns**: None

  **Fields**:
  - `$testMode`: Boolean indicating if in test mode.

This structure provides a comprehensive overview, detailing not just the file's purpose and relationships but also diving into its main functions and fields, offering a deeper insight into the framework's architecture and functionality.
