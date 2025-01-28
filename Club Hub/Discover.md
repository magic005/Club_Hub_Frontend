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
    <label for="interest1">Cyber</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest2" name="interests" value="Robotics">
    <label for="interest2">Robots</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest3" name="interests" value="Artificial Intelligence">
    <label for="interest3">AI</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest4" name="interests" value="Photography">
    <label for="interest4">Photos</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest5" name="interests" value="Space Exploration">
    <label for="interest5">Space</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest6" name="interests" value="Gaming">
    <label for="interest6">Games</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest7" name="interests" value="Programming">
    <label for="interest7">Code</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest8" name="interests" value="Machine Learning">
    <label for="interest8">ML</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest9" name="interests" value="Blockchain">
    <label for="interest9">Chain</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest10" name="interests" value="Music">
    <label for="interest10">Music</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest11" name="interests" value="Art">
    <label for="interest11">Arts</label>
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
    <label for="interest15">Language</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest16" name="interests" value="Entrepreneurship">
    <label for="interest16">Business</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest17" name="interests" value="Finance">
    <label for="interest17">Finance</label>
</div>

<div class="interest-item">
    <input type="checkbox" id="interest18" name="interests" value="Astronomy">
    <label for="interest18">Stars</label>
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
    <label for="interest23">Math</label>
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
        submitInterests(); // submitInterests when showResults
    }
    // attach to submit
    const submitButton = document.getElementById('submitInterestsButton');
    if (submitButton) {
        submitButton.addEventListener('click', submitInterests);
    }
    window.onload = fetchAndDisplayInterests;
    window.showResults = showResults;
</script>














