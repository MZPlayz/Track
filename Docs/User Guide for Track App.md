# User Guide for Track App


## 1. Introduction

Welcome to **Track**, your personal Money Tracker Web App! This comprehensive user guide is designed to help you navigate and effectively utilize all the features of Track, empowering you to take full control of your financial journey. Whether you are looking to meticulously track your expenses, set ambitious savings goals, manage your budget, or gain insightful reports into your spending habits, Track provides an intuitive and powerful platform to achieve your financial aspirations.

Track is built with a mobile-first, minimalist design philosophy, ensuring a clean, uncluttered, and highly functional user experience. The dark theme with rose highlights and white text is designed for optimal readability and a sophisticated aesthetic, allowing you to focus on what matters most: your money. This guide will walk you through every aspect of the application, from initial setup to advanced features, ensuring you can maximize its potential.

We believe that managing your finances should be straightforward and motivating. This guide will provide step-by-step instructions, tips, and best practices to help you save, grow, and strengthen your finances with confidence. Let's begin your journey to financial empowerment!



## 2. Getting Started with Track

Starting your financial journey with Track is quick and easy. This section guides you through the initial setup, including account registration and linking your financial institutions.

### 2.1. Account Registration and Login

1.  **Accessing Track:** Open your web browser and navigate to the Track PWA URL. For a seamless experience, you can install Track as a Progressive Web App on your mobile device for quick access.
2.  **Sign Up:** If you are a new user, click on the **"Sign Up"** button on the welcome screen. You will be prompted to enter your email address and create a secure password. Ensure your password meets the strength requirements displayed.
3.  **Agree to Terms:** Read and accept the Terms of Service and Privacy Policy. This is a crucial step to ensure you understand how your data is handled.
4.  **Register:** Click **"Register"** to create your account.
5.  **Log In:** If you already have an account, click **"Log In"** and enter your registered email and password.

### 2.2. Initial Profile Setup

Upon successful registration or your first login, Track will guide you through a brief setup process to personalize your experience:

1.  **Financial Goals:** Select your primary financial goals (e.g., saving for a house, paying off debt, building an emergency fund). You can choose multiple goals and prioritize them. This helps Track tailor insights and recommendations for you.
2.  **Currency Selection:** Choose your preferred currency (e.g., USD, GBP, BDT). All financial data within the app will be displayed in this currency.
3.  **Account Linking Prompt:** You will be asked if you wish to link your bank accounts. Linking accounts allows Track to automatically import your transactions, saving you time and ensuring accuracy.

### 2.3. Linking Your Financial Accounts

Linking your bank accounts is the most efficient way to track your finances. Track uses secure third-party aggregators (like Plaid) to connect to your financial institutions.

1.  **Initiate Linking:** From the onboarding flow or the **"Accounts"** section, click **"Link New Account"**.
2.  **Select Institution:** Search for and select your bank or financial institution from the provided list.
3.  **Secure Login:** You will be securely redirected to the aggregator's interface where you will enter your online banking credentials. **Track does not store your bank login information.** This process is encrypted and handled directly by the secure aggregator.
4.  **Select Accounts:** Choose which specific accounts (checking, savings, credit cards, investments) you want to link to Track.
5.  **Authorize:** Grant permission for the aggregator to access your transaction and balance data. This permission is read-only and does not allow Track to move money.
6.  **Synchronization:** Once authorized, Track will begin synchronizing your historical transactions and current balances. This may take a few moments.

**What if I don't want to link accounts?**

No problem! You can choose to **"Skip for Later"** during onboarding. You can always link accounts later, or you can manually add all your transactions. Track is flexible to suit your preferences.

Once your accounts are linked and initial setup is complete, you will be taken to your personalized dashboard, ready to explore your financial world.



## 3. Understanding Your Dashboard

The dashboard is your central hub in Track, providing a quick, at-a-glance overview of your financial health. Designed with a minimalist aesthetic, it highlights key metrics and provides quick access to essential actions. The dark theme ensures clarity and focus on your financial data.

### 3.1. Key Financial Metrics

At the top of your dashboard, you will find summary cards displaying your most important financial figures:

*   **Total Balance:** This represents the sum of all balances across your linked and manually added accounts. It gives you an immediate understanding of your overall financial position.
*   **Monthly Income:** Shows your total income for the current month, including salaries, freelance payments, and any other money received.
*   **Monthly Expenses:** Displays your total spending for the current month, categorized and tracked from your transactions.
*   **Savings Rate:** This metric indicates the percentage of your income that you are saving. A higher savings rate means you are putting more money towards your financial goals.

Each of these cards may also show a small percentage change from the previous period, providing context and helping you quickly identify trends.

### 3.2. Quick Actions

Below your financial metrics, the "Quick Actions" section provides immediate access to the most frequent tasks:

*   **Add Transaction:** Use this button to manually record any income or expense that isn't automatically imported from a linked account. This is essential for accurate tracking, especially for cash transactions.
*   **Add Income:** A shortcut to quickly log income transactions.
*   **Add Expense:** A shortcut to quickly log expense transactions.
*   **View Reports:** Navigates you directly to the comprehensive reports section, where you can dive deeper into your financial data.

These buttons are designed with the rose highlight color to make them easily identifiable and interactive.

### 3.3. Recent Transactions

The "Recent Transactions" list on your dashboard provides a chronological overview of your latest financial activities. This allows you to quickly review recent spending and income without navigating to the full transactions list.

Each entry typically includes:

*   **Date:** When the transaction occurred.
*   **Description:** A brief detail of the transaction (e.g., "Coffee Shop," "Salary").
*   **Category:** The assigned category for the transaction (e.g., "Food & Dining," "Income").
*   **Amount:** The value of the transaction, clearly indicating whether it was an income (green text) or an expense (white text).

### 3.4. Navigation Bar

At the bottom of your screen, the persistent navigation bar allows you to easily move between the main sections of the app:

*   **Home:** Returns you to the dashboard.
*   **Transactions:** Takes you to the detailed list of all your financial transactions, where you can view, edit, filter, and search.
*   **Reports:** Leads you to the various financial reports and insights, including spending analysis, income vs. expense, and net worth.
*   **Profile/Settings:** Access your account settings, manage linked accounts, update preferences, and find help.

The navigation bar is designed to be intuitive and always accessible, ensuring a smooth user experience across the application.

Your dashboard is designed to be your personalized financial command center, providing you with the essential information and tools you need at your fingertips. Take a moment to familiarize yourself with its layout and features.



## 4. Managing Your Transactions

Track provides robust tools to manage all your financial transactions, whether they are automatically imported or manually entered. Accurate transaction management is the foundation of effective financial tracking, budgeting, and reporting.

### 4.1. Viewing All Transactions

1.  **Access:** Tap on the **"Transactions"** icon in the bottom navigation bar. This will take you to a comprehensive list of all your financial transactions.
2.  **Transaction List:** The list displays transactions in chronological order, with the most recent at the top. Each entry includes the date, description, category, and amount. Income transactions are highlighted in green, while expenses are in white text against the dark background.
3.  **Search and Filter:**
    *   **Search Bar:** Use the search bar at the top of the screen to quickly find transactions by description or amount.
    *   **Filters:** Apply filters to narrow down your transactions by date range, category, account, or type (income/expense). This helps you analyze specific spending patterns or find particular entries.

### 4.2. Adding a Manual Transaction

Even with linked accounts, you may need to manually add transactions, especially for cash payments or unlinked accounts.

1.  **Initiate:** From the dashboard, tap **"Add Transaction"**, **"Add Income"**, or **"Add Expense"**. Alternatively, from the Transactions screen, look for a similar "Add" button.
2.  **Fill Details:** A minimalist form will appear. Fill in the following:
    *   **Amount:** Enter the transaction amount. Ensure you use the correct sign (positive for income, negative for expense).
    *   **Date:** Select the date of the transaction.
    *   **Description:** Provide a clear description (e.g., "Groceries at SuperMart," "Freelance Payment").
    *   **Category:** This is crucial for budgeting and reporting. Select an existing category from the dropdown list. If a suitable category doesn't exist, you can create a new one.
    *   **Account:** Choose the account from which the transaction occurred or to which it was deposited.
3.  **Save:** Tap **"Save Transaction"**. The transaction will be added to your list and reflected in your account balances and budget.

### 4.3. Editing and Deleting Transactions

To ensure accuracy, you can easily modify or remove transactions:

1.  **Select Transaction:** Tap on any transaction in the list to view its details.
2.  **Edit:** Tap the **"Edit"** button (often represented by a pencil icon). The transaction form will reappear, pre-filled with the current details. Make your changes and tap **"Save"**.
3.  **Delete:** Tap the **"Delete"** button (often represented by a trash can icon). A confirmation prompt will appear to prevent accidental deletion. Confirm to remove the transaction.

### 4.4. Categorizing and Reviewing Transactions

Track attempts to automatically categorize imported transactions. However, it's important to review and adjust them for accuracy.

1.  **Reviewing Auto-Categorized:** Newly imported transactions might have a small indicator if they were auto-categorized. Tap on them to review the assigned category.
2.  **Re-categorize:** If the category is incorrect, tap **"Edit"** and select the appropriate category. Track learns from your changes, improving future auto-categorization.
3.  **Creating Custom Categories:** If you need a more specific category, you can usually create one during the transaction editing process or in the app's settings. This allows for highly personalized financial tracking.

Effective transaction management is the backbone of your financial insights. By diligently categorizing and reviewing your transactions, you provide Track with the accurate data it needs to help you make informed financial decisions.



## 5. Budgeting and Goal Setting

Track empowers you to take control of your money through effective budgeting and motivating financial goal setting. These features help you allocate your funds wisely and work towards your financial aspirations.

### 5.1. Creating and Managing Budgets

Budgeting helps you understand where your money goes and ensures you stay within your spending limits.

1.  **Access Budgets:** Tap on the **"Budgets"** section (usually accessible from the bottom navigation bar or a dedicated icon).
2.  **Budget Overview:** You will see a list of your active budgets, typically organized by month or category. Each budget displays the budgeted amount, the amount spent, and the remaining balance.
3.  **Create a New Budget:**
    *   Tap **"Create New Budget"**.
    *   **Category:** Select the spending category you want to budget for (e.g., "Groceries," "Entertainment," "Transportation").
    *   **Amount:** Enter the maximum amount you plan to spend in this category for the budget period.
    *   **Period:** Choose the budget period (e.g., monthly, weekly, custom).
    *   **Save:** Tap **"Save Budget"**.
4.  **Monitoring Progress:** As you record transactions, your budget progress bars will update in real-time. The minimalist progress bar (rose highlight for progress, light grey for track) provides a clear visual indicator.
    *   **Green:** You are well within your budget.
    *   **Orange:** You are approaching your budget limit (e.g., 80% spent).
    *   **Red:** You have exceeded your budget.
5.  **Drill Down:** Tap on any budget category to see a detailed list of all transactions contributing to that budget.
6.  **Edit/Delete Budget:** Tap on a budget to edit its amount or period, or to delete it.

### 5.2. Setting and Tracking Financial Goals

Goals help you save for future aspirations or pay off debt systematically.

1.  **Access Goals:** Tap on the **"Goals"** section (usually accessible from the bottom navigation bar or a dedicated icon).
2.  **Goals Overview:** You will see a list of your financial goals, each with its target amount, current amount saved/paid, and a visual progress indicator.
3.  **Create a New Goal:**
    *   Tap **"Create New Goal"**.
    *   **Goal Type:** Select the type of goal (e.g., "Save for Down Payment," "Pay Off Credit Card," "Emergency Fund").
    *   **Target Amount:** Enter the total amount you need to save or pay off.
    *   **Target Date (Optional):** Set a date by which you want to achieve the goal. Track can help you calculate how much you need to contribute regularly.
    *   **Save:** Tap **"Save Goal"**.
4.  **Contributing to Goals:**
    *   **Manual Contribution:** Tap on a goal and select **"Add Contribution"**. Enter the amount you are contributing and the account it came from.
    *   **Automated Contributions (Future Feature):** In future updates, Track may allow you to set up recurring, automated transfers to your goals from linked accounts.
5.  **Monitoring Progress:** The minimalist progress bar (rose highlight) for each goal visually updates as you contribute. Celebrate milestones as you get closer to your target!
6.  **Goal Reminders:** Track can send you reminders to contribute to your goals, helping you stay on track.

By actively using the budgeting and goal-setting features, you can gain immense clarity and control over your financial future, turning your aspirations into achievable milestones.



## 6. Reports and Insights

Track provides powerful reporting and insights tools to help you understand your financial behavior, identify trends, and make informed decisions. These reports are presented with a minimalist design, ensuring clarity and focus on the data.

### 6.1. Accessing Reports

1.  **Access:** Tap on the **"Reports"** icon in the bottom navigation bar or click **"View Reports"** from the dashboard.
2.  **Reports Dashboard:** You will see an overview of available reports, including Spending Analysis, Income vs. Expense, and Net Worth.

### 6.2. Spending Analysis

This report helps you understand where your money is going.

1.  **Select "Spending Analysis":** Choose this option from the reports dashboard.
2.  **Category Breakdown:** A clean pie chart or bar chart will display your spending broken down by category for the selected period. The rose highlight color may indicate your largest spending category or a selected segment.
3.  **Time Period:** Use the options at the top to select the time period you wish to analyze (e.g., "This Month," "Last Month," "Last Quarter," or a custom date range).
4.  **Drill Down:** Tap on any category segment in the chart to view a detailed list of all transactions within that category for the selected period.
5.  **Trend Analysis:** A line graph will show your spending trends over time, allowing you to spot patterns and make adjustments.

### 6.3. Income vs. Expense Report

Understand your cash flow and identify if you are spending more than you earn.

1.  **Select "Income vs. Expense":** Choose this option from the reports dashboard.
2.  **Trend Graph:** A minimalist line graph will display your income (green line) and expenses (white or light grey line) over time. The net cash flow may be highlighted in rose.
3.  **Net Cash Flow:** A clear numerical display of your net cash flow for the selected period.
4.  **Comparative Analysis:** You can compare different periods to see how your income and expenses have changed.

### 6.4. Net Worth Report

Track your overall financial growth by monitoring your net worth.

1.  **Select "Net Worth":** Choose this option from the reports dashboard.
2.  **Net Worth Trend:** A line graph will show your net worth over time, calculated from your linked accounts and any manually entered assets or liabilities. The trend line may be highlighted in rose.
3.  **Asset/Liability Breakdown:** A summary will show your total assets and total liabilities, giving you a clear picture of your financial standing.

### 6.5. Personalized Insights

Track provides proactive, personalized financial insights and tips based on your data. These insights appear in various sections of the app and are designed to be actionable and motivating. They often use a rose-colored accent to draw your attention.

*   **Examples:** "You spent X% more on dining out this month. Consider setting a budget for this category.", "You're on track to reach your savings goal 3 months early!"

By regularly reviewing your reports and insights, you can gain a deeper understanding of your financial habits and make informed decisions to improve your financial health.



## 7. Conclusion

Congratulations! You have now explored the core functionalities of **Track**, your personal Money Tracker Web App. By utilizing its intuitive features for transaction management, budgeting, goal setting, and insightful reporting, you are well-equipped to take charge of your financial future.

Remember, consistent use is key to maximizing the benefits of Track. Regularly log your transactions, monitor your budgets, track your goals, and review your reports to gain a clear understanding of your financial habits. The minimalist design and dark theme are crafted to make this process as seamless and enjoyable as possible.

We are continuously working to enhance Track with new features and improvements. Should you have any questions, feedback, or require assistance, please refer to the in-app help section or contact our support team. Thank you for choosing Track to help you save, grow, and strengthen your finances!


