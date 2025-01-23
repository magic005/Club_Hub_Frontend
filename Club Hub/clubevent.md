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
        .event-box {
            margin-top: 20px;
            padding: 20px;
            border: 2px solid #FF3B3B;
            border-radius: 8px;
            background-color: #073461;
            color: white;
            width: 50%;
            margin: 20px auto;
        }
        .event-box h3 {
            margin: 0;
            padding-bottom: 10px;
            font-size: 24px;
        }
        .event-box p {
            margin: 5px 0;
        }
        .delete-btn {
            background-color: #dc3545;
            color: white;
            padding: 5px 10px;
            font-size: 14px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .delete-btn:hover {
            background-color: #c82333;
        }
        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
            margin-top: 20px;
        }
        .calendar div {
            padding: 20px;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
        }
        .calendar .header {
            background-color: #0056b3;
            font-weight: bold;
        }
        .event-details {
            display: none;
            margin-top: 20px;
            padding: 20px;
            border: 2px solid #FF3B3B;
            border-radius: 8px;
            background-color: #001F3F;
            color: white;
        }
    </style>
</head>
<body>
    <br>
    <button class="show-form-btn" id="showFormBtn">Create a New Event</button>
    <br>
    <div class="form-container" id="formContainer">
        <h2>Event Registration Form</h2>
        <form id="eventForm">
            <div class="form-group">
                <label for="eventTitle">Club Name</label>
                <input type="text" id="eventTitle" placeholder="Enter event title" required>
            </div>
            <div class="form-group">
                <label for="eventDescription">Event Description</label>
                <input type="text" id="eventDescription" placeholder="Describe your event" required>
            </div>
            <div class="form-group">
                <label for="eventDate">Event Date</label>
                <input type="date" id="eventDate" required>
            </div>
            <button type="submit" class="submit-btn">Create Event</button>
        </form>
    </div>
    <div id="eventListContainer">
        <!-- New events will appear here -->
    </div>
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
    <script>
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
        let events = [];
        let currentYear = new Date().getFullYear();
        let currentMonth = new Date().getMonth();
        // Show the form when the "Create a New Event" button is clicked
        showFormBtn.addEventListener('click', function () {
            formContainer.style.display = 'block';
        });
        // Handle form submission
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
                try {
                    // Send a POST request to the backend
                    const response = await fetch('http://127.0.0.1:8887/api/event', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify(payload)
                    });
                    if (response.ok) {
                        const createdEvent = await response.json();
                        // Add the newly created event to the UI
                        const eventBox = document.createElement('div');
                        eventBox.classList.add('event-box');
                        eventBox.innerHTML = `
                            <h3>${createdEvent.title}</h3>
                            <p><strong>Description:</strong> ${createdEvent.description}</p>
                            <p><strong>Date:</strong> ${createdEvent.date}</p>
                            <button class="delete-btn" onclick="deleteEvent(${createdEvent.id})">Delete</button>
                        `;
                        eventListContainer.appendChild(eventBox);
                        // Reset the form and hide it
                        eventForm.reset();
                        formContainer.style.display = 'none';
                        // Add event to calendar events list
                        events.push(createdEvent);
                        // Refresh the calendar
                        initializeCalendar(currentYear, currentMonth);
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
        // Function to fetch and display all events
        async function fetchAndDisplayEvents() {
            try {
                // Send a GET request to the backend to fetch all events
                const response = await fetch('http://127.0.0.1:8887/api/event', {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
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
        // Function to delete an event
        async function deleteEvent(eventId) {
            try {
                // Send a DELETE request to the backend to delete the event
                const response = await fetch(`http://127.0.0.1:8887/api/event/${eventId}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json'
                    }
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