# JT Framework Documentation

## 1. Getting Started
- Installation Guide
- Basic Configuration
- Directory Structure
- Quick Start Example

## 2. Core Concepts
### Request Handling
- Request Types
  - Literal Requests
  - Regex Requests
  - CLI Requests
- Request Flow
- URL Key System

### Controllers
- Base Controller
- Request Controller
- Specialized Controllers
  - Agent Controller
  - Data Controller
  - View Controller
  - Security Controller
  - etc.

### Models
- Model System Overview
- Available Models
  - Email Model
  - Error Model
  - Request Model
  - Response Model

### Views
- View System
- Forms Handling
- Page Rendering
- Available View Helpers

## 3. Advanced Topics
### Routing System
- URL Management
- Request Processing
- Custom Routes
- URL Keys and Handlers

### Security
- Input Scrubbing
- Request Validation
- Security Best Practices

### Ajax Handling
- Ajax Requests
- State Management
- Request Types
- Response Handling

## 4. API Reference
### Controllers
```php
// Example Controller Documentation
class jt_request_controller {
    /**
     * Registers literal URL requests
     * @param array $requests Array of request configurations
     */
    public static function registerLiteralRequests($requests)

    /**
     * Registers regex-based URL patterns
     * @param array $requests Array of regex patterns and handlers
     */
    public static function registerRegexRequests($requests)
    // ... other methods
}
```

## 5. Examples and Tutorials
### Basic Usage
```php
// Example: Setting up a basic page route
jt_request_controller::registerLiteralRequests([
    'home' => [
        'name' => 'home',
        'handler' => 'HomeController::index',
        'type' => 'page'
    ]
]);
```

### Advanced Usage
```php
// Example: Custom URL key handler
jt_request_controller::registerUrlKeyHandler('products', function($urlKeyData, $uriPart) {
    // Handler logic
});
```

## 6. Best Practices and Guidelines
- Code Organization
- Naming Conventions
- Error Handling
- Performance Optimization

## 7. Troubleshooting
- Common Issues
- Debug Tools
- Error Messages
- FAQs
