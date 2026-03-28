# Realtime Currency Converter

A full-stack web application for converting currencies, cryptocurrency values, and units in real-time. Built with Spring Boot and Thymeleaf, featuring user authentication and caching for optimal performance.

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Database](#database)
- [Caching](#caching)
- [Security](#security)
- [Building & Deployment](#building--deployment)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

- **Real-time Currency Conversion** - Convert between multiple currencies with live exchange rates
- **Cryptocurrency Tracking** - Get real-time crypto prices from Binance
- **Unit Converter** - Convert between different units (length, weight, temperature, etc.)
- **User Authentication** - Secure login and registration system
- **Responsive Dashboard** - User-friendly web interface with responsive design
- **Performance Caching** - 6-hour cache for exchange rates to reduce API calls
- **In-Memory Database** - H2 database for quick prototyping and testing

## 🛠 Tech Stack

### Backend
- **Core Framework**: Spring Boot 4.0.5
- **Java Version**: Java 22
- **Server**: Spring Boot Embedded Server
- **ORM**: Spring Data JPA with Hibernate
- **Database**: H2 Database (In-Memory)

### Frontend
- **Template Engine**: Thymeleaf
- **Markup**: HTML5
- **Styling**: CSS3

### Security
- **Framework**: Spring Security 6
- **Authentication**: Form-based login with Thymeleaf integration

### Caching
- **Cache Provider**: Caffeine
- **Cache Strategy**: Expiry after 6 hours

### APIs & External Services
- **Exchange Rates**: ExchangeRate-API v6
- **Cryptocurrency**: Binance API

### Build & Development
- **Build Tool**: Maven
- **Testing**: JUnit 5 with Spring Boot Test
- **Additional Libraries**: Lombok (for reducing boilerplate code)

## 📦 Prerequisites

- **Java 22** or higher
- **Maven 3.6+**
- **Git**
- Internet connection for API calls

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Muskan-zehra12/Realtime-_Converter.git
   cd realtime_currency_converter
   ```

2. **Navigate to project directory**
   ```bash
   cd realtime_currency_converter
   ```

3. **Build the project**
   ```bash
   mvn clean install
   ```

## ⚙️ Configuration

The application is configured via `application.yaml`. Key configurations include:

### Database Configuration
```yaml
spring:
  datasource:
    url: jdbc:h2:mem:currency_db
    driver-class-name: org.h2.Driver
    username: sa
    password: password
```

### Cache Configuration
```yaml
spring:
  cache:
    type: caffeine
    cache-names: exchange-rates, supported-currencies
    caffeine:
      spec: expireAfterWrite=6h
```

### API Configuration
```yaml
app:
  exchange-rate-api:
    url: https://v6.exchangerate-api.com/v6
    key: YOUR_API_KEY_HERE
```

## 🎯 Running the Application

### Using Maven
```bash
mvn spring-boot:run
```

### Using Java
```bash
java -jar target/realtime_currency_converter-0.0.1-SNAPSHOT.jar
```

### Access the Application
- **Home**: http://localhost:8080/
- **H2 Console**: http://localhost:8080/h2-console
- **Login**: http://localhost:8080/login
- **Register**: http://localhost:8080/register

## 📁 Project Structure

```
realtime_currency_converter/
├── src/
│   ├── main/
│   │   ├── java/com/example/realtime_currency_converter/
│   │   │   ├── RealtimeCurrencyConverterApplication.java
│   │   │   ├── config/
│   │   │   │   └── SecurityConfig.java
│   │   │   ├── controller/
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── CurrencyController.java
│   │   │   │   ├── CryptoController.java
│   │   │   │   └── UnitConverterController.java
│   │   │   ├── model/
│   │   │   │   ├── User.java
│   │   │   │   ├── CurrencyInfo.java
│   │   │   │   └── ExchangeRateResponse.java
│   │   │   ├── repository/
│   │   │   │   └── UserRepository.java
│   │   │   └── service/
│   │   │       ├── UserService.java
│   │   │       ├── CurrencyService.java
│   │   │       ├── CryptoService.java
│   │   │       ├── ExchangeRateClient.java
│   │   │       └── BinanceClient.java
│   │   └── resources/
│   │       ├── application.yaml
│   │       ├── static/
│   │       └── templates/
│   │           ├── home.html
│   │           ├── login.html
│   │           ├── register.html
│   │           ├── dashboard.html
│   │           ├── converter.html
│   │           ├── crypto-converter.html
│   │           ├── unit-converter.html
│   │           └── fragments/
│   │               └── layout.html
│   └── test/
│       └── java/com/example/realtime_currency_converter/
├── pom.xml
└── README.md
```

## 🔗 API Documentation

### Currency Conversion
- **Endpoint**: `/currency/convert`
- **Method**: POST/GET
- **Parameters**: `from`, `to`, `amount`

### Cryptocurrency
- **Endpoint**: `/crypto/price`
- **Method**: GET
- **Parameters**: `symbol` (e.g., BTC, ETH)

### Unit Conversion
- **Endpoint**: `/unit/convert`
- **Method**: POST/GET
- **Parameters**: `from`, `to`, `value`, `type`

### Authentication
- **Login**: POST `/login`
- **Register**: POST `/register`

## 💾 Database

The application uses **H2 Database** in-memory mode for quick development and testing.

### H2 Console Access
- URL: http://localhost:8080/h2-console
- JDBC URL: `jdbc:h2:mem:currency_db`
- Username: `sa`
- Password: `password`

### Database Features
- Automatic schema creation and updates via Hibernate
- JPA persistence for user data
- JPQL queries for data retrieval

## ⚡ Caching

Caffeine caching is enabled with the following configuration:

- **Cache Names**:
  - `exchange-rates`: Cached exchange rate data
  - `supported-currencies`: Cached list of supported currencies
- **Expiration**: 6 hours (`expireAfterWrite=6h`)

This reduces API calls and improves application performance.

## 🔒 Security

### Features
- Spring Security 6 integration
- Form-based authentication
- Password encoding
- Session management
- CSRF protection

### Security Configuration
- Secured endpoints using `SecurityConfig.java`
- Public endpoints: `/login`, `/register`, `/` (home)
- Protected endpoints: Dashboard, conversion functions

## 🏗️ Building & Deployment

### Build for Production
```bash
mvn clean package
```

### Build with Tests
```bash
mvn clean verify
```

### Generate WAR for Deployment
```bash
mvn clean package -Pwar
```

## 🧪 Testing

### Run All Tests
```bash
mvn test
```

### Run Specific Test Class
```bash
mvn test -Dtest=RealtimeCurrencyConverterApplicationTests
```

### Test Coverage
```bash
mvn test jacoco:report
```

## 👥 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is available under the MIT License. See the LICENSE file for more details.

---

## 📞 Support

For issues and questions, please visit the [GitHub Issues](https://github.com/Muskan-zehra12/Realtime-_Converter/issues) page.

## 🙏 Acknowledgments

- **ExchangeRate-API** - For real-time exchange rate data
- **Binance API** - For cryptocurrency price data
- **Spring Boot Team** - For the excellent framework
- **Thymeleaf** - For server-side templating

---

**Version**: 0.0.1-SNAPSHOT  
**Last Updated**: March 2026  
**Repository**: [GitHub](https://github.com/Muskan-zehra12/Realtime-_Converter)