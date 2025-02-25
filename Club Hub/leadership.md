---
layout: post
title: Leadership Application Form
permalink: /applyleadership
menu: nav/home.html
show_reading_time: false
---

<body>
   <style>
       body {
           font-family: Arial, sans-serif;
           background-color: #f4f4f9;
           margin: 0;
           padding: 20px;
           color: #333;
       }
       .show-form-btn {
           background-color: #007bff;
           color: white;
           padding: 10px 20px;
           border: none;
           border-radius: 5px;
           cursor: pointer;
           font-size: 16px;
           margin-bottom: 20px;
           box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
       }
       .show-form-btn:hover {
           background-color: #0056b3;
       }
       .form-container {
           background: black;
           padding: 20px;
           border-radius: 10px;
           box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
           max-width: 500px;
           margin: 0 auto;
           display: none;
       }
       .form-group {
           margin-bottom: 15px;
       }
       label {
           font-weight: bold;
           margin-bottom: 5px;
           display: block;
       }
       input,
       select,
       textarea {
           width: 100%;
           padding: 10px;
           border: 1px solid #ccc;
           border-radius: 5px;
           font-size: 14px;
       }
       input:focus,
       select:focus,
       textarea:focus {
           border-color: #007bff;
           outline: none;
           box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
       }
       .submit-btn {
           background-color: #28a745;
           color: white;
           padding: 10px 20px;
           border: none;
           border-radius: 5px;
           cursor: pointer;
           font-size: 16px;
       }
       .submit-btn:hover {
           background-color: #218838;
       }
       #applicationListContainer {
           margin-top: 30px;
       }
       .application-box {
           background: black;
           padding: 15px;
           border-radius: 10px;
           box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
           margin-bottom: 20px;
       }
    .application-box h3 {
        margin-top: 0;
        background: linear-gradient(#FF416C, #FF4B2B);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }
       .application-box p {
           margin: 5px 0;
           line-height: 1.5;
       }
       .delete-btn, .update-btn {
           background-color: #dc3545;
           color: white;
           padding: 5px 10px;
           border: none;
           border-radius: 5px;
           cursor: pointer;
           font-size: 14px;
           margin-top: 10px;
       }
       .delete-btn:hover, .update-btn:hover {
           background-color: #bd2130;
       }
   </style>

   <br>
   <button class="show-form-btn" id="showFormBtn">Apply for Leadership</button>
   <br>
   <div class="form-container" id="formContainer">
       <h2>Leadership Application Form</h2>
       <form id="leadershipForm">
           <div class="form-group">
               <label for="applicantName">Your Name</label>
               <input type="text" id="applicantName" placeholder="Enter your full name" required>
           </div>
           <div class="form-group">
               <label for="role">Role</label>
               <input type="text" id="role" placeholder="Enter the role you are applying for" required>
           </div>
           <div class="form-group">
               <label for="club">Club</label>
               <select id="club" required>
                   <option value="">Select a Club</option>
                   <!-- Club options will be dynamically populated -->
               </select>
           </div>
           <div class="form-group">
               <label for="experience">Leadership Experience</label>
               <textarea id="experience" placeholder="Describe your leadership experience" rows="4" required></textarea>
           </div>
           <button type="submit" class="submit-btn">Submit Application</button>
       </form>
   </div>
   <div id="applicationListContainer">
       <!-- Submitted leadership applications will be listed here -->
   </div>

   <script type="module">
    import { pythonURI } from "{{site.baseurl}}/assets/js/api/config.js";
    const showFormBtn = document.getElementById('showFormBtn');
    const formContainer = document.getElementById('formContainer');
    const leadershipForm = document.getElementById('leadershipForm');
    const applicationListContainer = document.getElementById('applicationListContainer');
    const clubSelect = document.getElementById('club');
    const clubNameSelect = document.getElementById('clubName');

    let currentApplicationId = null; // Variable to track which application is being updated

    // Show the form when the button is clicked
    showFormBtn.addEventListener('click', function () {
        formContainer.style.display = 'block';
        leadershipForm.reset(); // Reset form when showing it
        currentApplicationId = null; // Clear current application id
    });

    // Fetch clubs from the server and populate the dropdown
async function fetchClubNames() {
    try {
        console.log("Fetching club names...");

        const response = await fetch(`${pythonURI}/api/clubs`, {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json',
                // Ensure token is defined, otherwise remove this line
                ...(typeof token !== "undefined" ? { 'Authorization': `Bearer ${token}` } : {})
            }
        });

        console.log("Response received:", response);

        if (!response.ok) {
            throw new Error(`Failed to fetch clubs: ${response.status} ${response.statusText}`);
        }

        const clubs = await response.json();
        console.log("Clubs received:", clubs);

        // Clear existing options
        const clubSelect = document.getElementById('club');
        clubSelect.innerHTML = '<option value="">Select a Club</option>';

        // Populate dropdown
        clubs.forEach(club => {
            const option = document.createElement('option');
            option.value = club.name;
            option.textContent = club.name;
            clubSelect.appendChild(option);
        });

        console.log("Club dropdown updated successfully.");
    } catch (error) {
        console.error("Error fetching club names:", error);
        alert("An error occurred while fetching club names. Check the console for details.");
    }
}

// Ensure this function is called when the page loads
document.addEventListener('DOMContentLoaded', fetchClubNames);


    // Handle form submission to create a new leadership application
    leadershipForm.addEventListener('submit', async function (e) {
        e.preventDefault();

        const applicantName = document.getElementById('applicantName').value.trim();
        const role = document.getElementById('role').value.trim();
        const club = document.getElementById('club').value.trim();
        const experience = document.getElementById('experience').value.trim();


        const payload = { name: applicantName, role, club, experience };

        try {
            let response;
            if (currentApplicationId) {
                // Update the application if an ID exists
                response = await fetch(`${pythonURI}/api/leadership/${currentApplicationId}`, {
                    method: 'PUT',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload),
                });
            } else {
                // Create a new application if no ID exists
                response = await fetch(`${pythonURI}/api/leadership`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload),
                });
            }

            if (response.ok) {
                const updatedApplication = await response.json();
                if (currentApplicationId) {
                    updateApplicationInUI(updatedApplication); // Update the application in UI
                } else {
                    addApplicationToUI(updatedApplication); // Add the new application to UI
                }
                leadershipForm.reset();
                formContainer.style.display = 'none';
            } else {
                alert('Error: Unable to submit your application.');
            }
        } catch {
            alert('An error occurred while submitting your application.');
        }
    });

    // Fetch and display all leadership applications on page load
async function fetchAndDisplayApplications() {
    try {
        const URL = `${pythonURI}/api/leadership`;
        const response = await fetch(URL, { method: 'GET' });
        
        if (!response.ok) throw new Error('Failed to fetch applications');
        
        const applications = await response.json();
        applicationListContainer.innerHTML = ''; // Clear the list container

        if (applications.length > 0) {
            applications.forEach(app => addApplicationToUI(app)); // Add each application to the UI
        } else {
            applicationListContainer.innerText = 'No applications available.';
        }
    } catch (error) {
        console.error('Error fetching applications:', error);
        alert('An error occurred while fetching applications.');
    }
}


    // Add a single leadership application to the UI
    function addApplicationToUI(application) {
        const applicationBox = document.createElement('div');
        applicationBox.classList.add('application-box');

        applicationBox.innerHTML = `
            <h3>${application.name}</h3>
            <p><strong>Role:</strong> ${application.role}</p>
            <p><strong>Club:</strong> ${application.club}</p>
            <p><strong>Experience:</strong> ${application.experience}</p>
            <button class="delete-btn" data-id="${application.id}">Delete</button>
            <button class="update-btn" data-id="${application.id}">Update</button>
        `;

        // Add delete functionality to the delete button
        const deleteBtn = applicationBox.querySelector('.delete-btn');
        deleteBtn.addEventListener('click', async function () {
            const applicationId = this.getAttribute('data-id');

            if (confirm('Are you sure you want to delete this application?')) {
                try {
                    const response = await fetch(`${pythonURI}/api/leadership/${applicationId}`, {
                        method: 'DELETE',
                    });

                    if (response.ok) {
                        applicationBox.remove(); // Remove the deleted application from the UI
                        alert('Application deleted successfully.');
                    } else {
                        const errorData = await response.json();
                        alert(`Error deleting the application: ${errorData.error}`);
                    }
                } catch {
                    alert('An error occurred while deleting the application.');
                }
            }
        });

        // Add update functionality to the update button
        const updateBtn = applicationBox.querySelector('.update-btn');
        updateBtn.addEventListener('click', function () {
            const applicationId = this.getAttribute('data-id');
            currentApplicationId = applicationId; // Set the current application ID to update

            // Pre-fill the form with the current application data
            document.getElementById('applicantName').value = application.name;
            document.getElementById('role').value = application.role;
            document.getElementById('club').value = application.club;
            document.getElementById('experience').value = application.experience;

            formContainer.style.display = 'block'; // Show the form to update the details
        });

        // Append the application box to the list container
        applicationListContainer.appendChild(applicationBox);
    }

    // Update application UI without re-fetching
    function updateApplicationInUI(updatedApplication) {
        const applicationBox = document.querySelector(`.application-box[data-id="${updatedApplication.id}"]`);
        if (applicationBox) {
            applicationBox.querySelector('h3').textContent = updatedApplication.name;
            applicationBox.querySelector('p:nth-of-type(1)').textContent = `Role: ${updatedApplication.role}`;
            applicationBox.querySelector('p:nth-of-type(2)').textContent = `Club: ${updatedApplication.club}`;
            applicationBox.querySelector('p:nth-of-type(3)').textContent = `Experience: ${updatedApplication.experience}`;
        }
    }

    // Fetch and display applications when the page loads
    document.addEventListener('DOMContentLoaded', function() {
        fetchAndDisplayApplications();
        fetchClubs(); // Fetch clubs when the page loads
    });
   </script>
</body>
