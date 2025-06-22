# Deployment Guide: Urjeans Backend to aHost.uz

This guide will walk you through deploying your Node.js backend application to aHost.uz hosting service.

## Prerequisites

- aHost.uz hosting account with Node.js support
- MySQL database (provided by aHost.uz or external)
- Git repository with your code

## Step 1: Prepare Your Application

### 1.1 Environment Variables
Create a `.env` file in your backend directory with the following variables:

```env
# Server Configuration
PORT=3000
NODE_ENV=production

# Database Configuration
DB_HOST=your_database_host
DB_USER=your_database_user
DB_PASSWORD=your_database_password
DB_NAME=urjeans_db

# Frontend URL (for CORS)
FRONTEND_URL=https://your-frontend-domain.com

# JWT Secret
JWT_SECRET=your_jwt_secret_key
```

### 1.2 Update package.json
Ensure your `package.json` has the correct start script:

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

### 1.3 Create .gitignore
Make sure your `.gitignore` includes:

```
node_modules/
.env
uploads/
*.log
```

## Step 2: Database Setup

### 2.1 Create Database
1. Log into your aHost.uz control panel
2. Navigate to MySQL Databases
3. Create a new database named `urjeans_db`
4. Create a database user with full privileges
5. Note down the database credentials

### 2.2 Import Database Schema
1. Use the database setup script from `backend/database/init.sql`
2. Import it through phpMyAdmin or MySQL command line

## Step 3: aHost.uz Deployment

### 3.1 Upload Your Code
**Option A: Git Deployment (Recommended)**
1. In your aHost.uz control panel, find Git deployment options
2. Connect your Git repository
3. Set the deployment branch (usually `main` or `master`)
4. Configure the deployment path to your backend directory

**Option B: Manual Upload**
1. Compress your backend folder
2. Upload via FTP/SFTP to your hosting directory
3. Extract the files

### 3.2 Configure Node.js Environment
1. In aHost.uz control panel, navigate to Node.js settings
2. Set the Node.js version (recommended: 18.x or 20.x)
3. Set the entry point to `server.js`
4. Configure the port (usually 3000 or as specified by aHost.uz)

### 3.3 Set Environment Variables
1. In your aHost.uz control panel, find environment variables section
2. Add all the variables from your `.env` file
3. Make sure to use production values for all configurations

## Step 4: Install Dependencies

### 4.1 SSH Access (if available)
```bash
# Connect to your server via SSH
ssh username@your-server.com

# Navigate to your project directory
cd /path/to/your/backend

# Install dependencies
npm install --production
```

### 4.2 Via Control Panel
1. Use the terminal/SSH feature in aHost.uz control panel
2. Navigate to your project directory
3. Run `npm install --production`

## Step 5: Configure Domain and SSL

### 5.1 Domain Configuration
1. In aHost.uz control panel, configure your domain
2. Point it to your Node.js application
3. Set up subdomain if needed (e.g., `api.yourdomain.com`)

### 5.2 SSL Certificate
1. Enable SSL certificate for your domain
2. Configure automatic redirects from HTTP to HTTPS
3. Update your CORS settings to use HTTPS

## Step 6: File Uploads Configuration

### 6.1 Create Uploads Directory
```bash
# Create uploads directory
mkdir uploads
chmod 755 uploads
```

### 6.2 Configure File Storage
Your application uses local server storage with the following features:
- **Multer** for file upload handling
- **Sharp** for image processing and optimization
- **Secure filename generation** to prevent conflicts
- **File type validation** (JPEG, PNG, WebP only)
- **File size limits** (5MB per file, max 5 files)
- **Image optimization** (resize to max 1000x1000, JPEG quality 80%)

### 6.3 File Permissions
Ensure the uploads directory has proper permissions:
```bash
# Set proper permissions for uploads directory
chmod 755 uploads
chown www-data:www-data uploads  # Adjust user/group as needed
```

### 6.4 Static File Serving
Your application serves uploaded files through the `/uploads` route. Make sure:
1. The uploads directory is accessible
2. Static file serving is properly configured in your Express app
3. File permissions allow web server to read the files

## Step 7: Process Management

### 7.1 Using PM2 (if available)
Create a `ecosystem.config.js` file:

```javascript
module.exports = {
  apps: [{
    name: 'urjeans-backend',
    script: 'server.js',
    instances: 1,
    autorestart: true,
    watch: false,
    max_memory_restart: '1G',
    env: {
      NODE_ENV: 'production'
    }
  }]
};
```

### 7.2 Start Application
```bash
# Install PM2 globally
npm install -g pm2

# Start the application
pm2 start ecosystem.config.js

# Save PM2 configuration
pm2 save

# Setup PM2 to start on system reboot
pm2 startup
```

## Step 8: Testing Your Deployment

### 8.1 Health Check
Test your API endpoints:

```bash
# Test the root endpoint
curl https://your-domain.com/

# Expected response:
# {"message":"Welcome to Urjeans API"}
```

### 8.2 Database Connection
Check if your application can connect to the database by viewing the logs.

### 8.3 API Endpoints
Test your main API endpoints:
- `GET /api/auth` - Authentication endpoints
- `GET /api/products` - Get all products (public, no authentication required)
- `GET /api/products/:id` - Get single product (public, no authentication required)
- `GET /api/products/brand/:brandName` - Get products by brand (public, no authentication required)
- `POST /api/products` - Create new product (requires admin authentication)
- `PUT /api/products/:id` - Update product (requires admin authentication)
- `DELETE /api/products/:id` - Delete product (requires admin authentication)

## Step 9: Monitoring and Logs

### 9.1 View Application Logs
```bash
# If using PM2
pm2 logs urjeans-backend

# Or check application logs in aHost.uz control panel
```

### 9.2 Monitor Performance
1. Use aHost.uz monitoring tools
2. Set up alerts for high CPU/memory usage
3. Monitor database performance

## Step 10: Security Considerations

### 10.1 Environment Variables
- Never commit `.env` files to version control
- Use strong, unique passwords for database
- Rotate JWT secrets regularly

### 10.2 CORS Configuration
Update your CORS settings to only allow your frontend domain:

```javascript
app.use(cors({
    origin: process.env.FRONTEND_URL,
    credentials: true
}));
```

### 10.3 Rate Limiting
Consider adding rate limiting middleware for production.

## Troubleshooting

### Common Issues

1. **Port Already in Use**
   - Check if another application is using the same port
   - Use the port assigned by aHost.uz

2. **Database Connection Failed**
   - Verify database credentials
   - Check if database server is accessible
   - Ensure firewall allows connections

3. **Environment Variables Not Loading**
   - Verify all variables are set in aHost.uz control panel
   - Check for typos in variable names

4. **File Upload Issues**
   - Verify Cloudinary credentials
   - Check file permissions on uploads directory

### Getting Help

- Check aHost.uz documentation
- Review application logs for error messages
- Contact aHost.uz support for hosting-specific issues

## Maintenance

### Regular Tasks
1. Update Node.js dependencies regularly
2. Monitor application logs
3. Backup database regularly
4. Update SSL certificates before expiration
5. Monitor disk space usage

### Updates
1. Pull latest code from Git repository
2. Install new dependencies: `npm install`
3. Restart the application: `pm2 restart urjeans-backend`

## Support

For hosting-specific issues, contact aHost.uz support.
For application-specific issues, check the application logs and documentation. 