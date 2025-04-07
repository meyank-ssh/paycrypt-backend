# Cryptocurrency Payment System

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Go Version](https://img.shields.io/badge/go-1.21%2B-00ADD8.svg)
[![API Documentation](https://img.shields.io/badge/docs-API-orange.svg)](docs/api-documentation.md)

**A secure, scalable cryptocurrency payment infrastructure for modern businesses.**

</div>

## Overview

The Cryptocurrency Payment System is an enterprise-grade platform enabling businesses to seamlessly accept, process, and manage cryptocurrency payments. Built with security, scalability, and usability as core principles, the system supports multiple blockchain networks and cryptocurrencies through a clean, RESTful API architecture.

### Key Features

- **Multi-Currency Support**: Process transactions in BTC, ETH, USDT, SOL, and USDC
- **Advanced Security**: Industry-standard encryption, secure key management, and comprehensive authentication
- **HD Wallet Infrastructure**: BIP32/BIP44 hierarchical deterministic wallet architecture for address management
- **Robust API**: RESTful endpoints with comprehensive documentation and examples
- **Transaction Monitoring**: Real-time payment status tracking with webhook notifications
- **Merchant Management**: Complete merchant account and authentication system
- **Production-Ready**: Containerized deployment, database migrations, and monitoring

## System Architecture

```mermaid
graph TD
    subgraph Client Layer
        Web[Web Interface]
        Mobile[Mobile App]
        API[API Integration]
    end

    subgraph Service Layer
        Auth[Authentication Service]
        Payment[Payment Processing]
        Wallet[Wallet Management]
        Merchant[Merchant Service]
    end

    subgraph Data Layer
        DB[(PostgreSQL)]
        Cache[(Redis)]
    end

    subgraph Blockchain Layer
        EthNode[Ethereum Node]
        BtcNode[Bitcoin Node]
        SolNode[Solana Node]
    end

    Client Layer --> Service Layer
    Service Layer --> Data Layer
    Service Layer --> Blockchain Layer
```

## Technology Stack

- **Backend**: Go 1.21+ with Gin framework
- **Database**: PostgreSQL with GORM ORM
- **Authentication**: JWT and API key authentication
- **Logging**: Structured logging with Zap
- **Containerization**: Docker and Docker Compose
- **API Documentation**: OpenAPI 3.0

## Quick Start

### Prerequisites

- Go 1.21 or higher
- PostgreSQL 13+
- Docker and Docker Compose (optional for containerized deployment)

### Environment Setup

1. Clone the repository:

```bash
git clone https://github.com/yourusername/payment-system.git
cd payment-system
```

2. Configure environment variables:

```bash
cp .env.example .env
```

Edit `.env` with your specific configuration:

```env
# Database Configuration
DATABASE_URL=postgres://username:password@localhost:5432/payment_system
DATABASE_MAX_CONNECTIONS=100
DATABASE_MAX_IDLE_CONNECTIONS=10

# Security
JWT_SECRET=your_secure_jwt_secret_key
API_KEY_PREFIX=sova

# Server Configuration
PORT=8080
ENV=production
```

### Local Development

1. Install dependencies:

```bash
go mod download
```

2. Run the application:

```bash
go run cmd/main.go
```

The API will be available at `http://localhost:8080`

### Docker Deployment

1. Build and start containers:

```bash
docker-compose up -d
```

2. Monitor container logs:

```bash
docker-compose logs -f
```

### Testing

Run the test suite:

```bash
go test ./... -v
```

## API Overview

The system provides a comprehensive RESTful API for all payment operations. See [API Documentation](docs/api-documentation.md) for complete details.

### Core Endpoints

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/auth/register` | POST | Register new merchant | None |
| `/auth/login` | POST | Authenticate merchant | None |
| `/api/keys/generate` | POST | Generate API key | JWT |
| `/payment/create-order` | POST | Create payment request | JWT or API Key |
| `/payment/:id` | GET | Get payment details | JWT or API Key |
| `/wallet/create` | GET | Create merchant wallets | JWT |

### Authentication

The system supports two authentication methods:

1. **JWT Tokens**: For user sessions
   ```
   Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
   ```

2. **API Keys**: For programmatic access
   ```
   X-API-Key: sova-a1b2c3d4-e5f6-7890-abcd-ef1234567890
   ```

## Project Structure

```
payment-system/
├── cmd/                # Application entry points
│   └── main.go         # Main server executable
├── docs/               # Documentation
│   ├── overview.md          # System overview
│   ├── api-documentation.md # API reference
│   └── business-use-cases.md # Integration examples
├── internal/           # Private application code
│   ├── handlers/       # HTTP request handlers
│   ├── logger/         # Logging configuration
│   ├── middleware/     # HTTP middleware
│   ├── models/         # Data models and database schema
│   ├── repository/     # Database access layer
│   ├── routes/         # API route definitions
│   ├── server/         # Server configuration
│   └── service/        # Business logic
├── utils/              # Utility functions
├── .env.example        # Example environment configuration
├── docker-compose.yml  # Docker Compose configuration
├── Dockerfile          # Docker build configuration
└── go.mod              # Go module definition
```

## Security Considerations

The platform implements multiple layers of security:

- **Authentication**: JWT tokens with expiration and API keys with rotation
- **Data Protection**: Encryption for sensitive data at rest and in transit
- **Wallet Security**: BIP39 seed phrases with AES-256 encryption
- **Input Validation**: Comprehensive validation for all API inputs
- **Database Security**: Parameterized queries and input sanitization
- **Logging**: Structured logging with sensitive data masking
- **Rate Limiting**: Protection against brute force attacks
- **HTTPS**: TLS for all connections in production

## Performance Optimization

- Database connection pooling
- Efficient database query design
- Memcached for transient data
- Asynchronous background processing for blockchain interactions
- Transaction batching for high-volume operations

## Monitoring and Observability

- Structured logging with correlation IDs
- Performance metrics collection
- Transaction lifecycle tracking
- Error aggregation and alerting

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

For inquiries, please contact:

- **Support Email**: support@paycrypt.com
- **API Support**: api-support@paycrypt.com
