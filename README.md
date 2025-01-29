# JT Framework Internal Documentation

## 1. Framework Overview
- Directory Structure
- Key Components
- Configuration Settings

## 2. Core Components

### Request System
- Understanding Request Types
  - Literal Requests (`registerLiteralRequests`)
  - Regex Requests (`registerRegexRequests`)
  - CLI Requests (`registerCLIRequests`)
- URL Key System
  - How URL Keys Work
  - Adding Custom URL Handlers
  - Database Integration

### Controllers
- Available Controllers Overview
  - Request Controller
  - Agent Controller
  - Data Controller
  - View Controller
  - Security Controller
  - etc.
- How to Create New Controllers
- Best Practices

### Models & Views
- Model System
- View System
- Forms Processing
- Page Rendering

## 3. Common Use Cases

### Basic Routing
```php
// Setting up a simple page route
jt_request_controller::registerLiteralRequests([
    'dashboard' => [
        'name' => 'dashboard',
        'handler' => 'DashboardController::index',
        'type' => 'page'
    ]
]);
```

### URL Key Handling
```php
// Custom URL handler for product pages
jt_request_controller::registerUrlKeyHandler('products', function($urlKeyData, $uriPart) {
    // Product page logic
    return new jt_request([
        'name' => 'product_page',
        'handler' => 'ProductController::show',
        'type' => 'page'
    ]);
});
```

### AJAX Request Handling
```php
// Example of handling AJAX requests
jt_request_controller::registerLiteralRequests([
    'api-endpoint' => [
        'name' => 'api_call',
        'handler' => 'ApiController::handle',
        'type' => 'raw'
    ]
]);
```

## 4. Database Integration
- URL Keys Table Structure
- Query Handling
- Best Practices for DB Operations

## 5. Security Features
- Input Scrubbing System
- Request Validation
- Security Best Practices

## 6. Troubleshooting Guide
- Common Issues
- Debug Techniques
- Error Messages
- Known Limitations

## 7. Code Examples Library
- Complete Working Examples
- Common Patterns
- Reusable Code Snippets

## 8. Internal API Reference
Detailed method documentation for each core class:

### jt_request_controller
```php
/**
 * Core request handling class
 */
class jt_request_controller {
    /**
     * Registers direct URL matches
     * @param array $requests Array of request configurations
     */
    public static function registerLiteralRequests($requests)

    /**
     * Registers pattern-based URL matches
     * @param array $requests Array of regex patterns and handlers
     */
    public static function registerRegexRequests($requests)
    
    // ... other methods
}
```
