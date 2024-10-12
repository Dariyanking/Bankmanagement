# Bankmanagement
HTML:-<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Management System</title>
    <link rel="stylesheet" href="sty.css">
</head>
<body>
    <header>
        <h1>Bank Management System</h1>
    </header>

    <!-- Login Section -->
    <section id="loginSection" class="section">
        <h2>Login</h2>
        <form id="loginForm">
            <label for="username">Username:</label>
            <input type="text" id="username" placeholder="Enter your username" required>

            <label for="password">Password:</label>
            <input type="password" id="password" placeholder="Enter your password" required>

            <label for="role">Role:</label>
            <select id="role" required>
                <option value="customer">Customer</option>
                <option value="admin">Admin</option>
            </select>

            <button type="submit">Login</button>
        </form>
        <button onclick="showNewAccountForm()">Create New Account</button>
    </section>

    <!-- New Account Section -->
    <section id="newAccountSection" class="section" style="display: none;">
        <h2>Create New Account</h2>
        <form id="newAccountForm">
            <label for="newName">Full Name:</label>
            <input type="text" id="newName" placeholder="Enter your full name" required>

            <label for="newAccountType">Account Type:</label>
            <select id="newAccountType" required>
                <option value="savings">Savings</option>
                <option value="checking">Checking</option>
            </select>

            <label for="initialDeposit">Initial Deposit:</label>
            <input type="number" id="initialDeposit" placeholder="Enter initial deposit" required>

            <button type="submit">Create Account</button>
        </form>
        <button onclick="cancelNewAccount()">Cancel</button>
    </section>

    <!-- Customer Dashboard -->
    <section id="customerDashboard" class="section" style="display: none;">
        <h2>Customer Dashboard</h2>
        <div class="account-info">
            <p><strong>Name:</strong> John Doe</p>
            <p><strong>Account Number:</strong> 1234567890</p>
            <p><strong>Balance:</strong> $10,000</p>
            <p><strong>Account Type:</strong> Savings</p>
        </div>
        <button onclick="logout()">Logout</button>
    </section>

    <!-- Admin Dashboard -->
    <section id="adminDashboard" class="section" style="display: none;">
        <h2>Admin Dashboard</h2>
        <div id="adminCustomerList">
            <div class="customer-info">
                <p><strong>Name:</strong> John Doe</p>
                <p><strong>Account Number:</strong> 1234567890</p>
                <p><strong>Balance:</strong> $10,000</p>
                <p><strong>Account Type:</strong> Savings</p>
                <button onclick="updateAccount('1234567890')">Update</button>
                <button onclick="deleteAccount('1234567890')">Delete</button>
            </div>

            <div class="customer-info">
                <p><strong>Name:</strong> Jane Smith</p>
                <p><strong>Account Number:</strong> 9876543210</p>
                <p><strong>Balance:</strong> $8,000</p>
                <p><strong>Account Type:</strong> Checking</p>
                <button onclick="updateAccount('9876543210')">Update</button>
                <button onclick="deleteAccount('9876543210')">Delete</button>
            </div>
        </div>
        <button onclick="logout()">Logout</button>
    </section>

    <footer>
        <p>&copy; 2024 Bank Management System. All rights reserved.</p>
    </footer>

    <script src="first.js"></script>
</body>
</html>


css:-/* Global Styling */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Arial', sans-serif;
    background-color: #f0f4f8;
    color: #333;
    line-height: 1.6;
}

header {
    background-color: #0066cc;
    color: white;
    padding: 1.5rem;
    text-align: center;
    font-size: 2rem;
    font-weight: bold;
    text-transform: uppercase;
}

.section {
    padding: 2rem;
    margin: 1rem auto;
    max-width: 800px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    animation: fadeIn 0.5s ease-in-out;
}

/* Login Form Styling */
form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 400px;
    margin: auto;
}

input, select {
    padding: 0.8rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 1rem;
    transition: all 0.3s ease-in-out;
}

input:focus, select:focus {
    border-color: #0066cc;
    box-shadow: 0 0 5px rgba(0, 102, 204, 0.5);
}

button {
    padding: 0.8rem;
    background-color: #0066cc;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
    transition: background-color 0.3s ease-in-out;
}

button:hover {
    background-color: #004d99;
}

button:focus {
    outline: none;
    box-shadow: 0 0 5px rgba(0, 102, 204, 0.5);
}

/* Dashboard Information Cards */
.account-info, .customer-info {
    background-color: #f8f9fa;
    padding: 1rem;
    border-radius: 8px;
    margin-bottom: 1.5rem;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease-in-out;
}

.account-info:hover, .customer-info:hover {
    transform: translateY(-5px);
}

/* Animations */
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

/* Footer */
footer {
    text-align: center;
    padding: 1rem;
    background-color: #0066cc;
    color: white;
    margin-top: 2rem;
    font-size: 1rem;
}

/* Responsive Design */
@media (max-width: 768px) {
    .section {
        padding: 1rem;
    }
    
    form {
        width: 100%;
        padding: 1rem;
    }
}
js:-document.getElementById('loginForm').addEventListener('submit', function(event) {
    event.preventDefault();

    const username = document.getElementById('username').value;
    const password = document.getElementById('password').value;
    const role = document.getElementById('role').value;

    if (username && password) {
        if (role === 'customer') {
            showCustomerDashboard();
        } else if (role === 'admin') {
            showAdminDashboard();
        }
    } else {
        alert('Please fill in all fields.');
    }
});

// Show New Account Form
function showNewAccountForm() {
    document.getElementById('loginSection').style.display = 'none';
    document.getElementById('newAccountSection').style.display = 'block';
}

// Cancel New Account Creation
function cancelNewAccount() {
    document.getElementById('newAccountSection').style.display = 'none';
    document.getElementById('loginSection').style.display = 'block';
}

// Create New Account (simulated)
document.getElementById('newAccountForm').addEventListener('submit', function(event) {
    event.preventDefault();

    const name = document.getElementById('newName').value;
    const accountType = document.getElementById('newAccountType').value;
    const initialDeposit = document.getElementById('initialDeposit').value;

    alert(`New account created for ${name} with a deposit of $${initialDeposit}`);
    document.getElementById('newAccountForm').reset();
    cancelNewAccount();  // Go back to login
});

// Show Customer Dashboard
function showCustomerDashboard() {
    document.getElementById('loginSection').style.display = 'none';
    document.getElementById('customerDashboard').style.display = 'block';
    document.getElementById('adminDashboard').style.display = 'none';
}

// Show Admin Dashboard
function showAdminDashboard() {
    document.getElementById('loginSection').style.display = 'none';
    document.getElementById('customerDashboard').style.display = 'none';
    document.getElementById('adminDashboard').style.display = 'block';
}

// Admin Functions
function updateAccount(accountNumber) {
    alert(`Update account with account number: ${accountNumber}`);
}

function deleteAccount(accountNumber) {
    alert(`Account with account number: ${accountNumber} has been deleted.`);
}

// Logout function
function logout() {
    document.getElementById('loginSection').style.display = 'block';
    document.getElementById('customerDashboard').style.display = 'none';
    document.getElementById('adminDashboard').style.display = 'none';
    document.getElementById('newAccountSection').style.display = 'none';
    document.getElementById('loginForm').reset();
}
