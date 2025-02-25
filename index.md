---
layout: post
title: Club Hub
search_exclude: true
description: Login and explore our social media hub for everything DNHS 
hide: true
menu: nav/home.html
---

<style>
    body {
        margin: 0;
        font-family: 'Roboto', Arial, sans-serif;
        background-color: #0E0E10;
        color: #F3F3F3;
        line-height: 1.6;
    }
    .header {
        background: linear-gradient(to right, #4A00E0, #8E2DE2);
        text-align: center;
        padding: 40px 20px;
        color: #fff;
        font-size: 2em;
        font-weight: bold;
    }
    .container {
        max-width: 900px;
        margin: 40px auto;
        padding: 20px;
        background: #1A1A1D;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    }
    h2 {
        text-align: center;
        font-weight: 700;
        color: #FF4D4D;
        margin-bottom: 10px;
    }
    .category {
        margin: 20px 0;
        padding: 20px;
        border: 2px solid;
        border-image: linear-gradient(to right, #FF416C, #FF4B2B) 1;
        border-radius: 10px;
        background: #2A2A2D;
        transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .category:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.8);
    }
    .post {
        margin: 10px 0;
        padding: 15px;
        background: #121212;
        border: 2px solid;
        border-image: linear-gradient(to right, #FF416C, #FF4B2B) 1;
        border-radius: 8px;
        transition: background 0.3s ease;
    }
    .post:hover {
        background: #1F1F23;
    }
    button {
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
    }
    button:hover {
        background: linear-gradient(to right, #FF4B2B, #FF416C);
        transform: translateY(-3px);
    }
    .form-container {
        padding: 20px;
        background: #1A1A1D;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        margin-top: 20px;
    }
    .form-container label {
        display: block;
        margin-bottom: 10px;
        color: #F3F3F3;
        font-size: 1.1em;
    }
    .form-container input,
    .form-container textarea {
        width: 100%;
        padding: 10px;
        margin-bottom: 15px;
        border: 1px solid #FF4B2B;
        border-radius: 5px;
        background: #121212;
        color: #F3F3F3;
        font-size: 1em;
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

    .right-container {
        flex: 1;
        max-width: 100%;
        padding: 20px;
        background: #1A1A1D;
        border-radius: 16px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        text-align: center;
    }
    h1, h2 {
        color: #FF4D4D;
        text-align: center;
        font-weight: 700;
    }
    .calendar {
        display: grid;
        grid-template-columns: repeat(7, 1fr);
        gap: 10px;
        background: #2A2A2D;
        padding: 20px;
        border-radius: 16px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    }
    .calendar div {
        text-align: center;
        padding: 15px;
        background: #4a4a6a;
        border-radius: 8px;
        color: #ffffff;
        font-weight: bold;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .calendar div:hover {
        background: #FF4D4D;
        color: #0E0E10;
        transform: scale(1.1);
    }
    .event-details {
        margin-top: 20px;
        padding: 20px;
        background: #2A2A2D;
        border-radius: 16px;
        color: #F3F3F3;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        text-align: center;
    }
    .event-details h2 {
        color: #FF4D4D;
    }
    .month-navigation {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 20px;
    }
    .month-navigation button {
        background-color: #4a4a6a;
        border: none;
        color: #ffffff;
        padding: 10px;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease;
        margin: 0 10px;
        font-size: 14px;
        font-weight: bold;
    }
    .month-navigation button:hover {
        background-color: #FF4D4D;
        color: #0E0E10;
        transform: scale(1.1);
    }
    #currentMonth {
        font-size: 18px;
        font-weight: bold;
        color: #ffffff;
    }
</style>

<body>
    <div class="right-container">
        <h1>Event Calendar</h1>
        <div class="month-navigation">
            <button id="prevMonthBtn">&lt;</button>
            <span id="currentMonth"></span>
            <button id="nextMonthBtn">&gt;</button>
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
    let currentPage = 1; // Default starting page for pagination

    // Declare all DOM elements at the top
    const calendar = document.getElementById('calendar');
    const eventDetails = document.getElementById('eventDetails');
    const selectedDateText = document.getElementById('selectedDate');
    const eventsOnDate = document.getElementById('eventsOnDate');
    const prevMonthBtn = document.getElementById('prevMonthBtn');
    const nextMonthBtn = document.getElementById('nextMonthBtn');
    const currentMonthText = document.getElementById('currentMonth');

    // Fetch events on page load
    document.addEventListener('DOMContentLoaded', async function () {
        await fetchAndDisplayEvents(currentPage);
    });

    // Function to fetch and display all events
    async function fetchAndDisplayEvents(page = 1) {
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

</body>
