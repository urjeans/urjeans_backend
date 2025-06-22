# Deployment Quick Reference

## Essential Commands

### Initial Setup
```bash
# Upload code to server
git clone your-repository-url
cd backend

# Create environment file
cp .env.example .env
# Edit .env with your production values

# Run deployment script
./deploy.sh
```

### PM2 Management
```bash
# Start application
pm2 start ecosystem.config.js

# View status
pm2 status

# View logs
pm2 logs urjeans-backend

# Restart application
pm2 restart urjeans-backend

# Stop application
pm2 stop urjeans-backend

# Delete application
pm2 delete urjeans-backend
```

### Manual Deployment
```bash
# Install dependencies
npm install --production

# Start application
node server.js

# Or with PM2
pm2 start server.js --name urjeans-backend
```

## Environment Variables Checklist

- [ ] `PORT` - Server port (usually 3000)
- [ ] `NODE_ENV` - Set to "production"
- [ ] `DB_HOST` - Database host
- [ ] `DB_USER` - Database username
- [ ] `DB_PASSWORD` - Database password
- [ ] `DB_NAME` - Database name (urjeans_db)
- [ ] `FRONTEND_URL` - Your frontend domain
- [ ] `JWT_SECRET` - Strong JWT secret key

## Testing Endpoints

```bash
# Health check
curl https://your-domain.com/

# Expected: {"message":"Welcome to Urjeans API"}

# Test auth endpoint
curl https://your-domain.com/api/auth

# Test public product endpoints (no authentication required)
curl https://your-domain.com/api/products
curl https://your-domain.com/api/products/1
curl https://your-domain.com/api/products/brand/Levi's

# Test protected product endpoints (requires admin authentication)
curl -X POST -H "Authorization: Bearer YOUR_TOKEN" https://your-domain.com/api/products
curl -X PUT -H "Authorization: Bearer YOUR_TOKEN" https://your-domain.com/api/products/1
curl -X DELETE -H "Authorization: Bearer YOUR_TOKEN" https://your-domain.com/api/products/1
```

## Troubleshooting

### Common Issues
1. **Port in use**: Check `pm2 status` and stop conflicting processes
2. **Database connection**: Verify credentials in `.env`
3. **Environment variables**: Ensure all are set in aHost.uz control panel
4. **File uploads**: Check uploads directory permissions and disk space
5. **Static files not serving**: Verify uploads directory exists and has proper permissions

### Log Locations
- PM2 logs: `pm2 logs urjeans-backend`
- Application logs: `./logs/` directory
- System logs: Check aHost.uz control panel

## Security Checklist

- [ ] SSL certificate enabled
- [ ] Strong JWT secret
- [ ] Database credentials secured
- [ ] CORS configured for production
- [ ] Environment variables not in version control
- [ ] File uploads directory secured

## Maintenance

### Regular Tasks
- Monitor logs: `pm2 logs urjeans-backend`
- Update dependencies: `npm update`
- Backup database regularly
- Check disk space usage
- Monitor application performance

### Updates
```bash
# Pull latest code
git pull origin main

# Install new dependencies
npm install

# Restart application
pm2 restart urjeans-backend
```

## Support Contacts

- **aHost.uz Support**: For hosting issues
- **Application Logs**: For debugging application issues
- **Database Issues**: Check MySQL connection and credentials 