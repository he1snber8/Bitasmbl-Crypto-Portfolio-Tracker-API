# Bitasmbl-Crypto-Portfolio-Tracker-API

Description:
Build a RESTful API that allows users to track their cryptocurrency investments by fetching live prices, calculating portfolio value, and recording transactions. This project focuses on building secure endpoints, data persistence, and integrating third-party APIs.

## Tech Stack
- ASP.NET Core

## Requirements
- Implement secure authentication using JWT or similar mechanism (Hint: Store tokens safely and verify before allowing portfolio access)
- Fetch live crypto data from public API (CoinGecko, Binance, etc.) (Hint: Use an async service layer to keep routes clean)
- Persist user portfolios and transactions using a database (Hint: Prefer relational DB for consistency or NoSQL for flexibility)

## Installation
bash
# Clone the repository
git clone https://github.com/<your-username>/Bitasmbl-Crypto-Portfolio-Tracker-API.git
cd Bitasmbl-Crypto-Portfolio-Tracker-API

# Set environment variables
export ASPNETCORE_ENVIRONMENT=Development
export JWT_SECRET="your_jwt_secret"
export DB_CONNECTION_STRING="Server=localhost;Database=CryptoTracker;User Id=sa;Password=Your_password123;"
export COINGECKO_API_URL="https://api.coingecko.com/api/v3"

# Restore dependencies and build
dotnet restore
dotnet build
  

## Usage
bash
# Apply EF Core migrations to set up the database
dotnet ef database update

# Run the API
dotnet run

# The API will be available at https://localhost:5001/api
  

## Implementation Steps
1. Initialize a new ASP.NET Core Web API project with `dotnet new webapi`.
2. Install NuGet packages:
   - Microsoft.EntityFrameworkCore
   - Microsoft.EntityFrameworkCore.SqlServer (or preferred provider)
   - Microsoft.EntityFrameworkCore.Tools
   - Microsoft.AspNetCore.Authentication.JwtBearer
   - Swashbuckle.AspNetCore (for Swagger, optional)
3. Configure `appsettings.json` for:
   - ConnectionStrings:DbContext
   - JWT:Secret, Issuer, Audience
   - CoinGecko:BaseUrl
4. Create entity models for User, Portfolio, and Transaction.
5. Implement `ApplicationDbContext` inheriting from `DbContext` and register it in `Startup.cs`.
6. Configure JWT authentication in `Startup.cs` using the secret from environment variables.
7. Implement a service (`CryptoPriceService`) using `IHttpClientFactory` to fetch live prices asynchronously from CoinGecko.
8. Create controllers:
   - `AuthController` for registration and login endpoints.
   - `PortfolioController` for retrieving portfolio and calculating current value.
   - `TransactionsController` for recording and listing transactions.
9. Register all services, DbContext, and authentication middleware in the DI container.
10. Generate and apply EF Core migrations, then test endpoints via Swagger UI or Postman.

## API Endpoints
- POST /api/auth/register : Register a new user
- POST /api/auth/login    : Authenticate and receive a JWT token
- GET  /api/portfolio     : Get the authenticated user’s portfolio
- GET  /api/portfolio/value : Get current total portfolio value
- POST /api/transactions  : Record a new buy/sell transaction