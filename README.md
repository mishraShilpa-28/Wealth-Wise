# AI-Powered Finance Platform

[project-logo](/public/logo.png)

A modern, AI-powered personal finance management platform built with Next.js, Supabase, Clerk, Prisma, and various other tools. This application allows users to manage their accounts, track transactions, set budgets, and gain financial insights through AI-driven features like receipt scanning and personalized recommendations. The platform also supports recurring transactions, monthly reports, and email notifications for budget alerts.

## Table of Contents

- [Features](#features)
- [Technologies](#technologies)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Deployment](#deployment)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Features

- **User Authentication**: Secure sign-in and sign-up with Clerk, including Google SSO support.
- **Account Management**: Create, update, and delete financial accounts with customizable names, types, and balances.
- **Transaction Tracking**: Log manual transactions or scan receipts using Gemini AI for automatic data extraction.
- **Budget Management**: Set monthly budgets and receive email alerts when nearing or exceeding limits.
- **Recurring Transactions**: Automate recurring transactions (e.g., subscriptions, bills) with customizable intervals.
- **Financial Insights**: AI-driven recommendations for saving and spending based on user transaction history.
- **Monthly Reports**: Automatically generate and email monthly financial reports summarizing income, expenses, and savings.
- **Dashboard**: Visualize financial data with charts (powered by Recharts) and view recent transactions.
- **Email Notifications**: Send budget alerts and monthly reports via Resend.
- **Security**: Protect routes and APIs with Arcjet's bot detection and rate limiting.
- **Background Jobs**: Handle recurring transactions, budget checks, and report generation with Inngest.
- **Responsive Design**: Built with Tailwind CSS and Shadcn/UI for a modern, mobile-friendly interface.
- **Onboarding Flow**: Guided setup for new users to create their first account and transaction.

## Technologies

- **Frontend**: Next.js 15.1.2 (with Turbopack), React 19, Tailwind CSS, Shadcn/UI, Lucide React, Recharts
- **Backend**: Next.js API Routes, Prisma (ORM), Supabase (PostgreSQL)
- **Authentication**: Clerk
- **AI**: Gemini API for receipt scanning and financial insights
- **Email**: Resend for sending budget alerts and reports
- **Security**: Arcjet for bot protection and rate limiting
- **Background Jobs**: Inngest for cron jobs and event-driven tasks
- **Database**: Supabase (PostgreSQL) with Prisma ORM
- **Development Tools**: ESLint, npm, Vercel (for deployment)

## Prerequisites

Before setting up the project, ensure you have the following installed:

- **Node.js**: Version 18 or later
- **npm**: Comes with Node.js (or use yarn if preferred)
- **Git**: For cloning the repository
- **Supabase Account**: For PostgreSQL database
- **Clerk Account**: For authentication
- **Gemini API Key**: For AI features
- **Resend Account**: For email notifications
- **Arcjet Account**: For security features
- **Inngest Account**: For background jobs
- A code editor like Visual Studio Code

## Setup Instructions

Follow these steps to set up the project locally:

### 1. Clone the Repository

```bash
git clone https://github.com/mishraShilpa-28/Wealth-Wise.git
cd Wealth-Wise
```

### 2. Install Dependencies

```bash
npm install
```

Install additional dependencies with legacy peer dependencies for React 19 compatibility:

```bash
npm install @clerk/nextjs @prisma/client prisma @arcjet/next inngest resend recharts lucide-react --legacy-peer-deps
```

Initialize Shadcn/UI components:

```bash
npx shadcn@latest init --legacy-peer-deps
```

Select: New York style, enable neutral CSS variables, and use legacy peer deps.

Add required components:

```bash
npx shadcn@latest add button badge calendar card checkbox drawer dropdown-menu input popover progress select switch table tooltip --legacy-peer-deps
```

### 3. Configure Environment Variables

Create a `.env` file in the project root and add the following variables (replace with your own keys):

```bash
# Supabase setup
DATABASE_URL=your-databse-url
DIRECT_URL=your-direct-databse-url

# Clerk setup
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your-clerk-publishable-key
CLERK_SECRET_KEY=your-clerk-secret-key
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/onboarding
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/onboarding

# Gemini AI setup
GEMINI_API_KEY=your-gemini-api-key

# Resend setup
RESEND_API_KEY=your-resend-api-key

# Arcjet setup
ARCJET_KEY=your-arcjet-key
```

### 4. Set Up Prisma and Database

Initialize Prisma:

```bash
npx prisma init
```

Update `prisma/schema.prisma` with the provided schema (see `prisma/schema.prisma` in the repository).

Apply the schema to the Supabase database:

```bash
npx prisma generate
npx prisma db push
```

### 5. Run Inngest Development Server

Install the Inngest CLI:

```bash
npm install -g inngest-cli
```

Start the Inngest dev server:

```bash
inngest-cli dev
```

### 6. Run the Development Server

Start the Next.js development server:

```bash
npm run dev
```

Open `http://localhost:3000` in your browser.

## Usage

1. **Homepage**: Visit `http://localhost:3000` to see the landing page with a hero section, stats, and call-to-action.
2. **Sign In/Sign Up**: Use Clerk to sign in or sign up (supports Google SSO). New users are redirected to `/onboarding`.
3. **Onboarding**: Follow the guided flow to set up your first account and transaction.
4. **Dashboard**: View accounts, transactions, budgets, and charts. Add transactions manually or via receipt scanning.
5. **Budgets**: Set monthly budgets and receive email alerts for overspending.
6. **Recurring Transactions**: Configure recurring transactions (e.g., daily, weekly) via the dashboard.
7. **Monthly Reports**: Receive automated email reports on the first day of each month.
8. **Inngest Dashboard**: Monitor background jobs at `http://localhost:8288`.

## Deployment

To deploy the project to Vercel:

1. Push the repository to GitHub:

   ```bash
   git add .
   git commit -m "Prepare for deployment"
   git push origin main
   ```

2. Import the repository into Vercel:
   - Create a new project in Vercel and link your GitHub repository.
   - Add all `.env` variables in the Vercel dashboard (`Settings > Environment Variables`).
   - Set the build command to include legacy peer dependencies:

     ```bash
     npm install --legacy-peer-deps
     ```

3. Integrate Inngest:
   - Follow Inngest’s Vercel integration guide to connect your app and sync functions.
4. Disable deployment protection (if needed):
   - In Vercel project settings, disable deployment protection to allow Inngest and other bots.

## Project Structure

```
ai-finance-platform/
├── app/                    # Next.js app router (pages, API routes)
├── components/             # React components (Shadcn/UI, custom)
├── lib/                    # Utilities (Prisma client, email templates)
├── prisma/                 # Prisma schema and migrations
├── public/                 # Static assets (logo.png, banner.jpeg)
├── inngest/                # Inngest functions (background jobs)
├── middleware.js           # Clerk and Arcjet middleware
├── .env                    # Environment variables
├── package.json            # Project dependencies
├── tailwind.config.js      # Tailwind CSS configuration
├── next.config.mjs         # Next.js configuration
```

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes and commit (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

Please ensure your code follows the project’s coding style and includes tests where applicable.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---
