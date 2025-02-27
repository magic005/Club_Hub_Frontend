---
layout: post
title: Discover
permalink: /discover
menu: nav/home.html
show_reading_time: false
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
        padding: 30px 20px;
        color: #fff;
        font-size: 1.5em;
    }
    .container {
        max-width: 900px;
        margin: 40px auto;
        padding: 20px;
        background: #1A1A1D;
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    }
    h1, h2 {
        text-align: center;
        font-weight: 700;
        color: #FF4D4D;
    }
    .quiz-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        margin-top: 20px;
    }
    .interest-item {
        width: 30%; /* Adjust for 3 columns */
        display: flex;
        align-items: center;
        margin-bottom: 15px;
    }
    .interest-item input {
        margin-right: 10px;
        cursor: pointer;
    }
    .interest-item label {
        font-size: 1.1em;
        cursor: pointer;
    }
    button {
        display: block;
        width: 100%;
        padding: 15px;
        margin-top: 20px;
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
        transform: translateY(-2px);
    }
    .results {
        margin-top: 20px;
        padding: 20px;
        background-color: #2A2A2D;
        border-radius: 8px;
    }
    .results {
    margin-top: 20px;
    padding: 20px;
    background-color: #2A2A2D;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    align-items: center; /* Centers content horizontally */
    justify-content: center; /* Centers content vertically */
    text-align: center; /* Ensures text alignment */
    }

    .results {
    margin: 20px auto; /* Centers horizontally */
    padding: 20px;
    background-color: #2A2A2D;
    border-radius: 8px;
    width: fit-content; /* Shrinks to the size of its content */
    text-align: center; /* Ensures text inside is centered */
    }

    .club-results {
    margin-top: 20px;
    padding: 20px;
    background-color: #2A2A2D;
    border-radius: 8px;
    text-align: center;
    }

    /* Centering and separating the club results container */
    .club-results {
        margin-top: 30px;
        padding: 25px;
        background-color: #1A1A1D; /* Ensures it matches the main container */
        border-radius: 10px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        text-align: center;
        max-width: 800px;
        margin-left: auto;
        margin-right: auto;
    }

    /* Ensure club cards are properly aligned */
    .clubs-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center; /* Centers the cards */
        gap: 20px;
    }

    /* Club card styling */
    .club-card {
        background: linear-gradient(135deg, #1E1E22, #25252B); /* Subtle gradient background */
        color: #F3F3F3;
        border-radius: 15px; /* Softer, more modern corners */
        padding: 30px;
        width: 500px; /* Adjusted width to make better use of space */
        min-height: 250px; /* Increased height for balance */
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4); /* Enhanced shadow for depth */
        transition: transform 0.3s ease, box-shadow 0.3s ease;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    /* Hover effect for interactivity */
    .club-card:hover {
        transform: translateY(-7px);
        box-shadow: 0 12px 30px rgba(0, 0, 0, 0.5);
    }

    /* Title styling with gradient text */
    .club-title {
        font-size: 1.8em; /* Bigger title */
        font-weight: bold;
        margin-bottom: 10px;
        background: linear-gradient(to right, #FF4B2B, #FF416C);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }

    /* Description styling */
    .club-description {
        font-size: 1.2em; /* Slightly larger text for readability */
        color: #D1D1D1; /* Softer white for less contrast strain */
        margin-bottom: 15px;
        text-align: center;
        line-height: 1.5;
        max-width: 90%;
    }

    /* Founder text with slight emphasis */
    .club-founder {
        font-size: 1em;
        color: #AAAAAA; /* Muted color to keep focus on title and description */
        font-style: italic;
    }

    /* Adjust No Match Message */
    /* No Matches Container */
    .no-matches-container {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 20px;
    }

    /* Styling for "No Clubs Match" Message */
    .no-matches {
        text-align: center;
        font-size: 1.2em;
        background: linear-gradient(to right, #FF4B2B, #FF416C);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        padding: 25px;
        border-radius: 12px;
        width: 500px; /* Matches club cards */
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
        font-weight: bold;
    }

    /* Matched Interest Count */
    .matched-interests {
        font-size: 1em;
        color: #BBBBBB;
        margin-top: 10px;
        font-style: italic;
    }

    /* Ensure consistent spacing */
    .clubs-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 20px;
        margin-top: 20px;
    }
</style>


<div class="header">
    <h1>Discover Your Interests</h1>
    <p>Select the topics that excite you the most!</p>
</div>

<div class="container">
    <h2>Choose Your Interests</h2>
    <form id="quiz-form">
        <div class="quiz-container">
        
<!-- Interest items -->
<div class="interest-item">
    <input type="checkbox" id="interest1" name="interests" value="Cybersecurity">
    <label for="interest1">Cybersecurity</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest2" name="interests" value="Robotics">
    <label for="interest2">Robotics</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest3" name="interests" value="Artificial Intelligence">
    <label for="interest3">Artificial Intelligence</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest4" name="interests" value="Photography">
    <label for="interest4">Photography</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest5" name="interests" value="Space Exploration">
    <label for="interest5">Space Exploration</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest6" name="interests" value="Gaming">
    <label for="interest6">Gaming</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest7" name="interests" value="Programming">
    <label for="interest7">Programming</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest8" name="interests" value="Machine Learning">
    <label for="interest8">Machine Learning</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest9" name="interests" value="Blockchain">
    <label for="interest9">Blockchain</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest10" name="interests" value="Music">
    <label for="interest10">Music</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest11" name="interests" value="Art">
    <label for="interest11">Art</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest12" name="interests" value="Fitness">
    <label for="interest12">Fitness</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest13" name="interests" value="Cooking">
    <label for="interest13">Cooking</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest14" name="interests" value="Travel">
    <label for="interest14">Travel</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest15" name="interests" value="Languages">
    <label for="interest15">Languages</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest16" name="interests" value="Entrepreneurship">
    <label for="interest16">Entrepreneurship</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest17" name="interests" value="Finance">
    <label for="interest17">Finance</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest18" name="interests" value="Astronomy">
    <label for="interest18">Astronomy</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest19" name="interests" value="Cars">
    <label for="interest19">Cars</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest20" name="interests" value="Literature">
    <label for="interest20">Literature</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest21" name="interests" value="Psychology">
    <label for="interest21">Psychology</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest22" name="interests" value="History">
    <label for="interest22">History</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest23" name="interests" value="Mathematics">
    <label for="interest23">Mathematics</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest24" name="interests" value="Biology">
    <label for="interest24">Biology</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest25" name="interests" value="Chemistry">
    <label for="interest25">Chemistry</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest26" name="interests" value="Physics">
    <label for="interest26">Physics</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest27" name="interests" value="Teaching">
    <label for="interest27">Teaching</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest28" name="interests" value="Volunteering">
    <label for="interest28">Volunteering</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest29" name="interests" value="Fashion">
    <label for="interest29">Fashion</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest30" name="interests" value="Fundraising">
    <label for="interest30">Fundraising</label>
</div>

<button type="button" onclick="showResults()">Submit Interests</button>

<div id="results" class="results" style="display: none;">
    <h3>Your Selected Interests:</h3>
    <p id="selectedInterests">None selected yet.</p>
</div>

<div id="club-results" class="club-results" style="display: none;">
    <h3>Clubs For You:</h3>
    <div id="clubs-container" class="clubs-container"></div>
</div>



<!--<script>
    function showResults() {
        const form = document.forms['quiz-form'];
        const selected = [];
        const checkboxes = form['interests'];
        checkboxes.forEach(checkbox => {
            if (checkbox.checked) selected.push(checkbox.value);
        });
        document.getElementById('selectedInterests').innerText = selected.length > 0 ? selected.join(', ') : 'No interests selected.';
        document.getElementById('results').style.display = 'block';
    }
</script>-->


<script type="module">
import { pythonURI } from "{{site.baseurl}}/assets/js/api/config.js";
// simulate getting a token from the storage thingy
function getToken() {
    return localStorage.getItem('token') || 'Bearer MOCK_TOKEN';
}
// submit interests
    async function submitInterests() {
        const form = document.forms['quiz-form'];
        const selected = [];
        const checkboxes = form.querySelectorAll('input[type="checkbox"]:checked');
        // collect selected interests
        checkboxes.forEach(checkbox => {
            selected.push(checkbox.value);
        });
        if (selected.length === 0) {
            alert('Please select at least one interest!');
            return;
        }
        try {
            const URL = `${pythonURI}/api/interests`;
            const response = await fetch(URL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': getToken(), // token
                },
                body: JSON.stringify({ interests: selected })
            });
            if (!response.ok) throw new Error('Failed to submit interests');
            alert('Interests saved successfully!');
            fetchAndDisplayInterests(); // refresh
        } catch (error) {
            console.error('Error submitting interests:', error);
            alert('Error submitting interests.');
        }
    }
    // fetch and display Interests
    async function fetchAndDisplayInterests() {
        try {
            const URL = `${pythonURI}/api/interests`;
            const response = await fetch(URL, {
                method: 'GET',
                headers: { 'Authorization': getToken() },
            });
            if (!response.ok) throw new Error('Failed to fetch interests');
            const data = await response.json();
            const interestsElement = document.getElementById('selectedInterests');
            if (data.interests.length > 0) {
                interestsElement.innerText = `Saved Interests: ${data.interests.join(', ')}`;
            } else {
                interestsElement.innerText = 'No interests saved yet.';
            }
            // show the results div
            document.getElementById('results').style.display = 'block';
        } catch (error) {
            console.error('Error fetching interests:', error);
            alert('Error fetching interests.');
        }
    }
    function showResults() {
        submitInterests(); // Submit interests first

        // Get selected interests after submission
        const form = document.forms['quiz-form'];
        const selectedInterests = Array.from(form.querySelectorAll('input[type="checkbox"]:checked'))
            .map(checkbox => checkbox.value);

        if (selectedInterests.length > 0) {
            fetchAndDisplayClubs(selectedInterests);
        }
    }
    // attach to submit
    const submitButton = document.getElementById('submitInterestsButton');
    if (submitButton) {
        submitButton.addEventListener('click', submitInterests);
    }

    // Function to fetch clubs and filter them based on selected interests
    async function fetchAndDisplayClubs(userInterests) {
        try {
            const URL = `${pythonURI}/api/club`; // API to fetch clubs
            const response = await fetch(URL, {
                method: 'GET',
                headers: { 'Authorization': getToken() },
            });

            if (!response.ok) throw new Error('Failed to fetch clubs');

            const clubs = await response.json();
            const clubsContainer = document.getElementById('clubs-container');
            clubsContainer.innerHTML = ''; // Clear previous results

            // Process and sort clubs by number of matching interests
            const matchedClubs = clubs.map(club => {
                const matchCount = club.topics.filter(topic => userInterests.includes(topic)).length;
                return { ...club, matchCount }; // Store match count
            }).filter(club => club.matchCount > 0) // Only show clubs that match at least 1 interest
            .sort((a, b) => b.matchCount - a.matchCount); // Sort by most matches

            if (matchedClubs.length > 0) {
                matchedClubs.forEach(club => {
                    const clubCard = document.createElement('div');
                    clubCard.classList.add('club-card');
                    clubCard.innerHTML = `
                        <div class="club-title">${club.name}</div>
                        <div class="club-description">${club.description}</div>
                        <div class="club-founder">Founded by: ${club.user_id}</div>
                        <div class="matched-interests">Matches ${club.matchCount} of your interests</div>
                    `;
                    clubsContainer.appendChild(clubCard);
                });
                document.getElementById('club-results').style.display = 'block';
            } else {
                clubsContainer.innerHTML = `<div class="no-matches">No clubs match your interests. Try selecting more!</div>`;
                document.getElementById('club-results').style.display = 'block';
            }
        } catch (error) {
            console.error('Error fetching clubs:', error);
            alert('Error fetching clubs.');
        }
    }

    window.onload = async function () {
        await fetchAndDisplayInterests();
        
        // Fetch the saved interests first, then pass them into fetchAndDisplayClubs
        try {
            const URL = `${pythonURI}/api/interests`;
            const response = await fetch(URL, {
                method: 'GET',
                headers: { 'Authorization': getToken() },
            });

            if (response.ok) {
                const data = await response.json();
                fetchAndDisplayClubs(data.interests || []); // Use saved interests
            } else {
                console.error('Failed to fetch saved interests');
            }
        } catch (error) {
            console.error('Error fetching saved interests:', error);
        }
    };

    window.showResults = showResults;
</script>