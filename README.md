# Project: SLA Dashboard Pro

**SLA Dashboard Pro** is an enhanced and refactored version of a dashboard application designed to display product information in a table format. The application includes advanced features like status-based filtering, search functionality, and pagination to provide an improved and user-friendly experience.

---

## Key Features

### Enhancements and Refactoring
- **Vue 3 Upgrade**: Migrated from Vue 2 to Vue 3, leveraging the Composition API for better code organization and reusability.
- **Single Responsibility Components**: Components have been modularized into smaller, reusable pieces, improving readability and maintainability.
- **Script Setup Syntax**: Utilized Vue 3's `<script setup>` syntax for cleaner and more concise component logic.
- **Improved Prop Handling**: Added explicit prop type validation to ensure components receive the correct data types.

### Pagination
- **Pagination Logic**: Implemented pagination to handle large datasets, displaying 100 rows per page.
- **User-Friendly Pagination UI**: Designed an intuitive pagination interface at the bottom of the table for seamless navigation.

### Color Coding
- **Dynamic Styling**: Rows are dynamically color-coded based on the "Status" column, making it easier to interpret data at a glance.
- **Scoped Styles**: Used scoped CSS to ensure styles are component-specific, avoiding unintended side effects.

### Search Functionality
- **Global Filtering**: Added a search bar to filter table rows across all columns based on user input.

---

## Completed Tasks
- **Code Refactoring and Upgrade**:
  - Transitioned to Vue 3 with Composition API.
  - Organized components into single-functionality modules.
- **Pagination**:
  - Implemented pagination for large datasets with a user-friendly UI.
- **Color Coding**:
  - Added dynamic row coloring based on the "Status" column.
- **Search Functionality (Bonus Task)**:
  - Integrated a search bar for real-time filtering of table rows.

---

## Components
- **App.vue**: The main Vue component that holds the entire application.
- **StatusBar.vue**: Displays status filters.
- **StatusCheckbox.vue**: Checkbox component for toggling product statuses.
- **ProductTable.vue**: Renders product data in a tabular format.
- **Pagination.vue**: Reusable pagination component.
- **ProductRow.vue**: Represents a single product row in the table.

---

## Additional Features
- **Status Filtering**: Toggle visibility of products based on their status.
- **Live Search**: Instantly filter products based on search terms.
- **Pagination**: Navigate through product data in chunks for better performance.

---

## Prerequisites
Before running the project, ensure you have the following installed:
- **Node.js** (preferably the latest LTS version).
- **npm** (comes with Node.js).

---

## Installation
To set up the development environment, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/Indrani-19/dashboard-sla-enhanced.git
   cd dashboard-sla-enhanced
   
**dashboard-sla-enhanced**/
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
