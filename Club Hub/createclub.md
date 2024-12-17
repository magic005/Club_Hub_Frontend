---
layout: post
title: Create Club
permalink: /createclub
menu: nav/home.html
show_reading_time: false
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Club Creator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #FDF5E6;
            text-align: center;
            padding: 50px;
        }
        .form-container {
            display: none; /* Hidden initially */
            margin-top: 20px;
            padding: 20px;
            border: 2px solid #FF3B3B;
            border-radius: 8px;
            background-color: #001F3F;
            width: 50%;
            margin: 0 auto;
        }
        .form-group {
            margin: 15px 0;
        }
        .form-group label {
            display: block;
            font-size: 18px;
        }
        .form-group input {
            width: 90%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #007bff;
            border-radius: 5px;
        }
        .submit-btn {
            background-color: #007bff;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .submit-btn:hover {
            background-color: #0056b3;
        }
        .show-form-btn {
            background-color: #28a745;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            border: 2px solid #FF3B3B;
            border-radius: 5px;
            cursor: pointer;
        }
        .show-form-btn:hover {
            background-color: #218838;
        }
        .club-box {
            margin-top: 20px;
            padding: 20px;
            border: 2px solid #FF3B3B;
            border-radius: 8px;
            background-color: #073461;
            color: white;
            width: 50%;
            margin: 20px auto;
        }
        .club-box h3 {
            margin: 0;
            padding-bottom: 10px;
            font-size: 24px;
        }
        .club-box p {
            margin: 5px 0;
        }
    </style>
</head>
<body>
    <h1>Create a Club</h1>
    <button class="show-form-btn" id="showFormBtn">Start a New Club</button>
    <div class="form-container" id="formContainer">
        <h2>Club Registration Form</h2>
        <form id="clubForm">
            <div class="form-group">
                <label for="clubName">Club Name</label>
                <input type="text" id="clubName" placeholder="Enter club name" required>
            </div>
            <div class="form-group">
                <label for="clubDescription">Club Description</label>
                <input type="text" id="clubDescription" placeholder="Describe your club" required>
            </div>
            <div class="form-group">
                <label for="clubLeader">Club Leader Name</label>
                <input type="text" id="clubLeader" placeholder="Enter leader's name" required>
            </div>
            <button type="submit" class="submit-btn">Create Club</button>
        </form>
    </div>
    <div id="clubListContainer">
        <!-- New clubs will appear here -->
    </div>
    <script>
        const showFormBtn = document.getElementById('showFormBtn');
        const formContainer = document.getElementById('formContainer');
        const clubForm = document.getElementById('clubForm');
        const clubListContainer = document.getElementById('clubListContainer');
        // Show the form when the "Start a New Club" button is clicked
        showFormBtn.addEventListener('click', function () {
            formContainer.style.display = 'block';
        });
        // Handle form submission
        clubForm.addEventListener('submit', function (e) {
            e.preventDefault();
            // Get values from form inputs
            const clubName = document.getElementById('clubName').value.trim();
            const clubDescription = document.getElementById('clubDescription').value.trim();
            const clubLeader = document.getElementById('clubLeader').value.trim();
            if (clubName && clubDescription && clubLeader) {
                // Create a new club box
                const clubBox = document.createElement('div');
                clubBox.classList.add('club-box');
                // Set club details
                clubBox.innerHTML = `
                    <h3>${clubName}</h3>
                    <p><strong>Description:</strong> ${clubDescription}</p>
                    <p><strong>Leader:</strong> ${clubLeader}</p>
                `;
                // Append the new club box to the club list container
                clubListContainer.appendChild(clubBox);
                // Reset the form and hide it
                clubForm.reset();
                formContainer.style.display = 'none';
            } else {
                alert("Please fill out all fields!");
            }
        });
    </script>
</body>
</html>