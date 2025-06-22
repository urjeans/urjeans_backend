# Urjeans

Urjeans is a web application for managing jeans inventory and sales. This repository contains the backend server implementation.

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v14 or higher)
- MySQL (v8.0 or higher)
- npm (Node Package Manager)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd Urjeans2
```

2. Navigate to the backend directory:
```bash
cd backend
```

3. Install dependencies:
```bash
npm install
```

4. Create a `.env` file in the backend directory with the following environment variables:
```env
DB_HOST=localhost
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password
DB_NAME=urjeans_db
PORT=3000
```

5. Set up the database:
- Create a new MySQL database named `urjeans_db`
- The database schema can be found in `backend/db-schema.md`

## Running the Application

### Development Mode

To run the server in development mode with auto-reload:

```bash
npm run dev
```

### Production Mode

To run the server in production mode:

```bash
npm start
```

The server will start running on `http://localhost:3000` (or the port specified in your .env file).

## API Documentation

The backend provides RESTful API endpoints for managing jeans inventory. Detailed API documentation can be found in the respective route files under the `backend/routes` directory.

## Project Structure

```
backend/
├── config/         # Configuration files
├── routes/         # API route handlers
├── server.js       # Main application file
├── package.json    # Project dependencies
└── db-schema.md    # Database schema documentation
```

## Dependencies

Main dependencies:
- Express.js - Web framework
- MySQL2 - MySQL database driver
- CORS - Cross-Origin Resource Sharing
- dotenv - Environment variable management

Development dependencies:
- Nodemon - Auto-reload during development

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.
