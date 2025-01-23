---
layout: post
title: Club Hub Events
permalink: /event1
menu: nav/home.html
show_reading_time: false
---



<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Management</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #1e1e2f;
            color: #e0e0e0;
            margin: 0;
            padding: 20px;
            display: flex;
            gap: 20px;
            box-sizing: border-box;
        }
        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            width: 95%;
            max-width: 1600px;
        }
        .left-container {
            flex: 1;
            max-width: 60%;
            padding: 20px;
            background-color: #252540;
            border-radius: 16px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
        }
        .right-container {
            flex: 1;
            max-width: 58%; /* Increased the width of the right container */
            padding: 20px;
            background-color: #252540;
            border-radius: 16px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
        }
        h1, h2 {
            color: #00ffd5;
            margin-bottom: 20px;
        }
        .form-container {
            margin-top: 20px;
            padding: 20px;
            background-color: #2d2d44;
            border-radius: 16px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #00ffd5;
        }
        .form-group input {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 8px;
            background-color: #1e1e2f;
            color: #e0e0e0;
            font-size: 16px;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.3);
        }
        .submit-btn, .show-form-btn, .delete-btn {
            display: inline-block;
            padding: 10px 20px;
            margin-top: 10px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-transform: uppercase;
            transition: all 0.3s ease;
        }
        .submit-btn {
            background-color: #0077ff;
            color: #ffffff;
        }
        .submit-btn:hover {
            background-color: #005bcc;
        }
        .show-form-btn {
            background-color: #00ffd5;
            color: #1e1e2f;
        }
        .show-form-btn:hover {
            background-color: #00cca6;
        }
        .delete-btn {
            background-color: #ff3b3b;
            color: white;
        }
        .delete-btn:hover {
            background-color: #cc2f2f;
        }
        .event-box {
            margin-top: 20px;
            padding: 20px;
            background-color: #333356;
            color: white;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
        }
        .event-box h3 {
            color: #00ffd5;
        }
        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            background-color: #2d2d44;
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
        }
        .calendar div {
            text-align: center;
            padding: 15px;
            background-color: #4a4a6a;
            border-radius: 8px;
            color: #ffffff;
            font-weight: bold;
            cursor: pointer;
        }
        .calendar div:hover {
            background-color: #00ffd5;
            color: #1e1e2f;
        }
        .calendar .header {
            background-color: #0077ff;
            color: white;
        }
        .event-details {
            margin-top: 20px;
            padding: 20px;
            background-color: #2d2d44;
            border-radius: 16px;
            color: #e0e0e0;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
        }
        .event-details h2 {
            color: #00ffd5;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="left-container">
            <button class="show-form-btn" id="showFormBtn">Create a New Event</button>
            <div class="form-container" id="formContainer">
                <h2>Event Registration Form</h2>
                <form id="eventForm">
                    <div class="form-group">
                        <label for="eventTitle">Club Name</label>
                        <input type="text" id="eventTitle" placeholder="Enter club name" required>
                    </div>
                    <div class="form-group">
                        <label for="eventDescription">Event Description</label>
                        <input type="text" id="eventDescription" placeholder="Describe your event" required>
                    </div>
                    <div class="form-group">
                        <label for="eventDate">Event Date</label>
                        <input type="date" id="eventDate" required>
                    </div>
                    <input type="hidden" id="eventId"> <!-- This hidden field holds the event ID -->
                    <button type="submit" class="submit-btn" id="submitBtn">Create Event</button>
                    <button type="button" class="update-btn" id="updateBtn" style="display: none;">Update Event</button>
                </form>
            </div>
            <div id="eventListContainer">
                <!-- New events will appear here -->
            </div>
        </div>
        <div class="right-container">
            <h1>Calendar</h1>
            <div>
                <button id="prevMonthBtn">&lt; Previous</button>
                <span id="currentMonth"></span>
                <button id="nextMonthBtn">Next &gt;</button>
            </div>
            <div class="calendar" id="calendar"></div>
            <div class="event-details" id="eventDetails">
                <h2>Events on <span id="selectedDate"></span></h2>
                <div id="eventsOnDate"></div>
            </div>
        </div>
    <script>
        let events = []; //  store all the event data fetched from the server
        let currentYear = new Date().getFullYear();
        let currentMonth = new Date().getMonth();
        let editingEventId = null; // Store the ID of the event being edited
        // Declare all DOM elements at the top
        const showFormBtn = document.getElementById('showFormBtn'); 
        const formContainer = document.getElementById('formContainer');
        const eventForm = document.getElementById('eventForm');
        const eventListContainer = document.getElementById('eventListContainer');
        const calendar = document.getElementById('calendar');
        const eventDetails = document.getElementById('eventDetails');
        const selectedDateText = document.getElementById('selectedDate');
        const eventsOnDate = document.getElementById('eventsOnDate');
        const prevMonthBtn = document.getElementById('prevMonthBtn');
        const nextMonthBtn = document.getElementById('nextMonthBtn');
        const currentMonthText = document.getElementById('currentMonth');
        const submitBtn = document.getElementById('submitBtn'); // Get the submit button
        const updateBtn = document.getElementById('updateBtn'); // Get the update button
        // Show the form when the "Create a New Event" button is clicked
        showFormBtn.addEventListener('click', function () {
            formContainer.style.display = 'block';
            editingEventId = null; // Reset editingEventId when creating a new event
            submitBtn.style.display = 'inline-block'; // Show create button
            updateBtn.style.display = 'none'; // Hide update button
            eventForm.reset(); // Reset the form
        });
        // Handles the form submission for creating an event. If the form is valid, a POST request is sent to the backend API to create a new event.
        eventForm.addEventListener('submit', async function (e) {
            e.preventDefault(); // Prevent default form submission
            // Get values from form inputs
            const eventTitle = document.getElementById('eventTitle').value.trim();
            const eventDescription = document.getElementById('eventDescription').value.trim();
            const eventDate = document.getElementById('eventDate').value;
            // Check if all required fields are filled
            if (eventTitle && eventDescription && eventDate) {
                const payload = {
                    title: eventTitle,
                    description: eventDescription,
                    date: eventDate,
                };
                const token = localStorage.getItem('authToken'); // Replace 'authToken' with the key where you store your token
                try {
                    const response = await fetch('http://127.0.0.1:8887/api/event', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                            'Authorization': `Bearer ${token}` // Add the token to the request headers
                        },
                        body: JSON.stringify(payload)
                    });
                    if (response.ok) {
                        fetchAndDisplayEvents(); // Refresh the event list
                        formContainer.style.display = 'none'; // Hide the form
                    } else {
                        const error = await response.json();
                        alert(`Error: ${error.message}`);
                    }
                } catch (error) {
                    alert('An error occurred while creating the event. Please try again.');
                    console.error(error);
                }
            } else {
                alert("Please fill out all fields!");
            }
        });
        // Handle form submission for updating events
        updateBtn.addEventListener('click', async function () {
            // Get values from form inputs
            const eventTitle = document.getElementById('eventTitle').value.trim();
            const eventDescription = document.getElementById('eventDescription').value.trim();
            const eventDate = document.getElementById('eventDate').value;
            const eventId = editingEventId; // Use the editingEventId variable
            console.log('Updating event with ID:', eventId); // Log the event ID
            console.log('Payload:', {
                id: eventId,
                title: eventTitle,
                description: eventDescription,
                date: eventDate,
            });
            // Check if all required fields are filled
            if (eventTitle && eventDescription && eventDate && eventId) {
                const payload = {
                    id: eventId, // Include the event ID
                    title: eventTitle,
                    description: eventDescription,
                    date: eventDate,
                };
                const token = localStorage.getItem('authToken'); // Replace 'authToken' with the key where you store your token
                try {
                    // Send a PUT request to update the event
                    const response = await fetch(`http://127.0.0.1:8887/api/event`, {
                        method: 'PUT',
                        headers: {
                            'Content-Type': 'application/json',
                            'Authorization': `Bearer ${token}`, // Add the token to the request headers
                        },
                        body: JSON.stringify(payload),
                    });
                    if (response.ok) {
                        fetchAndDisplayEvents(); // Refresh the event list
                        formContainer.style.display = 'none'; // Hide the form
                        alert('Event updated successfully!');
                    } else {
                        const error = await response.json();
                        alert(`Error: ${error.message}`);
                    }
                } catch (error) {
                    alert('An error occurred while updating the event. Please try again.');
                    console.error(error);
                }
            } else {
                alert('Please fill out all fields!');
            }
        });
        // Function to fetch and display all events
        async function fetchAndDisplayEvents() {
            const token = localStorage.getItem('authToken'); // Replace 'authToken' with the key where you store your token
            try {
                // Send a GET request to the backend to fetch all events
                const response = await fetch('http://127.0.0.1:8887/api/event', {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${token}` // Add the token to the request headers
                    }
                });
                if (response.ok) {
                    const fetchedEvents = await response.json();
                    events = fetchedEvents;
                    // Clear the existing event list
                    eventListContainer.innerHTML = '';
                    // Add each event to the UI
                    events.forEach(event => {
                        const eventBox = document.createElement('div');
                        eventBox.classList.add('event-box');
                        eventBox.innerHTML = `
                            <h3>${event.title}</h3>
                            <p><strong>Description:</strong> ${event.description}</p>
                            <p><strong>Date:</strong> ${event.date}</p>
                            <button class="edit-btn" onclick="editEvent(${event.id})">Edit</button>
                            <button class="delete-btn" onclick="deleteEvent(${event.id})">Delete</button>
                        `;
                        eventListContainer.appendChild(eventBox);
                    });
                    // Initialize the calendar
                    initializeCalendar(currentYear, currentMonth);
                } else {
                    const error = await response.json();
                    alert(`Error: ${error.message}`);
                }
            } catch (error) {
                alert('An error occurred while fetching events. Please try again.');
                console.error(error);
            }
        }
        // Function to edit an event
        function editEvent(eventId) {
            const event = events.find(e => e.id === eventId);
            if (event) {
                // Pre-fill the form with the current event data
                document.getElementById('eventTitle').value = event.title;
                document.getElementById('eventDescription').value = event.description;
                document.getElementById('eventDate').value = event.date;
                // Show the form
                formContainer.style.display = 'block';
                submitBtn.style.display = 'none'; // Hide create button
                updateBtn.style.display = 'inline-block'; // Show update button
                editingEventId = eventId; // Store the ID of the event being edited
            }
        }
        // Function to delete an event
        async function deleteEvent(eventId) {
            const token = localStorage.getItem('authToken'); // Replace 'authToken' with the key where you store your token
            try {
                // Send a DELETE request to the backend to delete the event
                const response = await fetch(`http://127.0.0.1:8887/api/event`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${token}` // Add the token to the request headers
                    },
                    body: JSON.stringify({ id: eventId }) // Pass the event ID in the request body
                });
                if (response.ok) {
                    alert('Event deleted successfully!');
                    fetchAndDisplayEvents(); // Refresh the event list
                } else {
                    const error = await response.json();
                    alert(`Error: ${error.message}`);
                }
            } catch (error) {
                alert('An error occurred while deleting the event. Please try again.');
                console.error(error);
            }
        }
        // Function to initialize the calendar
        function initializeCalendar(year, month) {
            const daysInMonth = new Date(year, month + 1, 0).getDate();
            const firstDayOfMonth = new Date(year, month, 1).getDay();
            // Clear existing calendar
            calendar.innerHTML = '';
            // Generate calendar headers
            const headers = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
            headers.forEach(header => {
                const headerDiv = document.createElement('div');
                headerDiv.classList.add('header');
                headerDiv.textContent = header;
                calendar.appendChild(headerDiv);
            });
            // Generate empty days before the first day of the month
            for (let i = 0; i < firstDayOfMonth; i++) {
                const emptyDiv = document.createElement('div');
                emptyDiv.textContent = '';
                calendar.appendChild(emptyDiv);
            }
            // Generate calendar days
            for (let day = 1; day <= daysInMonth; day++) {
                const dayDiv = document.createElement('div');
                dayDiv.textContent = day;
                dayDiv.addEventListener('click', function () {
                    const selectedDate = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    selectedDateText.textContent = selectedDate;
                    showEventsOnDate(selectedDate);
                });
                calendar.appendChild(dayDiv);
            }
            // Update current month text
            const monthNames = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            currentMonthText.textContent = `${monthNames[month]} ${year}`;
        }
        // Show events on the selected date
        function showEventsOnDate(date) {
            eventsOnDate.innerHTML = '';
            const filteredEvents = events.filter(event => event.date === date);
            if (filteredEvents.length > 0) {
                eventDetails.style.display = 'block';
                filteredEvents.forEach(event => {
                    const eventItem = document.createElement('div');
                    eventItem.classList.add('event-item');
                    eventItem.innerHTML = `<strong>${event.title}</strong><p>${event.description}</p>`;
                    eventsOnDate.appendChild(eventItem);
                });
            } else {
                eventsOnDate.innerHTML = '<p>No events on this date.</p>';
            }
        }
        // Event listeners for month navigation buttons
        prevMonthBtn.addEventListener('click', function () {
            currentMonth--;
            if (currentMonth < 0) {
                currentMonth = 11;
                currentYear--;
            }
            initializeCalendar(currentYear, currentMonth);
        });
        nextMonthBtn.addEventListener('click', function () {
            currentMonth++;
            if (currentMonth > 11) {
                currentMonth = 0;
                currentYear++;
            }
            initializeCalendar(currentYear, currentMonth);
        });
        // Call fetchAndDisplayEvents on page load
        document.addEventListener('DOMContentLoaded', fetchAndDisplayEvents);
    </script>
</body>
</html>