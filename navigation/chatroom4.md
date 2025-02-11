---
layout: post
title: Club Hub Gemini Integration
permalink: /chatroom4
menu: nav/home.html
show_reading_time: false
---

<div id="output"></div>


<script type="module">
    import { pythonURI, fetchOptions } from '/Club_Hub_Frontend/assets/js/api/config.js';
    async function fetchStudentData() {
            try {
                // Make the GET request to the '/student/clubs' endpoint
                const response = await fetch(`${pythonURI}/api/club1/clubs`);
                if (!response.ok) {
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }

                // Parse the JSON response
                const data = await response.json();

                // Display the data on the webpage
                const outputDiv = document.getElementById('output');
                outputDiv.innerHTML = `
                    <p><strong>Club Name:</strong> ${data.ClubName}</p>
                    <p><strong>President:</strong> ${data.President}</p>
                    <p><strong>Members Count:</strong> ${data.MembersCount}</p>
                    <p><strong>Email:</strong> ${data.Email}</p>
                    <p><strong>Location:</strong> ${data.Location}</p>
                `;
            } catch (error) {
                console.error('Error fetching student data:', error);
            }
        }

        // Call the function to fetch data
        fetchStudentData();
</script>


