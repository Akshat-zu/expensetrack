# Expense Tracker - Complete Deployment Guide

## 🚀 Quick Start for Git

### Step 1: Extract and Setup
```bash
# Extract the project
tar -xzf expense-tracker-final.tar.gz
cd expense-tracker

# Install dependencies
pnpm install

# Generate and apply database migrations
pnpm drizzle-kit generate
pnpm drizzle-kit migrate
```

### Step 2: Configure Environment
Create `.env.local`:
```env
# Database
DATABASE_URL=mysql://user:password@localhost:3306/expense_tracker

# OAuth
VITE_APP_ID=your_app_id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://portal.manus.im

# Security
JWT_SECRET=your_strong_secret_key_here

# Owner
OWNER_OPEN_ID=your_open_id
OWNER_NAME=Your Name

# APIs
BUILT_IN_FORGE_API_KEY=your_api_key
BUILT_IN_FORGE_API_URL=https://api.manus.im
VITE_FRONTEND_FORGE_API_KEY=your_frontend_key
VITE_FRONTEND_FORGE_API_URL=https://api.manus.im
```

### Step 3: Run Development
```bash
pnpm dev
# Access at http://localhost:3000
```

### Step 4: Build for Production
```bash
pnpm build
pnpm start
```

## 📦 Project Contents

### Frontend (React + Vite)
- **Dashboard**: Analytics with Recharts visualizations
- **Expenses**: Full CRUD with filtering and search
- **Budgets**: Monthly and category-level budget tracking
- **Categories**: Predefined and custom categories with colors
- **Reports**: Data export (CSV/JSON) and analytics

### Backend (Node.js + Express + tRPC)
- Type-safe API with tRPC
- Manus OAuth authentication
- Per-user data isolation
- Database query helpers with Drizzle ORM

### Database (MySQL)
- Users table with role-based access
- Categories with color coding
- Expenses with receipt support
- Budgets with alert thresholds

## 💱 Currency

**All amounts are in Indian Rupees (₹)**
- Dashboard displays ₹
- Expense lists show ₹
- Budget tracking in ₹
- Reports export in ₹

## 🔐 Security Features

✅ Manus OAuth authentication  
✅ Per-user data isolation  
✅ JWT session tokens  
✅ Protected tRPC procedures  
✅ SQL injection prevention (Drizzle ORM)  
✅ XSS protection (React)  
✅ CSRF protection (secure cookies)

## 📊 Key Features

### Dashboard
- Total expenses summary
- Monthly budget overview
- Savings rate calculation
- Top spending category
- Monthly trend chart (Recharts)
- Category distribution pie chart

### Expense Management
- Add/edit/delete expenses
- Filter by category, date, amount
- Search by keyword
- Receipt attachment support
- Expense list with sorting

### Budget Management
- Set monthly budgets
- Category-level budgets
- Progress tracking with bars
- Over-budget alerts
- Customizable alert thresholds

### Category Management
- 12 predefined categories
- Create custom categories
- Color-coded labels
- Category icons
- Usage statistics

### Reports & Analytics
- Monthly spending reports
- Category breakdown
- Spending trends
- CSV export
- JSON export

## 🔧 Development

### Run Tests
```bash
pnpm test
```

### Type Check
```bash
pnpm check
```

### Format Code
```bash
pnpm format
```

### Database Studio
```bash
pnpm drizzle-kit studio
```

## 🌐 Deployment Options

### Option 1: Manus Platform (Recommended)
- Built-in hosting
- Custom domains
- Database included
- One-click deployment

### Option 2: Railway
```bash
railway link
railway up
```

### Option 3: Render
1. Push to GitHub
2. Connect Render to repository
3. Configure environment variables
4. Deploy

### Option 4: Docker
```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY . .
RUN pnpm install
RUN pnpm build
EXPOSE 3000
CMD ["pnpm", "start"]
```

## 📋 Pre-Deployment Checklist

- [ ] All tests passing (`pnpm test`)
- [ ] No TypeScript errors (`pnpm check`)
- [ ] Code formatted (`pnpm format`)
- [ ] Environment variables configured
- [ ] Database migrations applied
- [ ] OAuth credentials set up
- [ ] Database backups configured
- [ ] HTTPS enabled
- [ ] Error logging configured
- [ ] Performance optimized

## 🚨 Troubleshooting

### Database Connection Error
```bash
# Test connection
mysql -h host -u user -p -e "SELECT 1"

# Check DATABASE_URL format
echo $DATABASE_URL
```

### OAuth Login Fails
- Verify VITE_APP_ID is correct
- Check OAUTH_SERVER_URL is accessible
- Ensure redirect URLs configured in Manus dashboard
- Clear browser cookies and try again

### Build Fails
```bash
# Clear cache and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm build
```

### Charts Not Displaying
- Check browser console for errors
- Verify data is fetching from API
- Ensure Recharts is installed
- Check network tab for API responses

## 📈 Performance Tips

1. **Database Optimization**
   - Indexes on userId, categoryId, date
   - Pagination for large datasets
   - Query optimization in db.ts

2. **Frontend Optimization**
   - Code splitting with Vite
   - Lazy loading pages
   - Image optimization
   - CSS minification

3. **Caching Strategy**
   - Browser caching for static assets
   - API response caching
   - Database query caching

## 🔄 Git Workflow

### Initialize Repository
```bash
git init
git add .
git commit -m "Initial commit: Expense tracker"
git remote add origin <your-repo-url>
git push -u origin main
```

### Feature Development
```bash
git checkout -b feature/your-feature
# Make changes
git add .
git commit -m "Add: description"
git push origin feature/your-feature
# Create Pull Request
```

### Versioning
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

## 📚 Documentation

- **README.md**: Main documentation
- **PROJECT_SUMMARY.md**: Project overview
- **GIT_SETUP_GUIDE.md**: Git setup instructions
- **DEPLOYMENT.md**: This file

## 🆘 Support

For issues or questions:
1. Check troubleshooting section
2. Review error logs
3. Check database connection
4. Verify environment variables
5. Test in development mode

## 📞 Contact

- GitHub Issues: Report bugs
- Discussions: Ask questions
- Email: support@example.com

---

**Ready to Deploy!** 🎉

Version: 1.0.0  
Last Updated: April 2026  
Status: Production Ready
