# SpendSave: Personal Finance Tracker

SpendSave – a personal finance tracker web app for students to log income and expenses, set monthly category budgets, track savings goals, and view spending on a dashboard. Built with React, Node.js/Express and PostgreSQL. CPAN 359 Agile team project.

### System Overview
SpendSave is a personal finance tracker designed for post-secondary students and young adults who would like to get a better grip on managing money on their own for the first time. Between tuition, rent, transit, groceries, and questionable splurging purchases, all paid for with part-time jobs and OSAP payments that only come a few times a year, it is easy to lose track of where the money goes. Banking apps show your transactions, but they don't help you plan for a semester or notice that you spent $180 altogether on food delivery last month. Our app is designed to host an easy place to keep track of spending habits and expenses to develop better financial habits and awareness, setting up for a brighter future.

A new user signs up with an email and password, then sets up their categories and their first monthly budget. After that, every transaction they add is saved to their account and updates the dashboard, budgets and goals right away. Budgets reset at the start of each month, but past transactions are still saved so users can look back at earlier months. All the calculations, like remaining budget and goal progress, are done on the server so the numbers are the same on every device.

### Intended Users
A typical user would open the app a few times a week, quickly adding an expense right after buying something or at the end of the day. Custom tags for different categories of transactions helps visualize the types of purchases being made, and becomes helpful later for evaluating budgeting choices. Once a month, users can set or change their preferred budget for each category, totalling to an overall budget designed off their recorded income. Savings goals can also be implemented and monitored from leftover income. Before making a bigger purchase, users can easily check how much budget remains in each spending category, how close they are to a savings goal, or make the purchase and account for the overspending in the next month. SpendSave runs in a web browser, so users can access the app from any location, on a laptop or a phone, without needing to install anything.

### Main Features

1. **Secure User Authentication & Cross-Device Sync**  
   Users create a personal account and log in securely, keeping all financial records private and isolated to their profile. Because account data is stored centrally in the cloud, users can log in and manage their finances seamlessly from a laptop, tablet, or smartphone.

2. **Income & Expense Tracking**  
   Users can log both incoming funds and daily expenditures in seconds. Each transaction entry captures:
   * **Amount & Type:** Whether the entry is income or an expense.
   * **Date:** When the transaction occurred.
   * **Category:** Customizable or preset tags (such as Food, Transportation, Entertainment, Tuition, or Income).
   * **Optional Note:** Custom context (e.g., *"Groceries at No Frills"* or *"Part-time shift payout"*).  
   To keep records accurate, users can edit details or delete entries at any time if they make a typo or log a duplicate transaction.

3. **Category-Based Monthly Budgeting & Smart Alerts**  
   Users can set monthly spending limits for individual categories like food, transportation, and entertainment. The application tracks spending against each limit in real time, displaying clear progress bars showing how much of each budget has been spent versus how much remains. When spending in any category crosses 80% of its monthly limit, the app triggers an early warning alert so users can adjust their habits before overspending.

4. **Savings Goals Tracker**  
   Users can define specific financial targets—such as saving $600 for a new laptop by April—by setting a target amount and a deadline. The app calculates the required savings pace and displays visual progress indicators, making it easy for users to see how close they are to their target and whether they are on track to hit their deadline.

5. **Interactive Financial Dashboard**  
   The home dashboard gives users an immediate, at-a-glance snapshot of their financial health for the current month. It brings together three core views:
   * **Current Monthly Balance:** Total monthly income minus total monthly expenses.
   * **Spending by Category Chart:** A visual breakdown showing exactly where money is going.
   * **Recent Transactions Feed:** A quick-access list of the latest logged entries.

6. **Transaction Filtering & CSV Export**  
   As transaction history grows, users can filter their ledger by date range or category to review specific spending periods or audit individual habits. Whenever users need to analyze their numbers in external spreadsheet software or keep offline backups, they can export their filtered or complete transaction history as a clean CSV file with a single click.

### System Components
We plan to split SpendSave into four main parts. Each part has a clear job, which makes the system easier to build, test and divide among team members during sprints.

1. **Front end (user interface)**  
   The front end will be a React web app that runs in the user's browser. It includes all the pages users interact with: sign-up and login, the dashboard, the transaction list, budget settings and savings goals. It also shows forms for adding income and expenses, and charts that show spending by category. The front end does not store or calculate any financial data itself. It sends requests to the back end through the API and displays the results. We chose React because it splits the interface into reusable components (like a transaction form or a budget progress bar), so different team members can build different pages at the same time. The layout will be responsive, so the app works on both laptops and phones.

2. **Back end (API)**  
   The back end will be a Node.js and Express server that provides a REST API for the front end. It handles all requests for accounts, transactions, categories, budgets and savings goals, such as adding an expense, editing a budget or loading the dashboard. All the business rules live here, including calculating the remaining budget, sending the 80 percent budget warning, tracking goal progress and resetting budgets at the start of each month. Keeping these rules on the server means they only need to be written and tested in one place, and users see the same numbers on every device. The back end also checks all incoming data (for example, that an amount is a valid number) before saving it.

3. **Authentication**  
   Authentication covers sign-up, login and logout. Passwords will be hashed before they are stored, so they are never saved as plain text. After logging in, the user receives a token that is sent with each request, so the back end knows who they are and only returns their own data. We are treating authentication as its own part because every other feature depends on it. Users can't add transactions or set budgets without an account, so we plan to build it in the first sprint.

4. **Database**  
   We will use a PostgreSQL database with tables for users, categories, transactions, budgets and savings goals. Our data is closely connected: each transaction belongs to one user and one category, and each budget is linked to a category and a month. A relational database handles these relationships well and keeps the data consistent. It also makes common calculations, like monthly spending totals per category, simple and fast with SQL queries. Past transactions are kept even after budgets reset, so users can review earlier months.
