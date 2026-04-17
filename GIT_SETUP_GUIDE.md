# Git Setup & Deployment Guide

## Quick Start for Git

### 1. Initialize Your Repository

```bash
# Clone or extract the project
git clone <your-repo-url> expense-tracker
cd expense-tracker

# Or if you have the archive
tar -xzf expense-tracker-git-ready.tar.gz
cd expense-tracker
```

### 2. Install Dependencies

```bash
pnpm install
```

### 3. Setup Environment Variables

Create a `.env.local` file in the project root:

```env
# Database
DATABASE_URL=mysql://user:password@localhost:3306/expense_tracker

# OAuth
VITE_APP_ID=your_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://portal.manus.im

# JWT
JWT_SECRET=your_jwt_secret_key

# Owner Info
OWNER_OPEN_ID=your_open_id
OWNER_NAME=Your Name

# API Keys
BUILT_IN_FORGE_API_KEY=your_api_key
BUILT_IN_FORGE_API_URL=https://api.manus.im
VITE_FRONTEND_FORGE_API_KEY=your_frontend_key
VITE_FRONTEND_FORGE_API_URL=https://api.manus.im

# Analytics (Optional)
VITE_ANALYTICS_ENDPOINT=https://analytics.example.com
VITE_ANALYTICS_WEBSITE_ID=your_website_id
```

### 4. Setup Database

```bash
# Generate migrations from schema
pnpm drizzle-kit generate

# Apply migrations
pnpm drizzle-kit migrate

# Or manually run migrations
mysql -u user -p database_name < drizzle/0001_brown_echo.sql
```

### 5. Run Development Server

```bash
pnpm dev
```

The application will be available at `http://localhost:3000`

### 6. Build for Production

```bash
pnpm build
pnpm start
```

## Git Workflow

### First Time Setup

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Full-stack expense tracker"

# Add remote repository
git remote add origin <your-repo-url>

# Push to GitHub/GitLab
git push -u origin main
```

### Regular Development

```bash
# Create feature branch
git checkout -b feature/your-feature

# Make changes and commit
git add .
git commit -m "Add: your feature description"

# Push to remote
git push origin feature/your-feature

# Create Pull Request on GitHub/GitLab
```

## Project Structure for Git

```
expense-tracker/
├── .git/                    # Git repository
├── .gitignore              # Git ignore rules
├── client/                 # React frontend
│   ├── src/
│   │   ├── pages/         # Page components
│   │   ├── components/    # Reusable components
│   │   ├── lib/           # Utilities
│   │   └── App.tsx        # Main app
│   ├── public/            # Static files
│   └── index.html         # HTML template
├── server/                # Node.js backend
│   ├── routers.ts         # tRPC routes
│   ├── db.ts              # Database helpers
│   └── _core/             # Framework code
├── drizzle/               # Database schema
│   ├── schema.ts          # Table definitions
│   └── migrations/        # SQL migrations
├── package.json           # Dependencies
├── tsconfig.json          # TypeScript config
├── vite.config.ts         # Vite config
├── README.md              # Documentation
├── PROJECT_SUMMARY.md     # Project overview
└── GIT_SETUP_GUIDE.md     # This file
```

## Important Files to Keep in Git

✅ **Commit These:**
- `client/src/**` - All source code
- `server/**` - All backend code
- `drizzle/**` - Database schema and migrations
- `package.json` - Dependencies list
- `tsconfig.json` - TypeScript configuration
- `vite.config.ts` - Build configuration
- `.env.example` - Environment template (without secrets)
- `README.md` - Documentation
- `.gitignore` - Git rules

❌ **Do NOT Commit:**
- `node_modules/` - Installed dependencies
- `dist/` - Build output
- `.env` - Sensitive credentials
- `.env.local` - Local environment
- `*.log` - Log files
- `.DS_Store` - macOS files
- `.idea/` - IDE files

## Deployment Checklist

### Before Deploying

- [ ] All tests passing: `pnpm test`
- [ ] No TypeScript errors: `pnpm check`
- [ ] Code formatted: `pnpm format`
- [ ] Environment variables configured
- [ ] Database migrations applied
- [ ] All features tested locally

### Deployment Steps

1. **Build the project**
   ```bash
   pnpm build
   ```

2. **Set production environment variables**
   ```bash
   export NODE_ENV=production
   export DATABASE_URL=<production-db-url>
   # ... other env vars
   ```

3. **Run migrations on production database**
   ```bash
   pnpm drizzle-kit migrate
   ```

4. **Start the server**
   ```bash
   pnpm start
   ```

## Hosting Options

### Option 1: Manus Platform
- Built-in hosting with custom domains
- Automatic SSL certificates
- Database included
- One-click deployment

### Option 2: Railway
```bash
# Install Railway CLI
npm i -g @railway/cli

# Login
railway login

# Link project
railway link

# Deploy
railway up
```

### Option 3: Render
```bash
# Push to GitHub
git push origin main

# Connect Render to GitHub repository
# Select expense-tracker project
# Configure environment variables
# Deploy
```

### Option 4: Vercel (Frontend Only)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

## Environment Variables for Production

```env
# Production Database (TiDB or MySQL)
DATABASE_URL=mysql://user:password@host:3306/expense_tracker

# OAuth Configuration
VITE_APP_ID=production_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://portal.manus.im

# Security
JWT_SECRET=<strong-random-secret>
NODE_ENV=production

# API Keys
BUILT_IN_FORGE_API_KEY=<production-key>
VITE_FRONTEND_FORGE_API_KEY=<production-frontend-key>

# Owner Information
OWNER_OPEN_ID=your_open_id
OWNER_NAME=Your Name
```

## Troubleshooting

### Database Connection Issues
```bash
# Test connection
mysql -h host -u user -p -e "SELECT 1"

# Check migrations
pnpm drizzle-kit studio
```

### Build Errors
```bash
# Clear cache
rm -rf node_modules pnpm-lock.yaml
pnpm install

# Rebuild
pnpm build
```

### TypeScript Errors
```bash
# Check types
pnpm check

# Fix formatting
pnpm format
```

## Continuous Integration (GitHub Actions)

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: pnpm/action-setup@v2
      - uses: actions/setup-node@v3
        with:
          node-version: '20'
          cache: 'pnpm'
      
      - run: pnpm install
      - run: pnpm check
      - run: pnpm test
      - run: pnpm build
      
      # Deploy to your platform
```

## Monitoring & Logs

### Development Logs
```bash
# View dev server logs
pnpm dev

# View database logs
pnpm drizzle-kit studio
```

### Production Logs
- Check platform-specific logging (Railway, Render, etc.)
- Monitor error tracking (Sentry, etc.)
- Review database query logs

## Support & Resources

- **Documentation**: See `README.md`
- **Project Overview**: See `PROJECT_SUMMARY.md`
- **GitHub Issues**: Report bugs and request features
- **Discussions**: Ask questions and share ideas

## Version Control Best Practices

1. **Commit Messages**: Use clear, descriptive messages
   ```
   ✅ Good: "Add budget spending aggregation"
   ❌ Bad: "fix stuff"
   ```

2. **Branch Naming**: Use descriptive branch names
   ```
   ✅ Good: feature/budget-alerts, fix/export-csv
   ❌ Bad: test, temp, update
   ```

3. **Pull Requests**: Include description and testing notes
4. **Code Review**: Have team members review before merge
5. **Semantic Versioning**: Tag releases (v1.0.0, v1.1.0, etc.)

## Next Steps

1. Push to GitHub/GitLab
2. Setup CI/CD pipeline
3. Configure production environment
4. Deploy to hosting platform
5. Monitor and iterate

---

**Ready to deploy!** 🚀
