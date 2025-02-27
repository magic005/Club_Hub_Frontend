---
layout: page 
permalink: /login
search_exclude: true
show_reading_time: false 
---

<style>

/* Container for Login & Signup */
.login-container {
    display: flex;
    justify-content: center;
    align-items: stretch; /* Ensures same height */
    flex-wrap: wrap;
    gap: 40px;
}

/* Apply consistent styles to both login and signup cards */
.login-card, .signup-card {
    flex: 1;
    max-width: 500px;
    min-width: 400px;
    background-color: #1A1A1D;
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
    text-align: center;
    border: 3px solid transparent;
    display: flex;
    flex-direction: column;
    justify-content: space-between; /* Ensures consistent spacing */
    min-height: 420px; /* Explicit min-height to make them equal */
}

/* Titles */
.login-card h1, .signup-card h1 {
    font-size: 1.8em;
    font-weight: bold;
    background: linear-gradient(to right, #FF4B2B, #FF416C);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    margin-bottom: 20px;
}

/* Input Container: Maintains structure */
.form-group {
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex-grow: 1;
}

/* Invisible Placeholder for Spacing */
.placeholder {
    visibility: hidden; /* Keeps space occupied but not visible */
    height: 45px; /* Matches input field height */
}

/* Form Inputs */
input[type="text"], input[type="password"] {
    width: 90%;
    padding: 12px;
    border-radius: 8px;
    border: 1px solid #333;
    background: #121212;
    color: white;
    font-size: 16px;
    outline: none;
    margin-bottom: 15px;
}

/* Buttons */
button {
    width: 100%;
    padding: 12px;
    background: linear-gradient(to right, #FF4B2B, #FF416C);
    border: none;
    border-radius: 8px;
    font-size: 1.2em;
    color: white;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.3s ease, transform 0.2s ease;
}

button:hover {
    background: linear-gradient(to right, #FF416C, #FF4B2B);
    transform: translateY(-3px);
}

/* Mobile Responsive */
@media (max-width: 768px) {
    .login-container {
        flex-direction: column;
        align-items: center;
    }

    .login-card, .signup-card {
        width: 90%;
    }
}
</style>

<div class="login-container">
    <!-- Python Login Form -->
    <div class="login-card">
        <h1 id="pythonTitle">User Login (Python/Flask)</h1>
        <form id="pythonForm" onsubmit="pythonLogin(); return false;">
            <p>
                <label>
                    GitHub ID:
                    <input type="text" name="uid" id="uid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="password" id="password" required>
                </label>
            </p>
            <div class="placeholder"></div>
            <p>
                <button type="submit">Login</button>
            </p>
            <p id="message" style="color: red;"></p>
        </form>
    </div>
    <div class="signup-card">
        <h1 id="signupTitle">Sign Up</h1>
        <form id="signupForm" onsubmit="signup(); return false;">
            <p>
                <label>
                    Name:
                    <input type="text" name="name" id="name" required>
                </label>
            </p>
            <p>
                <label>
                    GitHub ID:
                    <input type="text" name="signupUid" id="signupUid" required>
                </label>
            </p>
            <p>
                <label>
                    Password:
                    <input type="password" name="signupPassword" id="signupPassword" required>
                </label>
            </p>
            <p>
                <button type="submit">Sign Up</button>
            </p>
            <p id="signupMessage" style="color: green;"></p>
        </form>
    </div>
</div>

<script type="module">
    import { login, pythonURI, fetchOptions } from '{{site.baseurl}}/assets/js/api/config.js';

    // Function to handle Python login
    window.pythonLogin = function() {
        const options = {
            URL: `${pythonURI}/api/authenticate`,
            callback: pythonDatabase,
            message: "message",
            method: "POST",
            cache: "no-cache",
            body: {
                uid: document.getElementById("uid").value,
                password: document.getElementById("password").value,
            }
        };
        login(options);
    }

    // Function to handle signup
    window.signup = function() {
    const signupButton = document.querySelector(".signup-card button");

    // Disable the button and change its color
    signupButton.disabled = true;
    signupButton.style.backgroundColor = '#d3d3d3'; // Light gray to indicate disabled state

    const signupOptions = {
        URL: `${pythonURI}/api/user`,
        method: "POST",
        cache: "no-cache",
        body: {
            name: document.getElementById("name").value,
            uid: document.getElementById("signupUid").value,
            password: document.getElementById("signupPassword").value,
        }
    };

    fetch(signupOptions.URL, {
        method: signupOptions.method,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(signupOptions.body)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error(`Signup failed: ${response.status}`);
        }
        return response.json();
    })
    .then(data => {
        document.getElementById("signupMessage").textContent = "Signup successful!";
        // Optionally redirect to login page or handle as needed
        // window.location.href = '{{site.baseurl}}/profile';
    })
    .catch(error => {
        console.error("Signup Error:", error);
        document.getElementById("signupMessage").textContent = `Signup Error: ${error.message}`;
        // Re-enable the button if there is an error
        signupButton.disabled = false;
        signupButton.style.backgroundColor = ''; // Reset to default color
    });
}


    // Function to fetch and display Python data
    function pythonDatabase() {
        const URL = `${pythonURI}/api/id`;

        fetch(URL, fetchOptions)
            .then(response => {
                if (!response.ok) {
                    throw new Error(`Flask server response: ${response.status}`);
                }
                return response.json();
            })
            .then(data => {
                window.location.href = '{{site.baseurl}}/profile';
            })
            .catch(error => {
                console.error("Python Database Error:", error);
                const errorMsg = `Python Database Error: ${error.message}`;
            });
    }

    // Call relevant database functions on the page load
    window.onload = function() {
         pythonDatabase();
    };
</script>
