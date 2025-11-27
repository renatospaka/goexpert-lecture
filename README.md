# GoExpert Lecture Challenge

This project is a Go application designed as part of the GoExpert course challenges. It demonstrates a layered architecture with clear separation between entities, DTOs, infrastructure, and web server handlers.


### Prerequisites
- Go 1.18 or higher
- A running PostgreSQL instance (or the database specified in your `.env` file)


### Environment Variables (`.env`)

The project uses a `.env` file for sensitive configuration (database credentials, ports, etc.).

**Important:** The `.env` file is not included in the repository for security reasons. You must create your own `.env` file in the project root.

Example `.env`:

```env
DB_HOST=localhost
DB_PORT=5432
DB_USER=youruser
DB_PASSWORD=yourpassword
DB_NAME=yourdb
APP_PORT=8080
JWT_SECRET=your_jwt_secret_key  # Secret key used to sign and verify JWT tokens. Keep this value safe and do not share it.
JWT_EXPIRES_IN=604800           # Token expiration time in seconds. Example: 604800 = 1 week.
```

#### Attribute Details
- **JWT_SECRET**: Secret key used to sign and verify JWT tokens. This should be a strong, random string and must be kept confidential. If this value changes, all previously issued tokens become invalid.
- **JWT_EXPIRES_IN**: Number of seconds a JWT token remains valid after being issued. For example, `604800` means tokens expire after 1 week. Adjust as needed for your security requirements.

Adjust the values as needed for your environment.

### Running the Application

1. Install dependencies:
   ```bash
   go mod tidy
   ```
2. Run the server:
   ```bash
   go run cmd/server/main.go
   ```


## Testing

The `tests/` directory contains `.http` files (`user.http` and `product.http`) for manual or automated API testing. These files are compatible with VS Code's REST Client extension or similar tools.

### How to Use the HTTP Test Files

#### 1. `user.http`
This file demonstrates the authentication flow:

1. **Create a user**: Send a POST request to `/users` with a unique email, name, and password.
2. **Generate a fresh token**: Send a POST request to `/users/generate_token` with the same email and password to receive a valid JWT token in the response.

#### 2. `product.http`
This file demonstrates how to interact with the `/products` endpoints:

1. **Update the Bearer token**: Copy the JWT token generated in `user.http` (step 2) and paste it into the `Authorization: Bearer <PASTE_TOKEN_HERE>` header in all requests.
2. **Create a product**: Send a POST request to `/products` with product data. The response will include a product UUID.
3. **Use the product UUID**: For all subsequent requests (GET, PUT, DELETE), replace `<PRODUCT_UUID>` in the URL with the actual UUID returned from the product creation response. This ensures all operations target the product you just created.

**Example workflow:**
1. Run the requests in `user.http` to create a user and obtain a token.
2. Use the token in `product.http` to create and manage products, always updating the UUID as needed.

You can use the "Send Request" action in VS Code or your preferred HTTP client to execute each step.

## Notes

- The `.env` file is required for the application to run. If missing, the server may fail to start or connect to the database.
- The `.http` files in `tests/` are not tests in the Go sense, but are for API endpoint validation and exploration.

## License

This project is for educational purposes as part of the Pos Graduation GoExpert course.
