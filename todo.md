# Expense Tracker TODO

## Documentation & Setup
- [ ] Write professional GitHub README with architecture, features, and setup instructions
- [ ] Create environment variables documentation

## Database Schema & Migrations
- [ ] Design and implement users, expenses, budgets, categories, and attachments tables
- [ ] Generate and apply Drizzle migrations
- [ ] Add database indexes for frequently queried fields

## Backend - tRPC Procedures
- [ ] Implement expense CRUD procedures (create, read, list, update, delete)
- [ ] Implement budget CRUD procedures (create, read, list, update, delete)
- [ ] Implement category CRUD procedures (create, read, list, update, delete)
- [ ] Implement dashboard analytics procedure (total expenses, monthly budget, savings rate, top category)
- [ ] Implement expense filtering and search procedure
- [ ] Implement expense export procedure (CSV and JSON)
- [ ] Add unit tests for all backend procedures

## Frontend - Layout & Navigation
- [ ] Create responsive DashboardLayout with sidebar navigation
- [ ] Implement navigation for five pages: Dashboard, Expenses, Budgets, Categories, Reports
- [ ] Add user profile and logout functionality

## Frontend - Dashboard Page
- [x] Create summary cards (total expenses, monthly budget, savings rate, top category)
- [x] Implement monthly spending trend chart (Recharts line chart)
- [x] Implement category distribution chart (Recharts pie/donut chart)
- [x] Add date range filter for dashboard

## Frontend - Expenses Page
- [x] Create expense list table with columns: date, category, amount, description, actions
- [x] Implement add expense modal with form validation
- [ ] Implement edit expense modal
- [x] Implement delete expense confirmation
- [ ] Add expense filtering by date range, category, amount range
- [x] Add expense search by keyword
- [ ] Add expense sorting (date, amount, category)
- [ ] Implement receipt attachment upload and display

## Frontend - Budgets Page
- [x] Create budget list with progress bars
- [x] Implement add budget modal
- [ ] Implement edit budget modal
- [x] Implement delete budget confirmation
- [x] Add over-budget alerts and visual indicators
- [ ] Display budget vs actual spending comparison

## Frontend - Categories Page
- [x] Create category list with color-coded labels and icons
- [x] Implement add custom category modal
- [ ] Implement edit category modal
- [x] Implement delete category confirmation
- [x] Display predefined categories
- [ ] Show category usage statistics

## Frontend - Reports Page
- [x] Create monthly summary report
- [x] Implement CSV export functionality
- [x] Implement JSON export functionality
- [x] Add date range selector for reports
- [x] Display spending trends and insights
- [x] Create category-wise breakdown report

## Frontend - Data Visualization
- [ ] Implement Recharts line chart for monthly trends
- [ ] Implement Recharts bar chart for category comparison
- [ ] Implement Recharts pie chart for category distribution
- [ ] Implement Recharts donut chart variant
- [ ] Add chart tooltips and legends
- [ ] Add responsive chart sizing

## Frontend - Forms & Validation
- [ ] Create reusable form components with React Hook Form
- [ ] Implement input validation for all forms
- [ ] Add error messages and success notifications

## Testing & Quality Assurance
- [x] Write unit tests for backend procedures
- [ ] Fix mock database functions in tests
- [ ] Test all CRUD operations with proper mocks
- [ ] Test filtering and search functionality
- [ ] Test export functionality
- [ ] Verify responsive design on mobile and tablet
- [ ] Test authentication flow and per-user data isolation
- [ ] Implement budget spending aggregation
- [ ] Auto-seed predefined categories on first category access

## Deployment & Final Steps
- [ ] Create final checkpoint
- [ ] Verify all features work end-to-end
- [ ] Document any known limitations
