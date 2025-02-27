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
            display: block;
            width: 100%;
            padding: 15px;
            background: linear-gradient(to right, #FF416C, #FF4B2B);
            color: #fff;
            font-size: 1.1em;
            font-weight: bold;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
       }
       .show-form-btn:hover {
            background: linear-gradient(to right, #FF4B2B, #FF416C);
            transform: translateY(-2px);
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
            background: linear-gradient(to right, #FF416C, #FF4B2B);
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
       }
       .submit-btn:hover {
            background: linear-gradient(to right, #FF4B2B, #FF416C);
            transform: translateY(-2px);
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
            background: linear-gradient(to right, #FF416C, #FF4B2B);
            color: white;
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            margin-top: 10px;
            transition: all 0.3s ease;
       }
       .delete-btn:hover, .update-btn:hover {
            background: linear-gradient(to right, #FF4B2B, #FF416C);
            transform: translateY(-2px);
       }
       .pagination {
           display: flex;
           justify-content: center;
           margin-top: 20px;
       }
       .pagination button {
           background: linear-gradient(to right, #FF416C, #FF4B2B);
           color: white;
           padding: 10px;
           border: none;
           border-radius: 5px;
           cursor: pointer;
           font-size: 14px;
           margin: 0 5px;
           transition: all 0.3s ease;
       }
       .pagination button:hover {
           background: linear-gradient(to right, #FF4B2B, #FF416C);
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
   <div class="pagination" id="paginationContainer">
       <button id="prevPageBtn" disabled>Previous</button>
       <button id="nextPageBtn" disabled>Next</button>
   </div>

   <script type="module">
    import { pythonURI } from "{{site.baseurl}}/assets/js/api/config.js";
    const showFormBtn = document.getElementById('showFormBtn');
    const formContainer = document.getElementById('formContainer');
    const leadershipForm = document.getElementById('leadershipForm');
    const applicationListContainer = document.getElementById('applicationListContainer');
    const clubSelect = document.getElementById('club');
    const prevPageBtn = document.getElementById('prevPageBtn');
    const nextPageBtn = document.getElementById('nextPageBtn');

    let currentApplicationId = null; // Variable to track which application is being updated
    let currentPage = 1; // Current page for pagination
    const applicationsPerPage = 5; // Number of applications per page

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
                }
            });

            if (!response.ok) {
                throw new Error(`Failed to fetch clubs: ${response.status} ${response.statusText}`);
            }

            const clubs = await response.json();

            // Clear existing options
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

    // Fetch and display all leadership applications on page load
async function fetchAndDisplayApplications() {
    try {
        const URL = `${pythonURI}/api/leadership?page=${currentPage}&limit=${applicationsPerPage}`;
        const response = await fetch(URL, { method: 'GET' });

        if (!response.ok) throw new Error('Failed to fetch applications');

        const data = await response.json();
        console.log('API Response:', data); // Log the full response

        // Check if applications is defined and is an array
        if (!data.applications || !Array.isArray(data.applications)) {
            console.error('Received data:', data); // Log the received data for debugging
            throw new Error('Applications not found in the response');
        }

        applicationListContainer.innerHTML = ''; // Clear the list container

        if (data.applications.length > 0) {
            data.applications.forEach(app => addApplicationToUI(app)); // Add each application to the UI
            updatePaginationButtons(data.totalCount); // Update pagination buttons based on total count
        } else {
            applicationListContainer.innerText = 'No applications available.';
        }
    } catch (error) {
        console.error('Error fetching applications:', error);
        alert('An error occurred while fetching applications: ' + error.message);
    }
}


    // Update pagination buttons based on current page
    function updatePaginationButtons(totalCount) {
        const totalPages = Math.ceil(totalCount / applicationsPerPage);
        prevPageBtn.disabled = currentPage === 1;
        nextPageBtn.disabled = currentPage === totalPages;
    }

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
                fetchAndDisplayApplications(); // Refresh the applications list
            } else {
                alert('Error: Unable to submit your application.');
            }
        } catch {
            alert('An error occurred while submitting your application.');
        }
    });

    // Add a single leadership application to the UI
    function addApplicationToUI(application) {
        const applicationBox = document.createElement('div');
        applicationBox.classList.add('application-box');
        applicationBox.setAttribute('data-id', application.id);

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
                        fetchAndDisplayApplications(); // Refresh the applications list
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
            currentApplicationId = application.id; // Set the current application ID for updating
            document.getElementById('applicantName').value = application.name;
            document.getElementById('role').value = application.role;
            document.getElementById('club').value = application.club;
            document.getElementById('experience').value = application.experience;
            formContainer.style.display = 'block'; // Show the form to update
        });

        applicationListContainer.appendChild(applicationBox);
    }

    // Update the application in the UI (for updates)
    function updateApplicationInUI(application) {
        const applicationBox = applicationListContainer.querySelector(`[data-id='${application.id}']`);
        if (applicationBox) {
            applicationBox.innerHTML = `
                <h3>${application.name}</h3>
                <p><strong>Role:</strong> ${application.role}</p>
                <p><strong>Club:</strong> ${application.club}</p>
                <p><strong>Experience:</strong> ${application.experience}</p>
                <button class="delete-btn" data-id="${application.id}">Delete</button>
                <button class="update-btn" data-id="${application.id}">Update</button>
            `;
        }
    }

    // Handle pagination button clicks
    prevPageBtn.addEventListener('click', function () {
        if (currentPage > 1) {
            currentPage--;
            fetchAndDisplayApplications();
        }
    });

    nextPageBtn.addEventListener('click', function () {
        currentPage++;
        fetchAndDisplayApplications();
    });

    // Fetch club names and applications on page load
    fetchClubNames();
    fetchAndDisplayApplications();
   </script>
</body>
