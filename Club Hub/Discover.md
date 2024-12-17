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
            margin-top: 20px;
        }
        .interest-item {
            display: flex;
            align-items: center;
            padding: 10px 15px;
            border-bottom: 1px solid #333;
            cursor: pointer;
        }
        .interest-item input {
            margin-right: 15px;
            cursor: pointer;
        }
        .interest-item label {
            font-size: 1.1em;
            flex-grow: 1;
            cursor: pointer;
        }
        .interest-item:hover {
            background-color: #292929;
            border-radius: 5px;
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
        .results p {
            font-size: 1.1em;
            color: #F3F3F3;
        }
    </style>

<body>
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
            <!-- Add up to 25 interests in similar fashion -->
        </div>
        <button type="button" onclick="showResults()">Submit Interests</button>
    </form>
    <div id="results" class="results" style="display: none;">
        <h3>Your Selected Interests:</h3>
        <p id="selectedInterests">None selected yet.</p>
    </div>
</div>

<script>
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
</script>
</body>