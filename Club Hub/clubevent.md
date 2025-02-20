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
                        <label for="clubName">Club Name</label>
                        <select id="clubName" required>
                            <option value="">Select club</option>
                        </select>
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

<script type="module">
    import { pythonURI } from "{{site.baseurl}}/assets/js/api/config.js";
    let events = []; // store all the event data fetched from the server
    let currentYear = new Date().getFullYear();
    let currentMonth = new Date().getMonth();
    let editingEventId = null; // Store the ID of the event being edited
    let currentPage = 1; // Default starting page for pagination

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
    const clubNameSelect = document.getElementById('clubName'); // Get the club name dropdown

    // Show the form when the "Create a New Event" button is clicked
    showFormBtn.addEventListener('click', function () {
        formContainer.style.display = 'block';
        editingEventId = null; // Reset editingEventId when creating a new event
        submitBtn.style.display = 'inline-block'; // Show create button
        updateBtn.style.display = 'none'; // Hide update button
        eventForm.reset(); // Reset the form
    });

    // Fetch club names on page load
    document.addEventListener('DOMContentLoaded', fetchClubNames);

    // Fetch club names from the backend API
    async function fetchClubNames() {
        const token = localStorage.getItem('authToken');
        try {
            const response = await fetch(`${pythonURI}/api/club`, {
                method: 'GET',
                headers: {
                    'Content-Type': 'application/json',
                },
                credentials: 'include',
            });
            if (response.ok) {
                const clubs = await response.json();
                clubs.forEach(club => {
                    const option = document.createElement('option');
                    option.value = club.name;
                    option.textContent = club.name;
                    clubNameSelect.appendChild(option);
                });
            } else {
                const error = await response.json();
                alert(`Error: ${error.message}`);
            }
        } catch (error) {
            alert('An error occurred while fetching club names. Please try again.');
            console.error(error);
        }
    }

    // Handles the form submission for creating an event. If the form is valid, a POST request is sent to the backend API to create a new event.
    eventForm.addEventListener('submit', async function (e) {
        e.preventDefault(); // Prevent default form submission
        const clubName = clubNameSelect.value.trim();
        const eventDescription = document.getElementById('eventDescription').value.trim();
        const eventDate = document.getElementById('eventDate').value;

        // Check if all required fields are filled
        if (clubName && eventDescription && eventDate) {
            const payload = {
                title: clubName,
                description: eventDescription,
                date: eventDate,
            };
            const token = localStorage.getItem('authToken');
            try {
                const response = await fetch(`${pythonURI}/api/event`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    credentials: 'include',
                    body: JSON.stringify(payload),
                });
                if (response.ok) {
                    fetchAndDisplayEvents(currentPage); // Refresh the event list
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
        const clubName = clubNameSelect.value.trim();
        const eventDescription = document.getElementById('eventDescription').value.trim();
        const eventDate = document.getElementById('eventDate').value;
        const eventId = editingEventId;
        console.log('Updating event with ID:', eventId);
        console.log('Payload:', {
            id: eventId,
            title: clubName,
            description: eventDescription,
            date: eventDate,
        });

        // Check if all required fields are filled
        if (clubName && eventDescription && eventDate && eventId) {
            const payload = {
                id: eventId,
                title: clubName,
                description: eventDescription,
                date: eventDate,
            };
            const token = localStorage.getItem('authToken');
            try {
                const response = await fetch(`${pythonURI}/api/event`, {
                    method: 'PUT',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    credentials: 'include',
                    body: JSON.stringify(payload),
                });
                if (response.ok) {
                    fetchAndDisplayEvents(currentPage); // Refresh the event list
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
    async function fetchAndDisplayEvents(page = 1) {
        const token = localStorage.getItem('authToken');
        try {
            const response = await fetch(`${pythonURI}/api/event`, {
                method: 'GET',
                headers: {
                    'Content-Type': 'application/json',
                },
                credentials: 'include',
            });
            if (response.ok) {
                const fetchedEvents = await response.json();
                events = fetchedEvents.sort((a, b) => new Date(b.date) - new Date(a.date)); // Sort events by date descending
                const eventsPerPage = 10;
                const totalEvents = events.length;
                const totalPages = Math.ceil(totalEvents / eventsPerPage);
                const startIndex = (page - 1) * eventsPerPage;
                const paginatedEvents = events.slice(startIndex, startIndex + eventsPerPage);

                // Clear the existing event list
                eventListContainer.innerHTML = '';

                // Add each event to the UI
                paginatedEvents.forEach(event => {
                    const eventBox = document.createElement('div');
                    eventBox.classList.add('event-box');
                    eventBox.innerHTML = `
                        <h3>${event.title}</h3>
                        <p><strong>Description:</strong> ${event.description}</p>
                        <p><strong>Date:</strong> ${event.date}</p>
                        <button class="edit-btn">Edit</button>
                        <button class="delete-btn">Delete</button>
                    `;
                    eventListContainer.appendChild(eventBox);

                    const editBtn = eventBox.querySelector('.edit-btn');
                    const deleteBtn = eventBox.querySelector('.delete-btn');

                    // Add click listener for edit
                    editBtn.addEventListener('click', () => editEvent(event.id));
                    // Add click listener for delete
                    deleteBtn.addEventListener('click', () => deleteEvent(event.id));
                });

                // Pagination controls
                const pagination = document.createElement('div');
                pagination.classList.add('pagination');

                if (page > 1) {
                    const prevPageBtn = document.createElement('button');
                    prevPageBtn.textContent = 'Previous';
                    prevPageBtn.addEventListener('click', () => fetchAndDisplayEvents(page - 1));
                    pagination.appendChild(prevPageBtn);
                }

                if (page < totalPages) {
                    const nextPageBtn = document.createElement('button');
                    nextPageBtn.textContent = 'Next';
                    nextPageBtn.addEventListener('click', () => fetchAndDisplayEvents(page + 1));
                    pagination.appendChild(nextPageBtn);
                }

                eventListContainer.appendChild(pagination);

                // Initialize the calendar with events
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
            document.getElementById('clubName').value = event.title;
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
        const token = localStorage.getItem('authToken');
        try {
            const response = await fetch(`${pythonURI}/api/event`, {
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json',
                },
                credentials: 'include',
                body: JSON.stringify({ id: eventId })
            });
            if (response.ok) {
                alert('Event deleted successfully!');
                fetchAndDisplayEvents(currentPage); // Refresh the event list
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

        // Add event dot if events are available for this day
        const formattedDate = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        if (events.some(event => event.date === formattedDate)) {
            const dot = document.createElement('div');
            dot.classList.add('event-dot'); // Add the event-dot class for styling
            dot.style.backgroundColor = 'white'; // Directly make the dot white
            dayDiv.appendChild(dot);
        }


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

    // Show events on a specific date
    function showEventsOnDate(date) {
        eventsOnDate.innerHTML = ''; // Clear existing events on the selected date
        const eventsOnSelectedDate = events.filter(event => event.date === date);
        if (eventsOnSelectedDate.length === 0) {
            eventsOnDate.innerHTML = '<p>No events for this date.</p>';
        } else {
            eventsOnSelectedDate.forEach(event => {
                const eventDiv = document.createElement('div');
                eventDiv.classList.add('event-box');
                eventDiv.innerHTML = `
                    <h3>${event.title}</h3>
                    <p><strong>Description:</strong> ${event.description}</p>
                    <p><strong>Date:</strong> ${event.date}</p>
                `;
                eventsOnDate.appendChild(eventDiv);
            });
        }
    }

    // Handle next and previous month buttons
    prevMonthBtn.addEventListener('click', () => {
        currentMonth--;
        if (currentMonth < 0) {
            currentMonth = 11;
            currentYear--;
        }
        initializeCalendar(currentYear, currentMonth);
        fetchAndDisplayEvents(currentPage); // Refresh event list after month change
    });

    nextMonthBtn.addEventListener('click', () => {
        currentMonth++;
        if (currentMonth > 11) {
            currentMonth = 0;
            currentYear++;
        }
        initializeCalendar(currentYear, currentMonth);
        fetchAndDisplayEvents(currentPage); // Refresh event list after month change
    });

    // Initial load
    initializeCalendar(currentYear, currentMonth);
    fetchAndDisplayEvents(currentPage);
</script>
