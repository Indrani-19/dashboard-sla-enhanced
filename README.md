# Project: Dashboard SLA
This document provides an overview of the enhancements and refactoring changes made to the Dashboard SLA application. The application is designed to display product information in a table format, with features like status-based filtering, search functionality, and pagination for an improved user experience.

## Enhancements and Refactoring:
a. Code Refactoring:

- Vue 3 Upgrade: The entire application has been migrated from Vue 2 to Vue 3, taking advantage of the Composition API for better organization and reusability of logic.
- Single Responsibility Components: Components have been broken down into smaller, more manageable pieces, each with a single responsibility. This improves readability and makes the codebase easier to maintain.
- Script Setup Syntax: The new <script setup> syntax of Vue 3 is used to simplify component composition and make the code cleaner.
- Improvement in Prop Handling: More explicit prop type validation has been implemented, ensuring components receive the correct data type.

b. Pagination Implementation:

- Pagination Logic: Added comprehensive pagination logic to handle large datasets, displaying 100 rows per page.
- User-Friendly Pagination UI: Developed a user-friendly pagination interface at the bottom of the product table, allowing users to navigate between pages.

c. Color Coding:

- Dynamic Styling: Implemented dynamic class binding to color code rows in the ProductTable.vue component based on the "Status" column, enhancing data interpretability at a glance.
- Scoped Styles: Utilized scoped CSS to ensure styles apply only to the component they are defined in, preventing unintended side effects across the application.

d. Search Bar Implementation:

- Global Filtering: Introduced a search bar that enables users to filter table rows across all columns, based on the search criteria entered.

### Completed Tasks:
Code Refactoring and Upgrade:
- Transitioned the project to Vue 3 with improved Composition API usage.
- Organized components into single functionality modules for better clarity.
  Pagination:
- Implemented functional pagination to handle large sets of data, with a user-friendly UI component to navigate between pages.
  Color Coding:
- Table rows are now color-coded based on the "Status" value, improving the visual interpretation of data status.
  Search Functionality (Bonus Task):
- Added a search bar to filter rows dynamically based on user input, enhancing the application's usability.

Components
- App.vue: The main Vue component that holds the entire application.
- StatusBar.vue: A component to display status filters.
- StatusCheckbox.vue: Checkbox component for toggling product statuses.
- ProductTable.vue: Component that renders the product data in a tabular format.
- Pagination.vue: A reusable pagination component.
- ProductRow.vue: A row component for the ProductTable, representing a single product.

Additional Features
Status Filtering: 
Toggle visibility of products based on their status.
The user can get more clear display of same status column data at different place.
Live Search: 
Instantly filter out products that don't match the search term.
The search bar is on the top of the page.
So, mention the status name which you want to search, we can able to see only those rows

  Pagination: 
Navigate through product data in chunks, improving performance on large datasets.
Click on the next page button to see the next data for each status selected.

##### Prerequisites
Before running this project, make sure you have the following installed:

Node.js (Preferably the latest LTS version)
npm (Comes with Node.js)

##### Installing
To get the development environment running, follow these steps:

- Clone the repository to your local machine.

        git clone https://github.com/Indrani-19/dashboard-sla-enhanced.git

        cd dashboard-sla-enhanced

- Install the project dependencies using npm.

        npm install



- Start the development server.

        npm run dev

- After running the development server, the app should be available at:

Local: http://localhost:8080/
Network: Your IP address on the port 8080 (e.g., http://192.168.0.106:8080/)


- Project Structure

Here's an overview of the project's top-level structure:

dashboard-sla-enhanced/
|-- src/
|   |-- assets/
|   |   `-- data.json
|   |-- components/
|   |   |-- Pagination.vue
|   |   |-- ProductRow.vue
|   |   |-- ProductTable.vue
|   |   |-- StatusBar.vue
|   |   `-- StatusCheckbox.vue
|   `-- App.vue
`-- public/
    `-- index.html
