# ShulaTech_Solution_Expense_Tracker_Kumar
expense tracker using html css javascript




<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Expense Tracker App</title>
</head>
<style>body {
    font-family: Arial, sans-serif;
    margin: 0;
  }
  
  h1, h2 {
    text-align: center;
  }
  
  .input-section {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
  }
  
  .input-section label {
    font-weight: bold;
    margin-right: 10px;
  }
  
  .input-section input[type="number"], .input-section input[type="date"] {
    padding: 5px;
    margin-right: 10px;
  }
  
  .input-section button {
    padding: 5px 10px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .expenses-list {
    margin: 20px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  th {
    background-color: #4CAF50;
    color: white;
  }
  
  tfoot td {
    font-weight: bold;
  }
  
  .delete-btn {
    padding: 5px 10px;
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
</style>

<body>
    <h1>Expense Tracker App</h1>
    <div class="input-section">
        <label for="category-select">Category:</label>
        <select id="category-select">
            <option value="Food & Beverage">Food & Beverage</option>
            <option value="Rent">Rent</option>
            <option value="Transport">Transport</option>
            <option value="Relaxing">Relaxing</option>
        </select>
        <label for="amount-input">Amount:</label>
        <input type="number" id="amount-input">
        <label for="date-input">Date:</label>
        <input type="date" id="date-input">
        <button id="add-btn">Add</button>
    </div>
    <div class="expenses-list">
        <h2>Expenses List</h2>
        <table>
            <thead>
                <tr>
                    <th>Category</th>
                    <th>Amount</th>
                    <th>Date</th>
                    <th>Delete</th>
                </tr>
            </thead>
            <tbody id="expnese-table-body">

            </tbody>
            <tfoot>
                <tr>
                    <td>Total:</td>
                    <td id="total-amount"></td>
                    <td></td>
                    <td></td>
                </tr>
            </tfoot>
        </table>
    </div>
    <script src="script.js"></script>
</body>


</html>

<script>let expenses = [];
    let totalAmount = 0;
    
    const categorySelect = document.getElementById('category-select');
    const amountInput = document.getElementById('amount-input');
    const dateInput = document.getElementById('date-input');
    const addBtn = document.getElementById('add-btn');
    const expensesTableBody = document.getElementById('expnese-table-body');
    const totalAmountCell = document.getElementById('total-amount');
    
    addBtn.addEventListener('click', function() {
        const category = categorySelect.value;
        const amount = Number(amountInput.value);
        const date = dateInput.value;
    
        if (category === '') {
            alert('Please select a category');
            return;
        }
        if (isNaN(amount) || amount <=0 ) {
            alert('Please enter a valid amoun')
            return;
        }
        if(date === '') {
            alert('Please select a date')
            return;
        }
        expenses.push({category, amount, date});
    
        totalAmount += amount;
        totalAmountCell.textContent = totalAmount;
    
        const newRow = expensesTableBody.insertRow();
    
        const categoryCell = newRow.insertCell();
        const amountCell = newRow.insertCell();
        const dateCell = newRow.insertCell();
        const deleteCell = newRow.insertCell();
        const deleteBtn = document.createElement('button');
    
        deleteBtn.textContent = 'Delete';
        deleteBtn.classList.add('delete-btn');
        deleteBtn.addEventListener('click', function() {
            expenses.splice(expenses.indexOf(expense), 1);
    
            totalAmount -= expense.amount;
            totalAmountCell.textContent = totalAmount;
    
            expensesTableBody.removeChild(newRow);
        });
    
        const expense = expenses[expenses.length - 1];
        categoryCell.textContent = expense.category;
        amountCell.textContent = expense.amount;
        dateCell.textContent = expense.date;
        deleteCell.appendChild(deleteBtn);
    
    });
    
    for (const expense of expenses) {
        totalAmount += expense.amount;
        totalAmountCell.textContent = totalAmount;
    
        const newRow = expensesTableBody.inserRow();
        const categoryCell = newRow.insertCell();
        const amountCell = newRow.insertCell();
        const dateCell = newRow.insertCell();
        const deleteCell = newRow.insertCell();
        const deleteBtn = document.createElement('button');
        deleteBtn.textContent = 'Delete';
        deleteBtn.classList.add('delete-btn');
        deleteBtn.addEventListener('click', function() {
            expenses.splice(expenses.indexOf(expense), 1);
    
            totalAmount -= expense.amount;
            totalAmountCell.textContent = totalAmount;
    
            expensesTableBody.removeChild(newRow);
        });
        categoryCell.textContent = expense.category;
        amountCell.textContent = expense.amount;
        dateCell.textContent = expense.date;
        deleteCell.appendChild(deleteBtn);
    }</script>
