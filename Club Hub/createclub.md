---
layout: post
title: Club Creator
permalink: /createclub
menu: nav/home.html
show_reading_time: false
---

<br>
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
        width: 75%;
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
    #clubTopics {
        display: grid;
        grid-template-columns: repeat(3, 1fr); /* 3 equal-width columns */
        gap: 10px 0; /* Add vertical spacing between rows */
    }
    #clubTopics label {
        display: grid;
        grid-template-columns: 20px auto; /* Fixed width for checkboxes */
        align-items: center; /* Center checkbox and text vertically */
        justify-items: start; /* Align text to the left */
        gap: 10px; /* Space between checkbox and text */
    }


</style>

<body>
    <br>
    <button class="show-form-btn" id="showFormBtn">Start a New Club</button>
    <br>
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
                <label for="clubTopics">Club Topics</label>
                <br>
                <div id="clubTopics">
                    <label><input type="checkbox" name="topics" value="Cyber"> Cyber</label>
                    <label><input type="checkbox" name="topics" value="Robots"> Robots</label>
                    <label><input type="checkbox" name="topics" value="AI"> AI</label>
                    <label><input type="checkbox" name="topics" value="Photos"> Photos</label>
                    <label><input type="checkbox" name="topics" value="Space"> Space</label>
                    <label><input type="checkbox" name="topics" value="Games"> Games</label>
                    <label><input type="checkbox" name="topics" value="Code"> Code</label>
                    <label><input type="checkbox" name="topics" value="ML"> ML</label>
                    <label><input type="checkbox" name="topics" value="Chain"> Chain</label>
                    <label><input type="checkbox" name="topics" value="Music"> Music</label>
                    <label><input type="checkbox" name="topics" value="Arts"> Arts</label>
                    <label><input type="checkbox" name="topics" value="Fitness"> Fitness</label>
                    <label><input type="checkbox" name="topics" value="Cooking"> Cooking</label>
                    <label><input type="checkbox" name="topics" value="Travel"> Travel</label>
                    <label><input type="checkbox" name="topics" value="Language"> Language</label>
                    <label><input type="checkbox" name="topics" value="Business"> Business</label>
                    <label><input type="checkbox" name="topics" value="Finance"> Finance</label>
                    <label><input type="checkbox" name="topics" value="Stars"> Stars</label>
                    <label><input type="checkbox" name="topics" value="Cars"> Cars</label>
                    <label><input type="checkbox" name="topics" value="Literature"> Literature</label>
                    <label><input type="checkbox" name="topics" value="Psychology"> Psychology</label>
                    <label><input type="checkbox" name="topics" value="History"> History</label>
                    <label><input type="checkbox" name="topics" value="Math"> Math</label>
                    <label><input type="checkbox" name="topics" value="Biology"> Biology</label>
                    <label><input type="checkbox" name="topics" value="Chemistry"> Chemistry</label>
                    <label><input type="checkbox" name="topics" value="Physics"> Physics</label>
                    <label><input type="checkbox" name="topics" value="Teaching"> Teaching</label>
                    <label><input type="checkbox" name="topics" value="Volunteering"> Volunteering</label>
                    <label><input type="checkbox" name="topics" value="Fashion"> Fashion</label>
                    <label><input type="checkbox" name="topics" value="Fundraising"> Fundraising</label>
                </div>
                <br>
                <small>*Please select all relevant topics for your club.*</small>
                <br>
            </div>
            <button type="submit" class="submit-btn">Create Club</button>
        </form>
    </div>
    <div id="clubListContainer">
        <!-- New clubs will appear here -->
    </div>
    <script>
        // Declare all DOM elements at the top
        const showFormBtn = document.getElementById('showFormBtn');
        const formContainer = document.getElementById('formContainer');
        const clubForm = document.getElementById('clubForm');
        const clubListContainer = document.getElementById('clubListContainer'); 
        // Show the form when the "Start a New Club" button is clicked
        showFormBtn.addEventListener('click', function () {
            formContainer.style.display = 'block';
        });
        // Handle form submission
        clubForm.addEventListener('submit', async function (e) {
            e.preventDefault(); // Prevent default form submission
//
            // Get values from form inputs
            const clubName = document.getElementById('clubName').value.trim();
            const clubDescription = document.getElementById('clubDescription').value.trim();
//
            // Collect selected checkboxes
            const selectedTopics = [];
            document.querySelectorAll('input[name="topics"]:checked').forEach((checkbox) => {
                selectedTopics.push(checkbox.value);
            });
//
            // Check if all required fields are filled
            if (clubName && clubDescription && selectedTopics.length > 0) {
                const payload = {
                    name: clubName,
                    description: clubDescription,
                    topics: selectedTopics,
                };
//
                try {
                    // Send a POST request to the backend
                    const response = await fetch('http://127.0.0.1:8887/api/club', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                            'Authorization': `Bearer ${localStorage.getItem('token')}` // Include token if required
                        },
                        body: JSON.stringify(payload)
                    });
//
                    if (response.ok) {
                        const createdClub = await response.json();
//
                        // Add the newly created club to the UI
                        const clubBox = document.createElement('div');
                        clubBox.classList.add('club-box');
                        clubBox.innerHTML = `
                            <h3>${createdClub.name}</h3>
                            <p><strong>Description:</strong> ${createdClub.description}</p>
                            <p><strong>Topics:</strong> ${createdClub.topics.join(', ')}</p>
                        `;
                        clubListContainer.appendChild(clubBox);
//
                        // Reset the form and hide it
                        clubForm.reset();
                        formContainer.style.display = 'none';
                    } else {
                        const error = await response.json();
                        alert(`Error: ${error.message}`);
                    }
                } catch (error) {
                    alert('An error occurred while creating the club. Please try again.');
                    console.error(error);
                }
            } else {
                alert("Please fill out all fields and select at least one topic!");
            }
        });
    </script>

