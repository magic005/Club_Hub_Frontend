---
layout: post
title: Club Hub
search_exclude: true
description: Login and explore our social media hub for everything DNHS 
hide: true
menu: nav/home.html
---

<style>
    /* Event Section - Bigger and More Central */
    .event-container {
        max-width: 1100px;
        margin: 60px auto;
        padding: 50px;
        background: #1A1A1D;
        border-radius: 20px;
        box-shadow: 0 12px 40px rgba(0, 0, 0, 0.5);
        text-align: center;
    }

    /* Event Header - Bold and Eye-Catching */
    /* Gradient Header */
    /* Stronger Gradient Header */
    .event-container h2 {
        font-size: 2.5em;
        font-weight: bold;
        background: linear-gradient(to left, #ff802b, #FF5577);
        -webkit-text-fill-color: transparent; 
        -webkit-background-clip: text;
        text-align: center;
        margin-bottom: 35px;
    }

    /* Event Cards - Bigger, More Padding, More Presence */
    .event-card {
        background: linear-gradient(135deg, #2E2E33, #1E1E22);
        border-radius: 20px;
        padding: 45px;
        margin: 50px auto;
        box-shadow: 0 14px 35px rgba(0, 0, 0, 0.5);
        transition: transform 0.3s ease, box-shadow 0.3s ease;
        max-width: 1000px;
        text-align: left;
        min-height: 250px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        position: relative;
        border: 4px solid transparent; /* Make room for the border */
        background-clip: padding-box; /* Ensures inner part stays clean */
    }

    /* Gradient Border Fix */
    .event-card::before {
        content: "";
        position: absolute;
        inset: 0;
        border-radius: 20px;
        padding: 4px; /* Border thickness */
        background: linear-gradient(to right, #FF4B2B, #FF416C); /* Proper deep gradient */
        -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        -webkit-mask-composite: destination-out;
        mask-composite: exclude;
        pointer-events: none;
    }

    /* Hover Effect - Slight Lift */
    .event-card:hover {
        transform: translateY(-7px);
        box-shadow: 0 18px 40px rgba(0, 0, 0, 0.6);
    }

    /* Event Title - FIXED Gradient Text */
    .event-title {
        font-size: 2em;
        font-weight: bold;
        background: linear-gradient(to right, #ffffff, #000000);
        -webkit-text-fill-color: transparent; 
        -webkit-background-clip: text;
        margin-bottom: 20px;
    }

    /* Event Description - More Readable */
    .event-description {
        font-size: 1.3em;
        color: #EAEAEA;
        margin-top: 10px;
        line-height: 1.6;
    }

    /* Event Date - More Prominent */
    .event-date {
        font-size: 1.1em;
        color: #BBBBBB;
        font-style: italic;
        margin-top: 20px;
        display: flex;
        align-items: center;
        gap: 8px;
    }

    /* Date Icon */
    .event-date::before {
        content: "📅";
        font-size: 1.2em;
    }
</style>

<body>
    <div class="header">
        Welcome to Club Hub
        <p>Your platform for exploring extracurricular activities!</p>
    </div>

    <!-- Event Section -->
<div class="event-container">
    <h2>Upcoming Club Events</h2>
    <div id="event-list"></div> <!-- All club events will be inserted here -->
</div>
</body>

<script type="module">
    import { pythonURI } from '{{ site.baseurl }}/assets/js/api/config.js';

    function getToken() {
        return localStorage.getItem('token') || 'Bearer MOCK_TOKEN';
    }

    // Function to Fetch and Display Events
    async function fetchAndDisplayEvents() {
        try {
            const URL = `${pythonURI}/api/events`; // Adjust endpoint if necessary
            const response = await fetch(URL, {
                method: 'GET',
                headers: { 'Authorization': getToken() },
            });

            if (!response.ok) throw new Error('Failed to fetch events');

            const events = await response.json();
            const eventList = document.getElementById('event-list');
            eventList.innerHTML = ''; // Clear previous events

            if (events.length > 0) {
                events.forEach(event => {
                    const eventCard = document.createElement('div');
                    eventCard.classList.add('event-card');
                    eventCard.innerHTML = `
                        <div class="event-title">${event.title}</div>
                        <div class="event-description">${event.description}</div>
                        <div class="event-date">📅 Date: ${event.date}</div>
                    `;
                    eventList.appendChild(eventCard);
                });
            } else {
                eventList.innerHTML = "<p>No upcoming events.</p>";
            }
        } catch (error) {
            console.error('Error fetching events:', error);
            document.getElementById('event-list').innerHTML = "<p>Error loading events.</p>";
        }
    }

    // Load events on page load
    window.onload = function () {
        fetchAndDisplayEvents();
    };
</script>