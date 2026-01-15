# 🏦 Banking Application API Automation Framework

<div align="center">

![Java](https://img.shields.io/badge/Java-11-orange?style=for-the-badge&logo=openjdk&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)
![TestNG](https://img.shields.io/badge/TestNG-7.10.2-green?style=for-the-badge)
![RestAssured](https://img.shields.io/badge/RestAssured-5.3.0-blue?style=for-the-badge)
![CI/CD](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)

**A production-ready Banking Application API Automation Framework built with Java, TestNG, and RestAssured**

[Getting Started](#-getting-started) • [Features](#-key-features) • [Architecture](#%EF%B8%8F-framework-architecture) • [Documentation](#-demo-application-resources)

</div>

---

## 📋 Overview

This is a **modular Java-based REST API Automation Framework** designed to test banking application APIs. Built following industry best practices, it implements the **Service Layer Pattern** combined with comprehensive logging, reporting, and CI/CD integration.

### ✨ What Makes This Framework Special?

- 🏗️ **Clean Architecture** — Separation of concerns with Service, Model, and Test layers
- 🔄 **Reusable Components** — BaseService wrapper for all HTTP operations
- 📝 **Comprehensive Logging** — Custom filters for request/response logging
- 🤖 **CI/CD Ready** — Pre-configured GitHub Actions workflow with scheduled runs
- 🧪 **Flexible Testing** — TestNG with XML-based suite configuration

---

## 🌐 Demo Application Resources

| Resource | Description | Link |
|----------|-------------|------|
| 🏦 **Banking App** | Test Application UI | [swift.techwithjatin.com](https://swift.techwithjatin.com/) |
| 📘 **Swagger UI** | API Reference & Documentation | [Swagger Docs](http://64.227.160.186:8080/swagger-ui/index.html) |
| 📝 **Notion Docs** | E2E Framework Creation Guide | [Notion Page](https://tech-with-jatin.notion.site/E2E-Automation-Framework-Creation-1526d427c22780328b8fff211ee050b7?pvs=4) |

---

## 🏗️ Framework Architecture

```
BankingApplicationAPIAutomationFramework/
├── 📁 src/test/java/com/api/
│   │
│   ├── 📁 base/                              # 🔧 Service Layer
│   │   ├── BaseService.java                  # RestAssured wrapper with HTTP methods
│   │   ├── AuthService.java                  # Authentication endpoints (login, signup, forgot-password)
│   │   └── UserProfileManagementService.java # User profile endpoints (get, update)
│   │
│   ├── 📁 models/
│   │   ├── 📁 request/                       # 📤 Request POJOs
│   │   │   ├── LoginRequest.java             # Login payload
│   │   │   ├── SignUpRequest.java            # Signup payload with Builder pattern
│   │   │   └── ProfileRequest.java           # Profile update payload
│   │   └── 📁 response/                      # 📥 Response POJOs
│   │       ├── LoginResponse.java            # Login response mapping
│   │       └── UserProfileResponse.java      # Profile response mapping
│   │
│   ├── 📁 filters/                           # 🔍 Custom Filters
│   │   └── LoggingFilter.java                # Request/Response logging filter
│   │
│   ├── 📁 listeners/                         # 👂 TestNG Listeners
│   │   └── TestListener.java                 # Test lifecycle event handler
│   │
│   └── 📁 tests/                             # 🧪 Test Classes
│       ├── LoginAPITest3.java                # Login API validation
│       ├── AccountCreationTest.java          # User signup testing
│       ├── ForgotPasswordTest.java           # Password recovery testing
│       ├── GetProfileRequestTest.java        # Get profile testing
│       └── UpdateProfileTest.java            # Profile update testing
│
├── 📁 src/test/resources/
│   └── log4j2.xml                            # Log4j2 configuration
│
├── 📁 .github/workflows/
│   └── maven.yml                             # GitHub Actions CI/CD pipeline
│
├── 📁 logs/                                  # 📋 Execution logs
├── 📁 test-output/                           # 📊 TestNG reports
├── suite.xml                                 # TestNG suite configuration
└── pom.xml                                   # Maven dependencies & build config
```

---

## 🛠️ Technology Stack

| Technology | Version | Purpose |
|:-----------|:-------:|:--------|
| **Java** | 11 | Core Programming Language |
| **Maven** | 3.x | Build & Dependency Management |
| **TestNG** | 7.10.2 | Test Framework with Annotations & Assertions |
| **RestAssured** | 5.3.0 | Fluent API for HTTP Testing |
| **Jackson** | 2.18.2 | JSON Serialization/Deserialization |
| **Log4j2** | 2.20.0 | Structured Logging Framework |
| **GitHub Actions** | - | CI/CD Pipeline & Scheduled Execution |

---

## 🎯 Key Features

### 1️⃣ Service Layer Pattern
```java
// BaseService provides reusable HTTP methods
public class AuthService extends BaseService {
    public Response login(LoginRequest payload) {
        return postRequest(payload, "/api/auth/login");
    }
}
```
- **BaseService**: Centralized RestAssured configuration with `postRequest()`, `getRequest()`, `putRequest()` methods
- **AuthService**: Authentication operations (login, signup, forgot-password)
- **UserProfileManagementService**: Profile operations (get profile, update profile)

### 2️⃣ Builder Pattern for Request Objects
```java
SignUpRequest request = new SignUpRequest.Builder()
    .username("john_doe")
    .password("secure123")
    .email("john@example.com")
    .firstName("John")
    .lastName("Doe")
    .mobileNumber("1234567890")
    .build();
```

### 3️⃣ Custom Logging Filter
All API requests and responses are automatically logged:
```
08:37:51.330 [main] INFO  LoggingFilter - Base URI:http://64.227.160.186:8080
08:37:51.331 [main] INFO  LoggingFilter - Request Header:Accept=*/* Content-Type=application/json
08:37:51.331 [main] INFO  LoggingFilter - Request Body:{"username":"user","password":"pass"}
08:37:52.532 [main] INFO  LoggingFilter - Response Status: 200
08:37:52.631 [main] INFO  LoggingFilter - Response Body:{"token": "eyJhbGci..."}
```

### 4️⃣ TestNG Listeners
Test lifecycle events are captured for enhanced reporting:
```
Test Suite Started!!!
Started!! loginTest
Description!! Verify if Login API is working...
Test Suite Completed!!!
```

### 5️⃣ CI/CD Integration
The framework includes a pre-configured GitHub Actions workflow:
- ✅ Triggered on push/PR to `master` branch
- ✅ Scheduled runs at **6:00 PM** and **3:00 AM** UTC daily
- ✅ Automatic artifact upload (logs)
- ✅ Test report publishing

---

## 🚀 Getting Started

### Prerequisites

| Requirement | Version | Check Command |
|-------------|---------|---------------|
| Java JDK | 11+ | `java -version` |
| Maven | 3.x | `mvn -version` |
| Git | Latest | `git --version` |

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/DemoAPIAutomationFramework.git

# Navigate to project directory
cd DemoAPIAutomationFramework

# Install dependencies
mvn clean install -DskipTests
```

---

## ▶️ Running Tests

### Execute All Tests
```bash
mvn clean test -Dsuite=suite
```

### Execute with Environment Parameter
```bash
mvn clean test -Dsuite=suite -Denv=qa
```

### Run in Verbose Mode
```bash
mvn clean test -Dsuite=suite -X
```

### Parameters Explained

| Parameter | Description | Example |
|-----------|-------------|---------|
| `-Dsuite` | TestNG suite file name (without .xml) | `-Dsuite=suite` |
| `-Denv` | Environment configuration | `-Denv=qa` |
| `-X` | Enable debug/verbose output | `-X` |

---

## 🧪 Test Scenarios

| Test Class | API Endpoint | Description |
|------------|--------------|-------------|
| `LoginAPITest3` | `POST /api/auth/login` | Validates login with token, email, and ID assertions |
| `AccountCreationTest` | `POST /api/auth/signup` | Tests new user registration flow |
| `ForgotPasswordTest` | `POST /api/auth/forgot-password` | Tests password recovery via email |
| `GetProfileRequestTest` | `GET /api/users/profile` | Retrieves authenticated user profile |
| `UpdateProfileTest` | `PUT /api/users/profile` | Updates user profile information |

### Sample Test Implementation
```java
@Listeners(TestListener.class)
public class LoginAPITest3 {

    @Test(description = "Verify if Login API is working...")
    public void loginTest() {
        LoginRequest loginRequest = new LoginRequest("username", "password");
        AuthService authService = new AuthService();
        
        Response response = authService.login(loginRequest);
        LoginResponse loginResponse = response.as(LoginResponse.class);
        
        Assert.assertNotNull(loginResponse.getToken());
        Assert.assertEquals(loginResponse.getEmail(), "expected@email.com");
    }
}
```

---

## 📊 Logging & Reporting

### 📁 Log Files
Execution logs are stored in `logs/test.log`:
```
08:37:48.533 [main] INFO  TestListener - Test Suite Started!!!
08:37:51.330 [main] INFO  LoggingFilter - Base URI:http://64.227.160.186:8080
08:37:52.943 [main] INFO  TestListener - Started!! loginTest
08:37:52.993 [main] INFO  TestListener - Test Suite Completed!!!
```

### 📊 TestNG Reports
Generated in `test-output/` directory:
- `index.html` — Comprehensive HTML report
- `emailable-report.html` — Email-friendly summary
- `testng-results.xml` — Detailed XML for CI/CD integration

---

## 🔄 CI/CD Pipeline

The framework includes GitHub Actions integration (`.github/workflows/maven.yml`):

```yaml
name: API Test Framework

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]
  schedule:
    - cron: "00 18 * * *"  # 6:00 PM UTC
    - cron: "00 3 * * *"   # 3:00 AM UTC
```

### Pipeline Features
- 🔹 Runs on Ubuntu with JDK 11
- 🔹 Maven dependency caching
- 🔹 Test execution with logs
- 🔹 Artifact upload (logs directory)
- 🔹 JUnit-style test report publishing

---

## 🔧 Configuration Files

### `suite.xml` — TestNG Suite
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="API Test Suite">
    <test thread-count="5" name="API Test">
        <classes>
            <class name="com.api.tests.LoginAPITest3"/>
            <!-- Add more test classes as needed -->
        </classes>
    </test>
</suite>
```

### `log4j2.xml` — Logging Configuration
- **Console Appender**: Real-time console output
- **File Appender**: Persistent log file (`logs/test.log`)
- **Pattern**: `%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n`

---

## 📌 Design Patterns & Best Practices

| Pattern/Practice | Implementation |
|-----------------|----------------|
| ✅ **Service Layer Pattern** | Separate service classes for each API module |
| ✅ **Builder Pattern** | `SignUpRequest.Builder` for flexible object creation |
| ✅ **POJO Models** | Type-safe request/response serialization |
| ✅ **Custom Filters** | `LoggingFilter` for cross-cutting logging |
| ✅ **TestNG Listeners** | `TestListener` for lifecycle event handling |
| ✅ **Separation of Concerns** | Tests, Services, Models in dedicated packages |
| ✅ **Centralized Configuration** | Base URL and settings in `BaseService` |
| ✅ **Token Management** | Dynamic bearer token injection for authenticated requests |

---

## 🔮 Future Enhancements

- [ ] **Data-Driven Testing** — TestNG DataProvider integration
- [ ] **Extent Reports** — Advanced HTML reporting with screenshots
- [ ] **Schema Validation** — JSON schema assertions for responses
- [ ] **Environment Configs** — Property files for multiple environments
- [ ] **Parallel Execution** — Enhanced parallel test configuration
- [ ] **API Contract Testing** — Pact/OpenAPI integration

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is for educational and demonstration purposes.

---

<div align="center">

**Framework Version**: `0.0.1-SNAPSHOT`

**Last Updated**: January 2026

Made with ❤️ for API Testing

</div>
