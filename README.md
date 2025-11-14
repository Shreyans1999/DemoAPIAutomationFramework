# API Automation Framework

## 📋 Project Overview
This is a **Java-based REST API Automation Framework** built using **Maven**, **TestNG**, and **RestAssured**. The framework follows best practices with a modular architecture, implementing the **Page Object Model (POM)** design pattern for API testing, along with comprehensive logging and reporting capabilities.

## 🏗️ Framework Architecture

### Project Structure
```
DemoAPIAutomationFramework/
├── src/test/java/com/api/
│   ├── base/                          # Service layer (Base classes)
│   │   ├── BaseService.java           # RestAssured wrapper with common methods
│   │   ├── AuthService.java           # Authentication API endpoints
│   │   └── UserProfileManagementService.java  # User profile API endpoints
│   ├── models/
│   │   ├── request/                   # Request POJOs
│   │   │   ├── LoginRequest.java
│   │   │   ├── SignUpRequest.java
│   │   │   └── ProfileRequest.java
│   │   └── response/                  # Response POJOs
│   │       ├── LoginResponse.java
│   │       └── UserProfileResponse.java
│   ├── filters/                       # Custom filters
│   │   └── LoggingFilter.java         # Request/Response logging filter
│   ├── listeners/                     # TestNG listeners
│   │   └── TestListener.java          # Test execution listener
│   └── tests/                         # Test classes
│       ├── LoginAPITest3.java
│       ├── AccountCreationTest.java
│       ├── ForgotPasswordTest.java
│       ├── GetProfileRequestTest.java
│       └── UpdateProfileTest.java
├── src/test/resources/
│   └── log4j2.xml                     # Log4j2 configuration
├── logs/                              # Log files directory
│   └── test.log                       # Execution logs
├── test-output/                       # TestNG reports
│   ├── testng-results.xml
│   └── emailable-report.html
├── suite.xml                          # TestNG suite configuration
└── pom.xml                            # Maven dependencies
```

## 🛠️ Technologies & Tools

| Technology | Version | Purpose |
|-----------|---------|---------|
| **Java** | 11 | Programming Language |
| **Maven** | - | Build & Dependency Management |
| **TestNG** | 7.10.2 | Testing Framework |
| **RestAssured** | 5.3.0 | API Testing Library |
| **Jackson** | 2.18.2 | JSON Serialization/Deserialization |
| **Log4j2** | 2.20.0 | Logging Framework |

## 🎯 Key Features

### 1. **Modular Architecture**
- **Service Layer Pattern**: Separate service classes (`AuthService`, `UserProfileManagementService`) for different API modules
- **BaseService**: Common RestAssured wrapper providing reusable methods (`postRequest`, `getRequest`, `putRequest`)
- **Model Classes**: POJO classes for request/response with Builder pattern implementation

### 2. **Advanced Logging**
- **Custom LoggingFilter**: Automatically logs all API requests and responses
- **Log4j2 Integration**: Dual logging to console and file (`logs/test.log`)
- **TestListener**: Captures test execution events (start, success, failure, skip)

### 3. **Request/Response Handling**
- **Builder Pattern**: Implemented in `SignUpRequest` and `ProfileRequest` for flexible object creation
- **JSON Serialization**: Automatic conversion between Java objects and JSON using Jackson
- **Token Management**: Dynamic bearer token handling for authenticated requests

### 4. **Comprehensive Test Coverage**
- Authentication APIs (Login, Signup, Forgot Password)
- User Profile Management (Get Profile, Update Profile)
- Assertion validations using TestNG

## 🚀 Getting Started

### Prerequisites
- **Java JDK 11** or higher installed
- **Maven** installed and configured
- **Git Bash** or any terminal

### Installation
1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd DemoAPIAutomationFramework
   ```

2. **Install dependencies**
   ```bash
   mvn clean install
   ```

## ▶️ Execution

### Run Tests via Maven
```bash
mvn clean test -Dsuite=suite -Denv=qa
```

**Parameters:**
- `-Dsuite=suite` : Specifies the TestNG suite file name (suite.xml)
- `-Denv=qa` : Environment parameter (can be customized)

### Suite Configuration
The `suite.xml` file controls which test classes to execute:
```xml
<suite name="API Test Suite">
    <test thread-count="5" name="API Test">
        <classes>
            <class name="com.api.tests.LoginAPITest3"/>
        </classes>
    </test>
</suite>
```

To run different tests, modify the `<class>` entries in `suite.xml`.

## 📊 Logging & Reporting

### 1. **Logs**
All execution logs are stored in `logs/test.log` with the following information:
- Test suite start/completion
- Request details (URI, Headers, Body)
- Response details (Status Code, Headers, Body)
- Test results (Pass/Fail/Skip)

**Sample Log Output:**
```
08:37:48.533 [main] INFO  com.api.listeners.TestListener - Test Suite Started!!!
08:37:51.330 [main] INFO  com.api.filters.LoggingFilter - Base URI:http://64.227.160.186:8080
08:37:51.331 [main] INFO  com.api.filters.LoggingFilter - Request Header:Accept=*/* Content-Type=application/json
08:37:51.331 [main] INFO  com.api.filters.LoggingFilter - Request Body:{"username":"shreyans1999","password":"shreyans1999"}
08:37:52.532 [main] INFO  com.api.filters.LoggingFilter - Request Header:Vary=Origin...
08:37:52.631 [main] INFO  com.api.filters.LoggingFilter - Request Body:{"token": "eyJhbGci...","type": "Bearer"...}
08:37:52.943 [main] INFO  com.api.listeners.TestListener - Started!! loginTest
08:37:52.943 [main] INFO  com.api.listeners.TestListener - Description!! Verify if Login API is working...
08:37:52.993 [main] INFO  com.api.listeners.TestListener - Test Suite Completed!!!
```

### 2. **TestNG Reports**
Reports are generated in the `test-output/` directory:
- **testng-results.xml** : Detailed XML report
- **emailable-report.html** : HTML email-friendly report
- **index.html** : Comprehensive HTML report

## 🧪 Test Scenarios

### 1. **LoginAPITest3**
- **Purpose**: Validates user login functionality
- **Assertions**: 
  - Token is not null
  - Email verification
  - User ID verification

### 2. **AccountCreationTest**
- **Purpose**: Tests new user account creation (signup)
- **Builder Pattern**: Uses SignUpRequest.Builder for request creation

### 3. **ForgotPasswordTest**
- **Purpose**: Tests password recovery functionality
- **Input**: User email address

### 4. **GetProfileRequestTest**
- **Purpose**: Retrieves user profile information
- **Flow**: Login → Get Token → Fetch Profile

### 5. **UpdateProfileTest**
- **Purpose**: Updates user profile details
- **Flow**: Login → Get Profile → Update Profile
- **Builder Pattern**: Uses ProfileRequest.Builder

## 🔑 Key Implementation Highlights

### BaseService Class
```java
- RestAssured wrapper providing reusable HTTP methods
- Base URI configuration: http://64.227.160.186:8080
- Bearer token authentication support
- Global LoggingFilter integration
```

### LoggingFilter
```java
- Intercepts all API requests/responses
- Logs complete request details (URI, Headers, Body)
- Logs complete response details (Status, Headers, Body)
- Integrates with Log4j2 for file and console logging
```

### Builder Pattern Implementation
```java
- Flexible object creation for complex request payloads
- Used in SignUpRequest and ProfileRequest
- Improves code readability and maintainability
```

## 📌 Interview Talking Points

1. **Framework Design Pattern**: 
   - Implemented Service Layer Pattern separating test logic from API calls
   - Used Builder Pattern for complex request object creation
   - POJO models for request/response deserialization

2. **Reusability**: 
   - BaseService provides common HTTP methods used across all services
   - Centralized configuration and request specification

3. **Logging Strategy**: 
   - Custom RestAssured filter for automatic request/response logging
   - TestNG listener for test lifecycle event logging
   - Log4j2 dual appender (Console + File)

4. **Test Configuration**: 
   - Dynamic suite execution via Maven parameters
   - TestNG XML for flexible test selection
   - Parallel execution support (thread-count=5)

5. **Authentication Handling**: 
   - Dynamic bearer token extraction and management
   - Automatic token injection in authenticated requests

6. **Reporting**: 
   - TestNG native HTML reports
   - Detailed execution logs in logs/test.log
   - XML reports for CI/CD integration

## 🔧 Configuration Files

### pom.xml
- Maven Surefire Plugin: Executes TestNG suites with dynamic suite parameter
- All dependencies managed with specific versions

### log4j2.xml
- Pattern layout: `%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n`
- Console and File appenders
- Root logger level: INFO

### suite.xml
- Configurable test suite
- Supports parallel execution
- Easy test class inclusion/exclusion

## 📝 Best Practices Implemented

✅ Separation of concerns (Service, Model, Test layers)  
✅ POJO model classes for type-safe API interaction  
✅ Comprehensive logging at all levels  
✅ Builder pattern for complex object creation  
✅ TestNG listeners for enhanced reporting  
✅ RestAssured filters for cross-cutting concerns  
✅ Maven for dependency and build management  
✅ Parameterized suite execution  

## 🤝 Contributing
This framework can be extended with:
- Data-driven testing using TestNG DataProvider
- Integration with CI/CD pipelines (Jenkins, GitHub Actions)
- Extent Reports for advanced reporting
- API response schema validation
- Environment-specific configuration files

**Framework Version**: 0.0.1-SNAPSHOT  
**Last Updated**: November 2025

