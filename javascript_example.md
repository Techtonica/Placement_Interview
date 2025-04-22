### JavaScript Comprehension Questions (15 minutes)

#### Example 1: JavaScript Fundamentals
**Variable Declarations**:
- Explain the differences between `var`, `let`, and `const` in JavaScript.
- How does variable hoisting work with each of these declarations?

**Data Types and Equality**:
- What's the difference between `==` and `===` in JavaScript?
- Provide examples where they would produce different results.
- Explain the concept of truthy and falsy values in JavaScript.

**Functions and Scope**:
- What is a closure in JavaScript? Provide a simple example.
- How does the `this` keyword behave differently in arrow functions compared to regular functions?


#### Example 2: JavaScript Concepts

**Asynchronous JavaScript**:
- Explain the difference between synchronous and asynchronous code execution.
- Compare and contrast callbacks, promises, and async/await.
- How would you handle errors in async/await code?

**DOM Manipulation**:
- Explain the difference between `innerHTML`, `textContent`, and `innerText`.
- What are event bubbling and event capturing? How can you stop event propagation?
- What is event delegation and why is it useful?

**Arrays and Objects**:
- Explain the difference between `map()`, `filter()`, and `reduce()` array methods.
- What are the different ways to clone an object in JavaScript?
- How would you check if a property exists in an object?


### JavaScript Code Challenge (40 minutes)

#### Example 1: Interactive Quiz Application

**Problem Description:**
Create an interactive quiz application that presents multiple-choice questions to users, tracks their score, and provides feedback on their answers.

**Requirements:**

1. Display questions one at a time with multiple-choice options
2. Allow users to select an answer and provide immediate feedback
3. Track and display the user's score
4. Show a summary of results at the end
5. Include a timer for each question
6. Allow users to restart the quiz


**Starter Code (HTML):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .quiz-container {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .question {
            font-size: 18px;
            margin-bottom: 15px;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .option {
            padding: 10px;
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 4px;
            cursor: pointer;
        }
        
        .option:hover {
            background-color: #f0f0f0;
        }
        
        .option.selected {
            background-color: #d4edda;
            border-color: #c3e6cb;
        }
        
        .option.correct {
            background-color: #d4edda;
            border-color: #c3e6cb;
        }
        
        .option.incorrect {
            background-color: #f8d7da;
            border-color: #f5c6cb;
        }
        
        .feedback {
            margin-top: 10px;
            padding: 10px;
            border-radius: 4px;
            display: none;
        }
        
        .feedback.correct {
            background-color: #d4edda;
            color: #155724;
        }
        
        .feedback.incorrect {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        button {
            padding: 10px 15px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        
        button:hover {
            background-color: #0069d9;
        }
        
        button:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        
        .timer {
            font-size: 16px;
            text-align: right;
            margin-bottom: 10px;
        }
        
        .score {
            font-size: 16px;
            margin-bottom: 10px;
        }
        
        .summary {
            margin-top: 20px;
            padding: 15px;
            background-color: #e9ecef;
            border-radius: 4px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div class="score">Score: <span id="score">0</span>/<span id="total">0</span></div>
        <div class="timer">Time: <span id="time">30</span> seconds</div>
        
        <div id="question-container">
            <div class="question" id="question"></div>
            <div class="options" id="options"></div>
            <div class="feedback" id="feedback"></div>
        </div>
        
        <div class="summary" id="summary"></div>
        
        <div class="controls">
            <button id="prev-btn" disabled>Previous</button>
            <button id="next-btn" disabled>Next</button>
            <button id="restart-btn" style="display: none;">Restart Quiz</button>
        </div>
    </div>
    
    <script src="quiz.js"></script>
</body>
</html>
```

```javascript
/**
 * Interactive Quiz Application
 * 
 * This application presents multiple-choice questions to users, tracks their score,
 * and provides feedback on their answers.
 * 
 * Functions to implement:
 * 1. initializeQuiz - Set up the quiz with questions and initial state
 * 2. displayQuestion - Display the current question and options
 * 3. selectOption - Handle user selection of an answer option
 * 4. checkAnswer - Check if the selected answer is correct
 * 5. showFeedback - Display feedback for the user's answer
 * 6. nextQuestion - Move to the next question
 * 7. previousQuestion - Move to the previous question
 * 8. startTimer - Start the timer for the current question
 * 9. showSummary - Display a summary of the quiz results
 * 10. restartQuiz - Reset the quiz to its initial state
 */

// Quiz questions
const quizQuestions = [
    {
        question: "What is JavaScript primarily used for?",
        options: [
            "Server-side scripting",
            "Client-side web development",
            "Database management",
            "Machine learning"
        ],
        correctAnswer: 1
    },
    {
        question: "Which of the following is NOT a JavaScript data type?",
        options: [
            "String",
            "Boolean",
            "Float",
            "Object"
        ],
        correctAnswer: 2
    },
    {
        question: "What does DOM stand for?",
        options: [
            "Document Object Model",
            "Data Object Model",
            "Document Oriented Model",
            "Digital Ordinance Model"
        ],
        correctAnswer: 0
    },
    {
        question: "Which method is used to add an element at the end of an array?",
        options: [
            "push()",
            "append()",
            "addToEnd()",
            "concat()"
        ],
        correctAnswer: 0
    },
    {
        question: "What is the correct way to check if the variable 'x' is equal to 5 in value and type?",
        options: [
            "x = 5",
            "x == 5",
            "x === 5",
            "x.equals(5)"
        ],
        correctAnswer: 2
    }
];

// DOM elements
const questionContainer = document.getElementById('question-container');
const questionElement = document.getElementById('question');
const optionsElement = document.getElementById('options');
const feedbackElement = document.getElementById('feedback');
const scoreElement = document.getElementById('score');
const totalElement = document.getElementById('total');
const timeElement = document.getElementById('time');
const summaryElement = document.getElementById('summary');
const prevButton = document.getElementById('prev-btn');
const nextButton = document.getElementById('next-btn');
const restartButton = document.getElementById('restart-btn');

// Quiz state
let currentQuestionIndex = 0;
let score = 0;
let userAnswers = [];
let timer;
let timeLeft;

/**
 * Initialize the quiz.
 */
function initializeQuiz() {
    // TODO: Implement this function
    // 1. Set up initial quiz state
    // 2. Display the first question
    // 3. Update the total questions count
    // 4. Start the timer
}

/**
 * Display the current question and options.
 */
function displayQuestion() {
    // TODO: Implement this function
    // 1. Get the current question
    // 2. Update the question text
    // 3. Clear previous options
    // 4. Create and display new options
    // 5. Update button states
}

/**
 * Handle user selection of an answer option.
 * 
 * @param {number} optionIndex - Index of the selected option
 */
function selectOption(optionIndex) {
    // TODO: Implement this function
    // 1. Store the user's answer
    // 2. Update the UI to show the selected option
    // 3. Check if the answer is correct
    // 4. Show feedback
    // 5. Enable the next button
}

/**
 * Check if the selected answer is correct.
 * 
 * @param {number} selectedIndex - Index of the selected option
 * @param {number} correctIndex - Index of the correct option
 * @returns {boolean} - Whether the answer is correct
 */
function checkAnswer(selectedIndex, correctIndex) {
    // TODO: Implement this function
    // 1. Compare the selected index with the correct index
    // 2. Update the score if correct
    // 3. Return whether the answer is correct
}

/**
 * Show feedback for the user's answer.
 * 
 * @param {boolean} isCorrect - Whether the answer is correct
 */
function showFeedback(isCorrect) {
    // TODO: Implement this function
    // 1. Display appropriate feedback message
    // 2. Apply correct styling
    // 3. Clear the timer
}

/**
 * Move to the next question.
 */
function nextQuestion() {
    // TODO: Implement this function
    // 1. Increment the question index
    // 2. Check if we've reached the end of the quiz
    // 3. If not, display the next question and start the timer
    // 4. If yes, show the summary
}

/**
 * Move to the previous question.
 */
function previousQuestion() {
    // TODO: Implement this function
    // 1. Decrement the question index
    // 2. Display the previous question
    // 3. Update button states
}

/**
 * Start the timer for the current question.
 */
function startTimer() {
    // TODO: Implement this function
    // 1. Set the initial time (e.g., 30 seconds)
    // 2. Update the timer display
    // 3. Start the countdown
    // 4. When time runs out, automatically select an answer or move to the next question
}

/**
 * Display a summary of the quiz results.
 */
function showSummary() {
    // TODO: Implement this function
    // 1. Hide the question container
    // 2. Show the summary element
    // 3. Calculate the final score
    // 4. Display the results and correct answers
    // 5. Show the restart button
}

/**
 * Reset the quiz to its initial state.
 */
function restartQuiz() {
    // TODO: Implement this function
    // 1. Reset all quiz state variables
    // 2. Hide the summary
    // 3. Show the question container
    // 4. Start the quiz again
}

// Event listeners
nextButton.addEventListener('click', nextQuestion);
prevButton.addEventListener('click', previousQuestion);
restartButton.addEventListener('click', restartQuiz);

// Initialize the quiz when the page loads
document.addEventListener('DOMContentLoaded', initializeQuiz);
```

#### Example 2: Budget Tracker

**Problem Description:**
Create a budget tracking application that allows users to add income and expenses, categorize transactions, and view their financial summary.

**Requirements:**

1. Add income and expense transactions with amounts, dates, and categories
2. Display a list of all transactions
3. Calculate and display the current balance
4. Filter transactions by type (income/expense) and category
5. Show a summary of income and expenses by category
6. Save transactions to local storage


**Starter Code (HTML):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Budget Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .balance-container {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        
        .balance {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .summary {
            display: flex;
            justify-content: space-around;
        }
        
        .income-summary, .expense-summary {
            padding: 10px;
            border-radius: 4px;
            flex: 1;
            margin: 0 5px;
        }
        
        .income-summary {
            background-color: #d4edda;
            color: #155724;
        }
        
        .expense-summary {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .form-container {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        
        button {
            padding: 10px 15px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        
        button:hover {
            background-color: #0069d9;
        }
        
        .transactions-container {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        
        .filters {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .transaction-list {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        
        .transaction-item {
            padding: 10px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-item.income {
            border-left: 4px solid #28a745;
        }
        
        .transaction-item.expense {
            border-left: 4px solid #dc3545;
        }
        
        .transaction-amount {
            font-weight: bold;
        }
        
        .transaction-amount.income {
            color: #28a745;
        }
        
        .transaction-amount.expense {
            color: #dc3545;
        }
        
        .transaction-details {
            display: flex;
            flex-direction: column;
        }
        
        .transaction-category {
            font-size: 12px;
            color: #6c757d;
        }
        
        .transaction-date {
            font-size: 12px;
            color: #6c757d;
        }
        
        .delete-btn {
            background-color: transparent;
            color: #dc3545;
            border: none;
            cursor: pointer;
            font-size: 16px;
            padding: 0 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Budget Tracker</h1>
        
        <div class="balance-container">
            <div class="balance">Current Balance: $<span id="balance">0.00</span></div>
            <div class="summary">
                <div class="income-summary">
                    <div>Income</div>
                    <div>$<span id="total-income">0.00</span></div>
                </div>
                <div class="expense-summary">
                    <div>Expenses</div>
                    <div>$<span id="total-expenses">0.00</span></div>
                </div>
            </div>
        </div>
        
        <div class="form-container">
            <h2>Add Transaction</h2>
            <form id="transaction-form">
                <div class="form-group">
                    <label for="transaction-type">Type</label>
                    <select id="transaction-type" required>
                        <option value="income">Income</option>
                        <option value="expense">Expense</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="transaction-category">Category</label>
                    <select id="transaction-category" required>
                        <option value="">Select a category</option>
                        <!-- Categories will be populated by JavaScript -->
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="transaction-amount">Amount</label>
                    <input type="number" id="transaction-amount" min="0.01" step="0.01" required placeholder="0.00">
                </div>
                
                <div class="form-group">
                    <label for="transaction-date">Date</label>
                    <input type="date" id="transaction-date" required>
                </div>
                
                <div class="form-group">
                    <label for="transaction-description">Description</label>
                    <input type="text" id="transaction-description" placeholder="Optional description">
                </div>
                
                <button type="submit">Add Transaction</button>
            </form>
        </div>
        
        <div class="transactions-container">
            <h2>Transactions</h2>
            
            <div class="filters">
                <select id="filter-type">
                    <option value="all">All Types</option>
                    <option value="income">Income</option>
                    <option value="expense">Expense</option>
                </select>
                
                <select id="filter-category">
                    <option value="all">All Categories</option>
                    <!-- Categories will be populated by JavaScript -->
                </select>
            </div>
            
            <ul class="transaction-list" id="transaction-list">
                <!-- Transactions will be populated by JavaScript -->
            </ul>
        </div>
    </div>
    
    <script src="budget.js"></script>
</body>
</html>
```

**Starter Code (JavaScript):**
```javascript
/**
 * Budget Tracker Application
 * 
 * This application allows users to track their income and expenses,
 * categorize transactions, and view their financial summary.
 * 
 * Functions to implement:
 * 1. initializeApp - Set up the application with initial state and event listeners
 * 2. addTransaction - Add a new transaction to the tracker
 * 3. deleteTransaction - Remove a transaction
 * 4. updateBalance - Update the balance and summary displays
 * 5. displayTransactions - Display the list of transactions with filters
 * 6. populateCategories - Populate category dropdowns based on transaction type
 * 7. saveTransactions - Save transactions to local storage
 * 8. loadTransactions - Load transactions from local storage
 */

// Categories for income and expenses
const categories = {
    income: [
        "Salary",
        "Freelance",
        "Investments",
        "Gifts",
        "Other Income"
    ],
    expense: [
        "Housing",
        "Food",
        "Transportation",
        "Utilities",
        "Entertainment",
        "Healthcare",
        "Shopping",
        "Education",
        "Personal Care",
        "Other Expenses"
    ]
};

// DOM elements
const balanceElement = document.getElementById('balance');
const totalIncomeElement = document.getElementById('total-income');
const totalExpensesElement = document.getElementById('total-expenses');
const transactionForm = document.getElementById('transaction-form');
const transactionTypeSelect = document.getElementById('transaction-type');
const transactionCategorySelect = document.getElementById('transaction-category');
const transactionAmountInput = document.getElementById('transaction-amount');
const transactionDateInput = document.getElementById('transaction-date');
const transactionDescriptionInput = document.getElementById('transaction-description');
const filterTypeSelect = document.getElementById('filter-type');
const filterCategorySelect = document.getElementById('filter-category');
const transactionList = document.getElementById('transaction-list');

// Application state
let transactions = [];

/**
 * Initialize the application.
 */
function initializeApp() {
    // TODO: Implement this function
    // 1. Set the default date to today
    // 2. Populate category dropdowns
    // 3. Load transactions from local storage
    // 4. Display transactions
    // 5. Update balance
    // 6. Add event listeners
}

/**
 * Add a new transaction.
 * 
 * @param {Event} event - Form submission event
 */
function addTransaction(event) {
    // TODO: Implement this function
    // 1. Prevent form submission
    // 2. Get form values
    // 3. Create a new transaction object
    // 4. Add the transaction to the transactions array
    // 5. Save transactions to local storage
    // 6. Update the UI
    // 7. Reset the form
}

/**
 * Delete a transaction.
 * 
 * @param {string} id - ID of the transaction to delete
 */
function deleteTransaction(id) {
    // TODO: Implement this function
    // 1. Filter out the transaction with the given ID
    // 2. Save transactions to local storage
    // 3. Update the UI
}

/**
 * Update the balance and summary displays.
 */
function updateBalance() {
    // TODO: Implement this function
    // 1. Calculate total income
    // 2. Calculate total expenses
    // 3. Calculate balance
    // 4. Update the UI elements
}

/**
 * Display the list of transactions with filters.
 */
function displayTransactions() {
    // TODO: Implement this function
    // 1. Get filter values
    // 2. Filter transactions based on type and category
    // 3. Clear the transaction list
    // 4. Create and append transaction elements
}

/**
 * Populate category dropdowns based on transaction type.
 * 
 * @param {string} type - Transaction type (income or expense)
 */
function populateCategories(type) {
    // TODO: Implement this function
    // 1. Clear existing options
    // 2. Get categories for the selected type
    // 3. Create and append option elements
}

/**
 * Save transactions to local storage.
 */
function saveTransactions() {
    // TODO: Implement this function
    // 1. Convert transactions to JSON
    // 2. Save to localStorage
}

/**
 * Load transactions from local storage.
 */
function loadTransactions() {
    // TODO: Implement this function
    // 1. Get transactions from localStorage
    // 2. Parse JSON to transactions array
    // 3. Handle case when no transactions are saved
}

/**
 * Format a number as currency.
 * 
 * @param {number} amount - Amount to format
 * @returns {string} - Formatted amount
 */
function formatCurrency(amount) {
    return amount.toFixed(2);
}

/**
 * Generate a unique ID.
 * 
 * @returns {string} - Unique ID
 */
function generateID() {
    return Date.now().toString();
}

// Event listeners
transactionTypeSelect.addEventListener('change', () => {
    populateCategories(transactionTypeSelect.value);
});

transactionForm.addEventListener('submit', addTransaction);

filterTypeSelect.addEventListener('change', displayTransactions);
filterCategorySelect.addEventListener('change', displayTransactions);

// Initialize the application when the page loads
document.addEventListener('DOMContentLoaded', initializeApp);
```
