# Fullstack MERN Generative AI Project

A full-stack application built with the MERN stack (MongoDB, Express.js, React, Node.js) featuring generative AI capabilities. This project provides a scalable foundation for building AI-powered web applications with modern web technologies.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Environment Variables Setup](#environment-variables-setup)
- [MongoDB Setup](#mongodb-setup)
  - [Option 1: Local MongoDB](#option-1-local-mongodb)
  - [Option 2: MongoDB Atlas (Cloud)](#option-2-mongodb-atlas-cloud)
- [Backend Setup and Installation](#backend-setup-and-installation)
- [Frontend Setup and Installation](#frontend-setup-and-installation)
- [Running the Application](#running-the-application)
- [Troubleshooting and Common Errors](#troubleshooting-and-common-errors)
- [Azure DevBox / Cloud Deployment](#azure-devbox--cloud-deployment)
- [Security Best Practices](#security-best-practices)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Full-Stack MERN Architecture**: MongoDB, Express.js, React, and Node.js
- **Generative AI Integration**: Ready for AI model integration (OpenAI, Azure OpenAI, etc.)
- **RESTful API**: Backend API with Express.js
- **Modern React Frontend**: Component-based UI with hooks
- **Authentication & Authorization**: User management system
- **Cloud-Ready**: Configured for Azure and other cloud deployments
- **Environment-Based Configuration**: Separate dev/prod configurations

## Prerequisites

Before you begin, ensure you have the following installed on your system:

### Required Software

- **Node.js** (v16.x or higher) - [Download](https://nodejs.org/)
- **npm** (v8.x or higher) or **yarn** (v1.22.x or higher)
- **MongoDB** (v5.x or higher) - [Download](https://www.mongodb.com/try/download/community) OR MongoDB Atlas account
- **Git** - [Download](https://git-scm.com/downloads)

### Optional but Recommended

- **Postman** or **Thunder Client** (for API testing)
- **MongoDB Compass** (for database GUI)
- **VS Code** with extensions:
  - ESLint
  - Prettier
  - MongoDB for VS Code
  - React Developer Tools

### For Azure Deployment

- **Azure CLI** - [Install](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- **Azure Account** - [Sign up](https://azure.microsoft.com/free/)
- **Azure DevBox** access (if using Azure DevBox)

### Verify Installation

```bash
# Check Node.js version
node --version

# Check npm version
npm --version

# Check MongoDB version (if installed locally)
mongod --version

# Check Git version
git --version
```

## Project Structure

```
Fullstack-MERN-generative-AI-Project/
├── backend/                    # Backend (Node.js + Express)
│   ├── config/                # Configuration files
│   │   └── db.js             # Database connection
│   ├── controllers/           # Request handlers
│   ├── models/                # MongoDB models (Mongoose schemas)
│   ├── routes/                # API routes
│   ├── middleware/            # Custom middleware (auth, error handling)
│   ├── utils/                 # Utility functions
│   ├── .env                   # Environment variables (DO NOT COMMIT)
│   ├── .env.example          # Environment variables template
│   ├── server.js             # Entry point
│   └── package.json          # Backend dependencies
│
├── frontend/                   # Frontend (React)
│   ├── public/                # Static files
│   ├── src/
│   │   ├── components/       # React components
│   │   ├── pages/            # Page components
│   │   ├── services/         # API service calls
│   │   ├── context/          # React context (state management)
│   │   ├── utils/            # Utility functions
│   │   ├── App.js            # Main App component
│   │   └── index.js          # Entry point
│   ├── .env                   # Frontend environment variables (DO NOT COMMIT)
│   ├── .env.example          # Frontend environment template
│   └── package.json          # Frontend dependencies
│
├── .gitignore                 # Git ignore rules
├── README.md                  # This file
└── LICENSE                    # License information
```

## Environment Variables Setup

### Backend Environment Variables

Create a `.env` file in the `backend/` directory with the following variables:

```bash
# Copy the example file
cd backend
cp .env.example .env
```

**backend/.env** (edit with your values):

```env
# Server Configuration
NODE_ENV=development
PORT=5000
HOST=localhost

# MongoDB Configuration
# For local MongoDB:
MONGODB_URI=mongodb://localhost:27017/mern-ai-db

# For MongoDB Atlas:
# MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/<dbname>?retryWrites=true&w=majority

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=7d

# AI API Configuration (choose your provider)
# OpenAI
OPENAI_API_KEY=sk-your-openai-api-key-here
OPENAI_MODEL=gpt-3.5-turbo

# Azure OpenAI (alternative)
# AZURE_OPENAI_API_KEY=your-azure-openai-key
# AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
# AZURE_OPENAI_DEPLOYMENT_NAME=your-deployment-name

# CORS Configuration
CORS_ORIGIN=http://localhost:3000

# Email Configuration (optional)
# SMTP_HOST=smtp.gmail.com
# SMTP_PORT=587
# SMTP_USER=your-email@gmail.com
# SMTP_PASS=your-app-password

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

### Frontend Environment Variables

Create a `.env` file in the `frontend/` directory:

```bash
cd frontend
cp .env.example .env
```

**frontend/.env** (edit with your values):

```env
# API Configuration
REACT_APP_API_URL=http://localhost:5000/api

# Environment
REACT_APP_ENV=development

# Optional: Analytics, etc.
# REACT_APP_GOOGLE_ANALYTICS_ID=UA-XXXXXXXXX-X
```

### Important Security Notes

- **NEVER commit `.env` files to version control**
- Always use `.env.example` files as templates (without actual secrets)
- Use different secrets for development and production
- Rotate API keys and secrets regularly

## MongoDB Setup

You have two options for MongoDB: local installation or cloud-based MongoDB Atlas.

### Option 1: Local MongoDB

#### Installation

**Windows:**
1. Download MongoDB Community Server from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Run the installer (use default settings)
3. MongoDB will install as a Windows service and start automatically

**macOS (using Homebrew):**
```bash
# Install MongoDB
brew tap mongodb/brew
brew install mongodb-community@5.0

# Start MongoDB service
brew services start mongodb-community@5.0
```

**Linux (Ubuntu/Debian):**
```bash
# Import MongoDB public GPG key
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

# Create list file
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

# Install MongoDB
sudo apt-get update
sudo apt-get install -y mongodb-org

# Start MongoDB
sudo systemctl start mongod
sudo systemctl enable mongod
```

#### Verify Local MongoDB Installation

```bash
# Check if MongoDB is running
mongosh

# In MongoDB shell:
show dbs
exit
```

#### Local MongoDB Connection String

```env
MONGODB_URI=mongodb://localhost:27017/mern-ai-db
```

### Option 2: MongoDB Atlas (Cloud)

MongoDB Atlas is a fully-managed cloud database service (free tier available).

#### Setup Steps

1. **Create an Account**
   - Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
   - Sign up for a free account

2. **Create a Cluster**
   - Click "Build a Database"
   - Choose "Shared" (free tier)
   - Select your cloud provider (AWS, Azure, or GCP) and region
   - Click "Create Cluster" (takes 3-5 minutes)

3. **Configure Database Access**
   - Go to "Database Access" in the left sidebar
   - Click "Add New Database User"
   - Choose "Password" authentication
   - Create username and password (save these!)
   - Set privileges to "Read and write to any database"
   - Click "Add User"

4. **Configure Network Access**
   - Go to "Network Access" in the left sidebar
   - Click "Add IP Address"
   - For development: Click "Allow Access from Anywhere" (0.0.0.0/0)
   - For production: Add specific IP addresses
   - Click "Confirm"

5. **Get Connection String**
   - Go to "Database" in the left sidebar
   - Click "Connect" on your cluster
   - Choose "Connect your application"
   - Copy the connection string
   - Replace `<password>` with your database user password
   - Replace `<dbname>` with your database name (e.g., `mern-ai-db`)

#### MongoDB Atlas Connection String

```env
MONGODB_URI=mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/mern-ai-db?retryWrites=true&w=majority
```

**Important:** Replace:
- `username` - your database username
- `password` - your database password
- `cluster0.xxxxx.mongodb.net` - your cluster URL
- `mern-ai-db` - your database name

## Backend Setup and Installation

### Step 1: Navigate to Backend Directory

```bash
cd backend
```

### Step 2: Install Dependencies

```bash
# Using npm
npm install

# Or using yarn
yarn install
```

### Step 3: Configure Environment Variables

```bash
# Copy example env file
cp .env.example .env

# Edit .env file with your configuration
# Use your preferred text editor
nano .env
# or
code .env
```

### Step 4: Verify MongoDB Connection

```bash
# Test the backend setup
npm run test-connection

# Or start the server and check logs
npm run dev
```

### Step 5: Seed Database (Optional)

```bash
# If seed scripts are available
npm run seed
```

### Backend npm Scripts

```bash
# Development mode (with hot reload)
npm run dev

# Production mode
npm start

# Run tests
npm test

# Lint code
npm run lint

# Format code
npm run format
```

## Frontend Setup and Installation

### Step 1: Navigate to Frontend Directory

```bash
cd frontend
```

### Step 2: Install Dependencies

```bash
# Using npm
npm install

# Or using yarn
yarn install
```

### Step 3: Configure Environment Variables

```bash
# Copy example env file
cp .env.example .env

# Edit .env file
nano .env
# or
code .env
```

Make sure `REACT_APP_API_URL` points to your backend:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

### Step 4: Start Development Server

```bash
# Using npm
npm start

# Or using yarn
yarn start
```

The application will open in your browser at `http://localhost:3000`

### Frontend npm Scripts

```bash
# Start development server
npm start

# Build for production
npm run build

# Run tests
npm test

# Eject (one-way operation)
npm run eject
```

## Running the Application

### Development Mode (Full Stack)

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```

The backend API will run on `http://localhost:5000`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm start
```

The frontend will run on `http://localhost:3000`

### Production Mode

**Build Frontend:**
```bash
cd frontend
npm run build
```

**Serve Static Files from Backend:**
```bash
cd backend
# Configure Express to serve static files from frontend/build
npm start
```

### Testing the Application

1. **Open Browser**: Navigate to `http://localhost:3000`
2. **API Health Check**: Visit `http://localhost:5000/api/health`
3. **Test Registration**: Create a new user account
4. **Test Login**: Log in with credentials
5. **Test AI Features**: Try AI-powered features

## Troubleshooting and Common Errors

### MongoDB Connection Issues

**Error: `MongooseServerSelectionError: connect ECONNREFUSED 127.0.0.1:27017`**

**Solutions:**
```bash
# Check if MongoDB is running
# Windows
services.msc  # Look for MongoDB service

# macOS
brew services list

# Linux
sudo systemctl status mongod

# Start MongoDB if not running
# macOS
brew services start mongodb-community@5.0

# Linux
sudo systemctl start mongod
```

**Error: `MongooseServerSelectionError: Could not connect to any servers in your MongoDB Atlas cluster`**

**Solutions:**
- Verify your IP address is whitelisted in Atlas Network Access
- Check username and password in connection string
- Ensure password doesn't contain special characters (URL encode if needed)
- Verify cluster is active and not paused

### Port Already in Use

**Error: `Error: listen EADDRINUSE: address already in use :::5000`**

**Solutions:**
```bash
# Find process using the port
# Windows
netstat -ano | findstr :5000

# macOS/Linux
lsof -i :5000

# Kill the process
# Windows (replace PID)
taskkill /PID <PID> /F

# macOS/Linux (replace PID)
kill -9 <PID>

# Or change port in backend/.env
PORT=5001
```

### Module Not Found Errors

**Error: `Error: Cannot find module 'xyz'`**

**Solutions:**
```bash
# Delete node_modules and package-lock.json
rm -rf node_modules package-lock.json

# Reinstall dependencies
npm install

# Or use npm ci for clean install
npm ci
```

### CORS Errors

**Error: `Access to fetch at 'http://localhost:5000/api/...' from origin 'http://localhost:3000' has been blocked by CORS policy`**

**Solutions:**
- Ensure `CORS_ORIGIN` in backend `.env` includes your frontend URL
- Check CORS middleware configuration in backend
- Verify frontend is making requests to correct API URL

### Environment Variables Not Loading

**Error: `undefined` when accessing `process.env.REACT_APP_*`**

**Solutions:**
- Ensure `.env` file is in correct directory
- Restart development server after changing `.env`
- Check variable names start with `REACT_APP_` for frontend
- Don't use quotes around values in `.env` file

### npm Install Failures

**Error: `npm ERR! code EACCES` or permission errors**

**Solutions:**
```bash
# Never use sudo with npm (security risk)
# Fix npm permissions
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Or use nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 16
nvm use 16
```

### Build Errors

**Error: `JavaScript heap out of memory`**

**Solutions:**
```bash
# Increase Node.js memory limit
export NODE_OPTIONS="--max-old-space-size=4096"

# Or in package.json scripts:
"scripts": {
  "build": "NODE_OPTIONS='--max-old-space-size=4096' react-scripts build"
}
```

### API Key Issues

**Error: `401 Unauthorized` or `Invalid API Key`**

**Solutions:**
- Verify API key is correct in `.env`
- Check for extra spaces or quotes around API key
- Ensure API key has correct permissions
- Verify API key hasn't expired or been revoked
- Check rate limits haven't been exceeded

## Azure DevBox / Cloud Deployment

### Azure App Service Deployment

#### Prerequisites

```bash
# Install Azure CLI
# Follow: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

# Login to Azure
az login

# Set subscription (if you have multiple)
az account set --subscription "<subscription-id>"
```

#### Method 1: Deploy Using Azure CLI

**Step 1: Create Resource Group**
```bash
az group create --name mern-ai-rg --location eastus
```

**Step 2: Create App Service Plan**
```bash
az appservice plan create \
  --name mern-ai-plan \
  --resource-group mern-ai-rg \
  --sku B1 \
  --is-linux
```

**Step 3: Create Web App for Backend**
```bash
az webapp create \
  --resource-group mern-ai-rg \
  --plan mern-ai-plan \
  --name mern-ai-backend-<unique-id> \
  --runtime "NODE|16-lts"
```

**Step 4: Configure Environment Variables**
```bash
az webapp config appsettings set \
  --resource-group mern-ai-rg \
  --name mern-ai-backend-<unique-id> \
  --settings \
    NODE_ENV=production \
    MONGODB_URI="<your-mongodb-atlas-uri>" \
    JWT_SECRET="<your-jwt-secret>" \
    OPENAI_API_KEY="<your-openai-key>"
```

**Step 5: Deploy Backend Code**
```bash
cd backend

# Create deployment zip
zip -r deploy.zip . -x "*.git*" "node_modules/*" ".env"

# Deploy
az webapp deployment source config-zip \
  --resource-group mern-ai-rg \
  --name mern-ai-backend-<unique-id> \
  --src deploy.zip
```

**Step 6: Create and Deploy Frontend**
```bash
cd ../frontend

# Update .env for production
echo "REACT_APP_API_URL=https://mern-ai-backend-<unique-id>.azurewebsites.net/api" > .env.production

# Build
npm run build

# Deploy frontend (using Azure Static Web Apps or App Service)
az webapp create \
  --resource-group mern-ai-rg \
  --plan mern-ai-plan \
  --name mern-ai-frontend-<unique-id> \
  --runtime "NODE|16-lts"

# Deploy build folder
cd build
zip -r ../frontend-deploy.zip .
cd ..

az webapp deployment source config-zip \
  --resource-group mern-ai-rg \
  --name mern-ai-frontend-<unique-id> \
  --src frontend-deploy.zip
```

#### Method 2: Deploy Using GitHub Actions

Create `.github/workflows/azure-deploy.yml`:

```yaml
name: Deploy to Azure

on:
  push:
    branches: [ main ]

env:
  AZURE_WEBAPP_NAME: mern-ai-backend
  NODE_VERSION: '16.x'

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: ${{ env.NODE_VERSION }}
    
    - name: Install backend dependencies
      run: |
        cd backend
        npm ci
    
    - name: Build frontend
      run: |
        cd frontend
        npm ci
        npm run build
    
    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: ./backend
```

**Configure GitHub Secrets:**
1. Go to repository Settings → Secrets → Actions
2. Add `AZURE_WEBAPP_PUBLISH_PROFILE` (download from Azure Portal)

#### Method 3: Azure DevBox Setup

Azure DevBox provides pre-configured cloud-hosted development environments.

**Step 1: Access Azure DevBox**
```bash
# Login to Azure DevBox portal
# https://devbox.microsoft.com/

# Or use Azure CLI
az extension add --name dev-box
az devbox list
```

**Step 2: Connect to DevBox**
- Use Remote Desktop or browser-based connection
- Clone repository in DevBox environment
- Follow local development setup steps above

**Step 3: Benefits of Azure DevBox**
- Pre-configured development tools
- Consistent environment across team
- Access from anywhere
- Integrated with Azure services
- Automatic backups and snapshots

### Azure Resources Checklist

After deployment, verify:
- [ ] Resource Group created
- [ ] App Service Plan created
- [ ] Backend Web App running
- [ ] Frontend Web App or Static Web App running
- [ ] Environment variables configured
- [ ] MongoDB Atlas connection working
- [ ] CORS configured for production domains
- [ ] SSL/TLS certificates active (HTTPS)
- [ ] Application Insights configured (monitoring)
- [ ] Backup and disaster recovery plan

### Cost Management

**Free Tier Options:**
- MongoDB Atlas: 512MB storage (M0 cluster)
- Azure App Service: F1 Free tier (limited)
- Azure Static Web Apps: Free tier for frontend

**Optimize Costs:**
```bash
# Stop resources when not in use
az webapp stop --name <app-name> --resource-group <resource-group>

# Start when needed
az webapp start --name <app-name> --resource-group <resource-group>

# Monitor costs
az consumption usage list --start-date 2025-01-01 --end-date 2025-01-31
```

## Security Best Practices

### 1. Environment Variables & Secrets

```bash
# ✅ DO
- Store secrets in .env files (never commit)
- Use Azure Key Vault for production secrets
- Rotate API keys regularly
- Use different secrets for dev/staging/production

# ❌ DON'T
- Hard-code secrets in source code
- Commit .env files to version control
- Share secrets via email or chat
- Use simple or default passwords
```

### 2. Authentication & Authorization

```javascript
// ✅ DO
- Implement JWT with short expiration times
- Use bcrypt for password hashing (min 10 rounds)
- Implement refresh token rotation
- Add rate limiting on auth endpoints
- Use HTTPS only in production
- Implement account lockout after failed attempts

// ❌ DON'T
- Store passwords in plain text
- Use weak JWT secrets
- Skip input validation
- Allow unlimited login attempts
```

### 3. API Security

```javascript
// ✅ DO
- Validate and sanitize all inputs
- Use parameterized queries (prevent SQL/NoSQL injection)
- Implement rate limiting
- Use CORS appropriately
- Add request size limits
- Implement API versioning
- Log security events

// ❌ DON'T
- Trust user input
- Expose detailed error messages to clients
- Allow unlimited API calls
- Skip authentication on sensitive endpoints
```

### 4. MongoDB Security

```javascript
// ✅ DO
- Use MongoDB Atlas with IP whitelisting
- Enable authentication
- Use least privilege principle for database users
- Regularly backup database
- Encrypt data at rest and in transit
- Monitor for suspicious queries

// ❌ DON'T
- Use default MongoDB credentials
- Allow 0.0.0.0/0 in production Network Access
- Store sensitive data unencrypted
- Skip regular security updates
```

### 5. Dependency Security

```bash
# Audit dependencies regularly
npm audit

# Fix vulnerabilities
npm audit fix

# Check for outdated packages
npm outdated

# Update dependencies
npm update

# Use security tools
npm install -g snyk
snyk test
```

### 6. Code Security

```javascript
// ✅ DO
- Use ESLint security plugins
- Implement Content Security Policy (CSP)
- Sanitize HTML to prevent XSS
- Use prepared statements
- Implement CSRF protection
- Keep dependencies updated
- Review code for security issues

// ❌ DON'T
- Use eval() or similar functions
- Render user input directly as HTML
- Skip security headers
- Ignore security warnings
```

### 7. Production Deployment Security

```bash
# ✅ DO Checklist
- [ ] Use HTTPS everywhere (TLS 1.2+)
- [ ] Set secure HTTP headers (helmet.js)
- [ ] Enable CORS for specific origins only
- [ ] Disable debug/verbose error messages
- [ ] Implement logging and monitoring
- [ ] Use environment-specific configurations
- [ ] Regular security audits
- [ ] Implement automated backups
- [ ] Use Web Application Firewall (WAF)
- [ ] Regular penetration testing

# ❌ DON'T
- [ ] Use HTTP in production
- [ ] Expose stack traces
- [ ] Allow access from any origin
- [ ] Skip monitoring and alerting
```

### 8. Azure-Specific Security

```bash
# Enable Azure Security Features
- Use Azure Key Vault for secrets
- Enable Azure AD authentication
- Configure Azure Firewall
- Use Managed Identities
- Enable Azure Defender
- Configure Application Gateway with WAF
- Use Azure Monitor and Security Center
- Implement Azure Private Link
```

### 9. Security Headers (Express.js)

```javascript
// Install helmet
npm install helmet

// In server.js
const helmet = require('helmet');
app.use(helmet());

// Custom security headers
app.use((req, res, next) => {
  res.setHeader('X-Content-Type-Options', 'nosniff');
  res.setHeader('X-Frame-Options', 'DENY');
  res.setHeader('X-XSS-Protection', '1; mode=block');
  res.setHeader('Strict-Transport-Security', 'max-age=31536000; includeSubDomains');
  next();
});
```

### 10. Regular Security Checklist

Weekly:
- [ ] Review access logs for anomalies
- [ ] Check for failed authentication attempts
- [ ] Review error logs

Monthly:
- [ ] Run npm audit and fix vulnerabilities
- [ ] Review and rotate API keys if needed
- [ ] Update dependencies
- [ ] Review user access and permissions

Quarterly:
- [ ] Security audit of codebase
- [ ] Review and update security policies
- [ ] Disaster recovery drill
- [ ] Third-party security assessment

## Contributing

We welcome contributions! Please follow these guidelines:

### Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/your-username/Fullstack-MERN-generative-AI-Project.git`
3. Create a branch: `git checkout -b feature/your-feature-name`
4. Make your changes
5. Test thoroughly
6. Commit: `git commit -m "Add: your feature description"`
7. Push: `git push origin feature/your-feature-name`
8. Open a Pull Request

### Code Style

- Follow ESLint and Prettier configurations
- Write meaningful commit messages
- Add comments for complex logic
- Update documentation as needed

### Testing

- Write tests for new features
- Ensure all tests pass before submitting PR
- Include edge cases in tests

### Pull Request Guidelines

- Provide clear description of changes
- Reference related issues
- Include screenshots for UI changes
- Ensure CI/CD checks pass

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

---

## Quick Start Summary

**For Developers (First Time Setup):**

```bash
# 1. Clone repository
git clone https://github.com/orkinosai25-org/Fullstack-MERN-generative-AI-Project.git
cd Fullstack-MERN-generative-AI-Project

# 2. Setup Backend
cd backend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev

# 3. Setup Frontend (new terminal)
cd ../frontend
npm install
cp .env.example .env
# Edit .env with your configuration
npm start

# 4. Access application
# Frontend: http://localhost:3000
# Backend: http://localhost:5000
```

**For Azure Deployment:**

```bash
# 1. Login to Azure
az login

# 2. Create resources
az group create --name mern-ai-rg --location eastus
az appservice plan create --name mern-ai-plan --resource-group mern-ai-rg --sku B1 --is-linux

# 3. Deploy backend
cd backend
az webapp create --resource-group mern-ai-rg --plan mern-ai-plan --name mern-ai-backend-<unique-id> --runtime "NODE|16-lts"
zip -r deploy.zip . -x "*.git*" "node_modules/*" ".env"
az webapp deployment source config-zip --resource-group mern-ai-rg --name mern-ai-backend-<unique-id> --src deploy.zip

# 4. Deploy frontend
cd ../frontend
npm run build
# Deploy build folder to Azure Static Web Apps or App Service
```

## Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check documentation above
- Review troubleshooting section

---

**Ready to build something amazing? Let's get started! 🚀**
