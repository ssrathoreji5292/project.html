<!DOCTYPE html>
<html>
<head>
    <title>Login Page</title>
    <style>
        
    body {
        font-family: Arial, sans-serif;
        background-color: #f2f2f2;
        margin: 0;
        padding: 0;
    }

    h1 {
        text-align: center;
    }

    h2 {
        margin-top: 20px;
    }

    form {
        background-color: #ffffff;
        padding: 20px;
        margin: 20px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }

    form input[type="text"],
    form input[type="password"],
    form input[type="all"] {
        width: 100%;
        padding: 10px;
        margin: 5px 0;
        border: 1px solid #ccc;
        border-radius: 3px;
    }

    button[type="submit"] {
        background-color: #4CAF50;
        color: #fff;
        padding: 10px 15px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    button[type="submit"]:hover {
        background-color: #45a049;
    }

    #customerList,
    div.customerInfo {
        background-color: #ffffff;
        padding: 20px;
        margin: 20px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }

    hr {
        border: 0;
        border-top: 1px solid #ddd;
        margin: 10px 0;
    }
</style>

        }
    </style>
</head>
<body>
    <h1>Login</h1>
    <form id="loginForm">
        Email: <input type="text" id="login_id" required>
        Password: <input type="password" id="password" required>
        <button type="submit">Login</button>
    </form>
    <div id="token"></div>

    <script>
        document.getElementById('loginForm').addEventListener('submit', function (e) {
            e.preventDefault();
            const login_id = document.getElementById('login_id').value;
            const password = document.getElementById('password').value;
            fetch("https://qa2.sunbasedata.com/sunbase/portal/api/assignment_auth.jsp", {
                method: 'POST',
                body: JSON.stringify({ login_id, password }),
                headers: { 'Content-Type': 'application/json' }
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('token').innerHTML = `Bearer Token: ${data.token}`;
            })
            .catch(error => {
                console.error('Authentication failed', error);
            });
        });
    </script>
    
        <h1>Customer List</h1>
        <div id="customerList"></div>
    
        <script>
            const token = 'YOUR_BEARER_TOKEN'; // Replace with the token received after login
            fetch("https://qa2.sunbasedata.com/sunbase/portal/api/assignment.jsp?cmd=get_customer_list", {
                method: 'GET',
                headers: { 'Authorization': `Bearer ${token}` }
            })
            .then(response => response.json())
            .then(data => {
                const customerList = document.getElementById('customerList');
                customerList.innerHTML = '<h2>Customers</h2>';
                data.forEach(customer => {
                    const customerInfo = document.createElement('div');
                    customerInfo.innerHTML = `<p>Name: ${customer.first_name} ${customer.last_name}</p><hr>`;
                    customerList.appendChild(customerInfo);
                });
            })
            .catch(error => {
                console.error('Failed to fetch customer list', error);
            });
        </script>

    <h1>Customer Management</h1>

    <h2>Customer Details</h2>
    <form id="createCustomerForm">
        First Name: <input type="text" id="first_name" required>
        Last Name: <input type="text" id="last_name" required>
        Street: <input type="text" id="Street" required>
        <h3>Address</h3>
        City: <input type="text" id="city" required>
        State: <input type="text" id="State" required>
        Email: <input type="all" id="email" required>
        Phone: <input type="All" id="phone" required>
        <button type="submit">Submit</button>
    </form>

    <h2>Update Customer</h2>
    <form id="updateCustomerForm">
        UUID: <input type="text" id="uuid" required>
        First Name: <input type="text" id="update_first_name">
        Last Name: <input type="text" id="update_last_name">
        Street: <input type="text" id="Street" required>
        <h3>Address </h3>
         City: <input type="text" id="city" required>
        State: <input type="text" id="State" required>First Name: <input type="text" id="first_name" required>
        Email: <input type="all" id="email" required>
        Phone: <input type="All" id="phone" required>
        <button type="submit">Update</button>
    </form>

    <h2>Delete Customer</h2>
    <form id="deleteCustomerForm">
        UUID: <input type="text" id="delete_uuid" required>
        <button type="submit">Delete</button>
    </form>

    <script>
        const token = 'YOUR_BEARER_TOKEN'; // Replace with the token received after login
        // Implement the logic for creating, updating, and deleting customers here
    </script>
</body>
</html>
