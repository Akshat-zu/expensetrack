# Smart Expense Management System

A production-grade, full-stack personal expense tracker built with modern web technologies. Track spending, manage budgets, visualize financial trends, and gain actionable insights into your finances with an intuitive, responsive interface.

## 🎯 Overview

The Smart Expense Management System is designed to help users take control of their personal finances through intelligent tracking, categorization, and visualization. Whether you're budgeting for a project, monitoring daily expenses, or analyzing spending patterns, this application provides the tools and insights you need to make informed financial decisions.

**Key Capabilities:**
- Real-time expense tracking with rich categorization
- Interactive dashboards with spending trends and category breakdowns
- Budget management with progress tracking and alerts
- Advanced filtering, searching, and sorting
- Data export in CSV and JSON formats
- Secure authentication with per-user data isolation
- Responsive design for desktop, tablet, and mobile devices

## 🏗️ Technology Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | React 19 + Vite | Component-based UI with optimized bundling |
| **Styling** | Tailwind CSS 4 | Utility-first CSS framework |
| **Backend** | Node.js + Express 4 | RESTful API server |
| **API** | tRPC 11 | End-to-end type-safe API layer |
| **Database** | MySQL (TiDB) | Relational data storage |
| **ORM** | Drizzle 0.44 | Type-safe database queries |
| **Authentication** | Manus OAuth | Secure user authentication |
| **Data Visualization** | Recharts 2.15 | Interactive charts and graphs |
| **UI Components** | shadcn/ui | Accessible, composable components |
| **Form Handling** | React Hook Form + Zod | Type-safe form validation |
| **State Management** | TanStack Query | Server state management |
| **Testing** | Vitest 2.1 | Unit and integration tests |

## 📋 Features

### Dashboard Overview
- **Summary Cards**: Display total expenses, monthly budget, savings rate, and top spending category
- **Spending Trends**: Interactive line chart showing monthly expense progression
- **Category Distribution**: Pie and donut charts visualizing spending by category
- **Quick Filters**: Date range selector for focused analysis

### Expense Management
- **Full CRUD Operations**: Add, view, edit, and delete expenses
- **Rich Data Entry**: Track amount, category, date, description, and receipt attachments
- **Advanced Filtering**: Filter by date range, category, amount range, and keywords
- **Sorting Options**: Sort by date, amount, or category
- **Receipt Storage**: Upload and attach receipts to expenses for documentation

### Budget Management
- **Monthly Budgets**: Set overall monthly spending limits
- **Category Budgets**: Define budget caps for specific categories
- **Progress Tracking**: Visual progress bars showing budget utilization
- **Over-Budget Alerts**: Automatic warnings when spending exceeds budget limits
- **Budget vs Actual**: Compare planned vs actual spending

### Category Management
- **Predefined Categories**: Common expense categories included by default
- **Custom Categories**: Create custom categories tailored to your needs
- **Color Coding**: Visual labels with custom colors for quick identification
- **Category Icons**: Intuitive icons for visual scanning
- **Usage Statistics**: View spending trends by category

### Reports & Analytics
- **Monthly Reports**: Comprehensive spending summaries
- **Category Breakdown**: Detailed analysis of spending by category
- **Trend Analysis**: Identify spending patterns and anomalies
- **Data Export**: Export expense records in CSV or JSON format for external analysis

### Security & Access Control
- **Manus OAuth Authentication**: Secure, passwordless login
- **Per-User Data Isolation**: Strict data boundaries ensure user privacy
- **Protected Routes**: Automatic redirection for unauthenticated users
- **Session Management**: Secure session handling with JWT tokens

## 🚀 Getting Started

### Prerequisites
- Node.js 22.13.0 or higher
- pnpm 10.4.1 or higher
- MySQL-compatible database (TiDB, MySQL 8.0+)

### Installation

1. **Clone the repository** (or use the provided project directory)
   ```bash
   cd expense-tracker
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Set up environment variables**
   Create a `.env.local` file with the following variables:
   ```
   DATABASE_URL=mysql://user:password@host:port/database
   JWT_SECRET=your-secret-key-here
   VITE_APP_ID=your-manus-app-id
   OAUTH_SERVER_URL=https://api.manus.im
   VITE_OAUTH_PORTAL_URL=https://manus.im/login
   ```

4. **Run database migrations**
   ```bash
   pnpm drizzle-kit generate
   pnpm drizzle-kit migrate
   ```

5. **Start the development server**
   ```bash
   pnpm dev
   ```

   The application will be available at `http://localhost:3000`

### Build for Production

```bash
pnpm build
pnpm start
```

## 📁 Project Structure

```
expense-tracker/
├── client/                          # Frontend React application
│   ├── src/
│   │   ├── pages/                   # Page components (Dashboard, Expenses, Budgets, etc.)
│   │   ├── components/              # Reusable UI components
│   │   ├── contexts/                # React contexts (auth, theme)
│   │   ├── hooks/                   # Custom React hooks
│   │   ├── lib/
│   │   │   └── trpc.ts              # tRPC client configuration
│   │   ├── App.tsx                  # Main app component and routing
│   │   ├── main.tsx                 # React entry point
│   │   └── index.css                # Global styles
│   └── public/                      # Static assets (favicon, robots.txt)
├── server/                          # Backend Node.js/Express server
│   ├── routers.ts                   # tRPC procedure definitions
│   ├── db.ts                        # Database query helpers
│   ├── auth.logout.test.ts          # Example unit test
│   └── _core/                       # Framework-level infrastructure
├── drizzle/                         # Database schema and migrations
│   └── schema.ts                    # Table definitions
├── shared/                          # Shared types and constants
├── storage/                         # S3 file storage helpers
├── package.json                     # Project dependencies
└── tsconfig.json                    # TypeScript configuration
```

## 🔄 Development Workflow

### Adding a New Feature

1. **Update Database Schema** (if needed)
   - Edit `drizzle/schema.ts` to add or modify tables
   - Run `pnpm drizzle-kit generate` to create migration SQL
   - Apply migration via the management UI or `webdev_execute_sql`

2. **Create Backend Procedures**
   - Add query helpers in `server/db.ts`
   - Define tRPC procedures in `server/routers.ts`
   - Write unit tests in `server/*.test.ts`

3. **Build Frontend Components**
   - Create page or component files in `client/src/pages/` or `client/src/components/`
   - Use tRPC hooks (`trpc.*.useQuery`, `trpc.*.useMutation`) for data fetching
   - Style with Tailwind CSS and shadcn/ui components

4. **Test & Verify**
   - Run `pnpm test` to execute unit tests
   - Test in browser and verify functionality
   - Check responsive design on multiple devices

### Running Tests

```bash
# Run all tests
pnpm test

# Run tests in watch mode
pnpm test --watch

# Run specific test file
pnpm test server/auth.logout.test.ts
```

### Type Checking

```bash
# Check TypeScript types without emitting
pnpm check
```

### Code Formatting

```bash
# Format code with Prettier
pnpm format
```

## 🔐 Authentication Flow

The application uses Manus OAuth for secure, passwordless authentication:

1. User clicks "Sign In" and is redirected to the Manus login portal
2. After successful authentication, Manus redirects to `/api/oauth/callback`
3. Backend validates the OAuth token and creates a session cookie
4. Frontend receives user context and grants access to protected routes
5. User can logout, which clears the session cookie and redirects to login

All API calls are automatically authenticated via the session cookie. Protected procedures use `protectedProcedure` to ensure only authenticated users can access them.

## 📊 Data Visualization

The application uses **Recharts** for all data visualization components:

- **Line Charts**: Display spending trends over time
- **Bar Charts**: Compare spending across categories or time periods
- **Pie Charts**: Show category distribution as percentages
- **Donut Charts**: Similar to pie charts with a center cutout for aesthetic appeal

All charts are responsive, include tooltips for detailed information, and support custom color schemes.

## 💾 Data Export

Users can export their expense data in two formats:

- **CSV**: Comma-separated values for use in spreadsheet applications
- **JSON**: Structured JSON format for programmatic analysis

Exports can be filtered by date range and category for targeted data extraction.

## 💹 Currency

The application uses **Indian Rupees (₹)** for all financial calculations and displays. All amounts are displayed in Indian Rupees throughout the dashboard, expense lists, budgets, and reports.

## 🎨 Design Principles

The application follows modern UI/UX design principles:

- **Clean, Professional Aesthetic**: Minimalist design with clear visual hierarchy
- **Responsive Layout**: Adapts seamlessly to desktop, tablet, and mobile screens
- **Accessibility**: WCAG 2.1 AA compliant with keyboard navigation and screen reader support
- **Consistent Branding**: Unified color palette, typography, and component styling
- **Intuitive Navigation**: Sidebar navigation with clear section labels and icons

## 🔧 Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | MySQL connection string | `mysql://user:pass@localhost/db` |
| `JWT_SECRET` | Secret for JWT token signing | `your-secret-key` |
| `VITE_APP_ID` | Manus OAuth application ID | `app-id-here` |
| `OAUTH_SERVER_URL` | Manus OAuth server URL | `https://api.manus.im` |
| `VITE_OAUTH_PORTAL_URL` | Manus login portal URL | `https://manus.im/login` |
| `OWNER_OPEN_ID` | Project owner's OpenID | `owner-id` |
| `OWNER_NAME` | Project owner's name | `Owner Name` |

### Database Connection

The application uses MySQL-compatible databases (MySQL 8.0+, TiDB, etc.). Ensure your database connection string is properly formatted and the database is accessible from your server.

## 🧪 Testing

The project includes example unit tests using Vitest. Tests are located alongside source files with `.test.ts` extensions.

**Example test file**: `server/auth.logout.test.ts`

To add tests for new features:
1. Create a `.test.ts` file in the same directory as the code being tested
2. Import test utilities from `vitest`
3. Write test cases using `describe()` and `it()` blocks
4. Run tests with `pnpm test`

## 📦 Deployment

### Frontend Deployment
The frontend can be deployed to any static hosting service:
- Vercel, Netlify, GitHub Pages, AWS S3 + CloudFront, etc.
- Build command: `pnpm build`
- Output directory: `dist/`

### Backend Deployment
The backend can be deployed to:
- Render, Railway, Heroku, AWS EC2, DigitalOcean, etc.
- Build command: `pnpm build`
- Start command: `pnpm start`
- Port: Configured via environment variables

### Database
Use a managed database service:
- MongoDB Atlas, AWS RDS, Google Cloud SQL, TiDB Cloud, etc.
- Ensure proper backups and security configurations

## 🐛 Troubleshooting

### Database Connection Issues
- Verify `DATABASE_URL` is correct and accessible
- Check firewall rules allow connections from your server
- Ensure database user has proper permissions

### OAuth Authentication Fails
- Verify `VITE_APP_ID` and `OAUTH_SERVER_URL` are correct
- Check that redirect URLs are properly configured in Manus dashboard
- Ensure cookies are enabled in browser

### Charts Not Displaying
- Verify Recharts is properly installed (`pnpm install`)
- Check browser console for JavaScript errors
- Ensure data is being fetched correctly from backend

### Slow Performance
- Check database query performance with indexes
- Verify API response times
- Optimize frontend bundle size with code splitting
- Consider caching strategies for frequently accessed data

## 📝 License

This project is licensed under the MIT License. See LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

For issues, questions, or feature requests, please open an issue on GitHub or contact the development team.

---

**Built with ❤️ by the Manus team**

Last updated: April 2026
