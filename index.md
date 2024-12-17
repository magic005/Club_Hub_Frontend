---
layout: post
title: Flocker Social Media Site 
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
    .category {
        margin: 20px 0;
        padding: 15px;
        border: 2px solid #FF4B2B; /* Red border */
        border-radius: 8px;
        background: #2A2A2D;
        color: #F3F3F3;
    }
    .post {
        margin: 10px 0;
        padding: 15px;
        background: #121212;
        border: 2px solid #FF4B2B; /* Red border */
        border-radius: 5px;
        transition: background 0.3s;
    }
    .post:hover {
        background-color: #292929;
    }
    .form-container {
        margin: 20px 0;
        padding: 20px;
        border: 2px solid #FF4B2B; /* Red border */
        border-radius: 8px;
        background: #2A2A2D;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    }
    .form-container h2 {
        margin-bottom: 15px;
        color: #FF4D4D;
        text-align: center;
    }
    .form-container label {
        display: block;
        margin-bottom: 8px;
    }
    .form-container input,
    .form-container select,
    .form-container textarea {
        width: 100%;
        padding: 10px;
        margin-bottom: 15px;
        border: 1px solid #FF4B2B; /* Red border */
        border-radius: 5px;
        background: #121212;
        color: #F3F3F3;
    }
    .form-container button {
        padding: 15px;
        background: linear-gradient(to right, #FF416C, #FF4B2B);
        color: #fff;
        font-weight: bold;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: all 0.3s ease;
    }
    .form-container button:hover {
        background: linear-gradient(to right, #FF4B2B, #FF416C);
        transform: translateY(-2px);
    }
    .data {
        display: flex;
        margin: 20px 0;
        padding: 20px;
        background: #1A1A1D;
        border: 2px solid #FF4B2B; /* Red border */
        border-radius: 8px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    }
    .left-side {
        width: 50%;
        padding-right: 20px;
    }
    .details {
        width: 50%;
    }
    .chatroom-link {
        position: absolute;
        top: 640px;
        right: 460px;
        padding: 10px 15px;
        background: linear-gradient(to right, #FF416C, #FF4B2B);
        color: #fff;
        text-decoration: none;
        font-weight: bold;
        border-radius: 5px;
        transition: background 0.3s, transform 0.2s;
    }
    .chatroom-link:hover {
        background: linear-gradient(to right, #FF4B2B, #FF416C);
        transform: translateY(-2px);
    }
</style>

    </style>
</head>

<body>
    <div class="header">
        <h1>Welcome to Club Hub</h1>
        <p>Your platform for exploring extracurricular activities!</p>
    </div>
    <div class="container">
        <div class="category">
            <h2>Cyber Club</h2>
            <div class="post">
                <h3>Weekly Meeting Update</h3>
                <p>Join us every Monday at 4 PM in Room A101 to discuss upcoming events.</p>
            </div>
            <div class="post">
                <h3>New Competition Announced!</h3>
                <p>We're excited to announce that the next CyberPatriot competition will be held on January 25th. Prepare your teams!</p>
            </div>
             <div class="buttons">
        <button class="join-btn" onclick="showJoinForm(this, 'Cyber Club')">Join Club</button>
        <button class="leave-btn" onclick="leaveClub(this, 'Cyber Club')" style="display: none;">Leave Club</button>
    </div>
    <div class="join-form" style="display: none;">
        <h4>Enter Your Details</h4>
        <input type="text" placeholder="Your Name" class="user-name" required>
        <select class="user-role" required>
            <option value="" disabled selected>Select Role</option>
            <option value="President">President</option>
            <option value="Vice President">Vice President</option>
            <option value="Member">Member</option>
        </select>
        <button onclick="joinClub(this, 'Cyber Club')">Confirm Join</button>
    </div>
    <div class="members-list" style="margin-top: 10px;">
        <h4>Current Members:</h4>
        <ul></ul>
    </div>
        </div>
        <br>
        <div class="category">
            <h2>Robotics Club</h2>
            <div class="post">
                <h3>Weekly Meeting Update</h3>
                <p>Join us every Tuesday immediately after school in Room A107 (Mr. Campillo's) to discuss upcoming events and work on improving the robot.</p>
            </div>
            <div class="post">
                <h3>New Competition Announced!</h3>
                <p>We're excited to announce that the next FRC competition will be held on December 12th. Prepare your robots!</p>
            </div>
            <div class="buttons">
        <button class="join-btn" onclick="showJoinForm(this, 'Robotics Club')">Join Club</button>
        <button class="leave-btn" onclick="leaveClub(this, 'Robotics Club')" style="display: none;">Leave Club</button>
    </div>
    <div class="join-form" style="display: none;">
        <h4>Enter Your Details</h4>
        <input type="text" placeholder="Your Name" class="user-name" required>
        <select class="user-role" required>
            <option value="" disabled selected>Select Role</option>
            <option value="President">President</option>
            <option value="Vice President">Vice President</option>
            <option value="Member">Member</option>
        </select>
        <button onclick="joinClub(this, 'Cyber Club')">Confirm Join</button>
    </div>
    <div class="members-list" style="margin-top: 10px;">
        <h4>Current Members:</h4>
        <ul></ul>
            
<script> 
    function showJoinForm(button, clubName) {
    // Display the form for entering user details
    const parentDiv = button.parentElement.parentElement;
    const joinForm = parentDiv.querySelector('.join-form');
    joinForm.style.display = 'block';
    button.style.display = 'none'; // Hide the "Join Club" button
}
function joinClub(button, clubName) {
    // Get user details
    const parentDiv = button.parentElement.parentElement;
    const userName = parentDiv.querySelector('.user-name').value.trim();
    const userRole = parentDiv.querySelector('.user-role').value;
    if (userName && userRole) {
        // Add the user to the members list
        const membersList = parentDiv.querySelector('.members-list ul');
        const listItem = document.createElement('li');
        listItem.textContent = `${userName} (${userRole})`;
        membersList.appendChild(listItem);
        // Hide the form and show the "Leave Club" button
        const joinForm = parentDiv.querySelector('.join-form');
        joinForm.style.display = 'none';
        const leaveBtn = parentDiv.querySelector('.leave-btn');
        leaveBtn.style.display = 'inline-block';
    } else {
        alert('Please enter both your name and role!');
    }
}
function leaveClub(button, clubName) {
    const parentDiv = button.parentElement.parentElement;
    // Confirm leaving the club
    const confirmLeave = confirm(`Are you sure you want to leave ${clubName}?`);
    if (confirmLeave) {
        // Clear the members list and reset UI
        const membersList = parentDiv.querySelector('.members-list ul');
        membersList.innerHTML = '';
        const joinForm = parentDiv.querySelector('.join-form');
        joinForm.style.display = 'none';
        const joinBtn = parentDiv.querySelector('.join-btn');
        joinBtn.style.display = 'inline-block';
        button.style.display = 'none'; // Hide the "Leave Club" button
        alert(`You have left the ${clubName}.`);
    }
}
</script>
        </div>
        <!--<a href="{{site.baseurl}}/shared_interests/agk/agk-chatroom.html" class="chatroom-link">Join the currently available chatrooms!</a>-->
    </div>
    <div class="container">
        <div class="form-container">
            <h2>Select Group and Channel</h2>
            <form id="selectionForm">
                <label for="group_id">Group:</label>
                <select id="group_id" name="group_id" required>
                    <option value="">Select a group</option>
                </select>
                <label for="channel_id">Channel:</label>
                <select id="channel_id" name="channel_id" required>
                    <option value="">Select a channel</option>
                </select>
                <button type="submit">Select</button>
            </form>
        </div>
    </div>
    <div class="container">
        <div class="form-container">
            <h2>Add New Post</h2>
            <form id="postForm">
                <label for="title">Title:</label>
                <input type="text" id="title" name="title" required>
                <label for="comment">Comment:</label>
                <textarea id="comment" name="comment" required></textarea>
                <button type="submit">Add Post</button>
            </form>
        </div>
    </div>
    <div class="container">
        <div id="data" class="data">
            <div class="left-side">
                <p id="count"></p>
            </div>
            <div class="details" id="details">
            </div>
        </div>
    </div>
</body>
<script type="module">
    // Import server URI and standard fetch options
    import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';

    /**
     * Fetch groups for dropdown selection
     * User picks from dropdown
     */
    async function fetchGroups() {
        try {
            const response = await fetch(`${pythonURI}/api/groups/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ section_name: "Shared Interest" }) // Adjust the section name as needed
            });
            if (!response.ok) {
                throw new Error('Failed to fetch groups: ' + response.statusText);
            }
            const groups = await response.json();
            const groupSelect = document.getElementById('group_id');
            groups.forEach(group => {
                const option = document.createElement('option');
                option.value = group.name; // Use group name for payload
                option.textContent = group.name;
                groupSelect.appendChild(option);
            });
        } catch (error) {
            console.error('Error fetching groups:', error);
        }
    }

    /**
     * Fetch channels based on selected group
     * User picks from dropdown
     */
    async function fetchChannels(groupName) {
        try {
            const response = await fetch(`${pythonURI}/api/channels/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ group_name: groupName })
            });
            if (!response.ok) {
                throw new Error('Failed to fetch channels: ' + response.statusText);
            }
            const channels = await response.json();
            const channelSelect = document.getElementById('channel_id');
            channelSelect.innerHTML = '<option value="">Select a channel</option>'; // Reset channels
            channels.forEach(channel => {
                const option = document.createElement('option');
                option.value = channel.id;
                option.textContent = channel.name;
                channelSelect.appendChild(option);
            });
        } catch (error) {
            console.error('Error fetching channels:', error);
        }
    }

    /**
      * Handle group selection change
      * Channel Dropdown refresh to match group_id change
      */
    document.getElementById('group_id').addEventListener('change', function() {
        const groupName = this.value;
        if (groupName) {
            fetchChannels(groupName);
        } else {
            document.getElementById('channel_id').innerHTML = '<option value="">Select a channel</option>'; // Reset channels
        }
    });

    /**
     * Handle form submission for selection
     * Select Button: Computer fetches and displays posts
     */
    document.getElementById('selectionForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const groupId = document.getElementById('group_id').value;
        const channelId = document.getElementById('channel_id').value;
        if (groupId && channelId) {
            fetchData(channelId);
        } else {
            alert('Please select both group and channel.');
        }
    });

    /**
     * Handle form submission for adding a post
     * Add Form Button: Computer handles form submission with request
     */
    document.getElementById('postForm').addEventListener('submit', async function(event) {
        event.preventDefault();

        // Extract data from form
        const title = document.getElementById('title').value;
        const comment = document.getElementById('comment').value;
        const channelId = document.getElementById('channel_id').value;

        // Create API payload
        const postData = {
            title: title,
            comment: comment,
            channel_id: channelId
        };

        // Trap errors
        try {
            // Send POST request to backend, purpose is to write to database
            const response = await fetch(`${pythonURI}/api/post`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(postData)
            });

            if (!response.ok) {
                throw new Error('Failed to add post: ' + response.statusText);
            }

            // Successful post
            const result = await response.json();
            alert('Post added successfully!');
            document.getElementById('postForm').reset();
            fetchData(channelId);
        } catch (error) {
            // Present alert on error from backend
            console.error('Error adding post:', error);
            alert('Error adding post: ' + error.message);
        }
    });

    /**
     * Fetch posts based on selected channel
     * Handle response: Fetch and display posts
     */
    async function fetchData(channelId) {
        try {
            const response = await fetch(`${pythonURI}/api/posts/filter`, {
                ...fetchOptions,
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ channel_id: channelId })
            });
            if (!response.ok) {
                throw new Error('Failed to fetch posts: ' + response.statusText);
            }

            // Parse the JSON data
            const postData = await response.json();

            // Extract posts count
            const postCount = postData.length || 0;

            // Update the HTML elements with the data
            document.getElementById('count').innerHTML = `<h2>Count ${postCount}</h2>`;

            // Get the details div
            const detailsDiv = document.getElementById('details');
            detailsDiv.innerHTML = ''; // Clear previous posts

            // Iterate over the postData and create HTML elements for each item
            postData.forEach(postItem => {
                const postElement = document.createElement('div');
                postElement.className = 'post-item';
                postElement.innerHTML = `
                    <h3>${postItem.title}</h3>
                    <p><strong>Channel:</strong> ${postItem.channel_name}</p>
                    <p><strong>User:</strong> ${postItem.user_name}</p>
                    <p>${postItem.comment}</p>
                `;
                detailsDiv.appendChild(postElement);
            });

        } catch (error) {
            console.error('Error fetching data:', error);
        }
    }

    // Fetch groups when the page loads
    fetchGroups();
</script>




<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Club Hub Chatroom</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #FDF5E6;
        }
        .chatroom-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            border: 2px solid #360000;
            border-radius: 8px;
            background-color: #001F3F;
        }
        .chatroom-header {
            text-align: center;
            color: #ff4747;
        }
        .chat-area {
            height: 400px;
            overflow-y: auto;
            background-color: #404040;
            border: 2px solid #360000;
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 20px;
            color: white;
            display: flex;
            flex-direction: column;
        }
        .message {
            max-width: 80%;
            margin: 10px 0;
            padding: 10px;
            border-radius: 20px;
            position: relative;
        }
        .message.sent {
            background-color: #ffd700;
            color: black;
            align-self: flex-end;
        }
        .message-form {
            display: flex;
            align-items: center;
        }
        #messageInput {
            flex: 1;
            padding: 10px;
            border: 2px solid #360000;
            border-radius: 5px;
        }
        button {
            background-color: #FFD700;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #733f3f;
        }
        .chatroom-link {
            display: block;
            text-align: center;
            margin: 20px 0;
            padding: 10px;
            background-color: #1A2A6C;
            color: black;
            text-decoration: none;
            border-radius: 5px;
        }
        .chatroom-link:hover {
            background-color: #733f3f;
        }
        /* Styling for the Delete All button */
        .delete-btn {
            background-color: #ff4747;
            border: none;
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            margin-left: 10px;
        }
        .delete-btn:hover {
            background-color: #cc0000;
        }
    </style>
</head>
<body>

<script>
    const chatArea = document.getElementById('chatArea');
    const messageForm = document.getElementById('messageForm');
    const messageInput = document.getElementById('messageInput');

    // Load messages from localStorage
    function loadMessages() {
        const savedMessages = JSON.parse(localStorage.getItem('chatMessages')) || [];
        savedMessages.forEach((message, index) => addMessageToChat(message, index));
    }

    // Save messages to localStorage
    function saveMessages(messages) {
        localStorage.setItem('chatMessages', JSON.stringify(messages));
    }

    // Add a message to the chat area
    function addMessageToChat(message, index) {
        const messageElement = document.createElement('div');
        messageElement.classList.add('message', 'sent');
        messageElement.textContent = message.text;

        chatArea.appendChild(messageElement);
        chatArea.scrollTop = chatArea.scrollHeight; // Auto-scroll
    }

    // Handle form submission
    messageForm.addEventListener('submit', function (e) {
        e.preventDefault();
        const messageText = messageInput.value.trim();
        if (messageText !== "") {
            const messages = JSON.parse(localStorage.getItem('chatMessages')) || [];
            const newMessage = {
                text: messageText
            };
            messages.push(newMessage);
            saveMessages(messages);
            addMessageToChat(newMessage, messages.length - 1);
            messageInput.value = "";
        }
    });

    // Delete all messages
    function deleteAllMessages() {
        if (confirm("Are you sure you want to delete all messages?")) {
            localStorage.removeItem('chatMessages'); // Remove all messages from localStorage
            chatArea.innerHTML = ''; // Clear the chat area
        }
    }

    // Handle "Enter" key submission
    messageInput.addEventListener('keydown', function (e) {
        if (e.key === "Enter" && !e.shiftKey) {
            e.preventDefault(); // Prevent new line
            messageForm.requestSubmit(); // Trigger form submit
        }
    });

    // Initial load
    loadMessages();
</script>
</body>
</html>

---


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Club Creator</title>
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
            width: 50%;
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
    </style>
</head>
<body>
    <h1>Create a Club</h1>
    <button class="show-form-btn" id="showFormBtn">Start a New Club</button>
    <div class="form-container" id="formContainer">
        <h2>Club Registration Form</h2>
        <form id="clubForm">
            <div class="form-group">
                <label for="clubName">Club Name</label>
                <input type="text" id="clubName" placeholder="Enter club name" required>
            </div>
            <div class="form-group">
                <label for="clubDescription">Club Description</label>
                <input type="text" id="clubDescription" placeholder="Describe your club" required>
            </div>
            <div class="form-group">
                <label for="clubLeader">Club Leader Name</label>
                <input type="text" id="clubLeader" placeholder="Enter leader's name" required>
            </div>
            <button type="submit" class="submit-btn">Create Club</button>
        </form>
    </div>
    <div id="clubListContainer">
        <!-- New clubs will appear here -->
    </div>
    <script>
        const showFormBtn = document.getElementById('showFormBtn');
        const formContainer = document.getElementById('formContainer');
        const clubForm = document.getElementById('clubForm');
        const clubListContainer = document.getElementById('clubListContainer');
        // Show the form when the "Start a New Club" button is clicked
        showFormBtn.addEventListener('click', function () {
            formContainer.style.display = 'block';
        });
        // Handle form submission
        clubForm.addEventListener('submit', function (e) {
            e.preventDefault();
            // Get values from form inputs
            const clubName = document.getElementById('clubName').value.trim();
            const clubDescription = document.getElementById('clubDescription').value.trim();
            const clubLeader = document.getElementById('clubLeader').value.trim();
            if (clubName && clubDescription && clubLeader) {
                // Create a new club box
                const clubBox = document.createElement('div');
                clubBox.classList.add('club-box');
                // Set club details
                clubBox.innerHTML = `
                    <h3>${clubName}</h3>
                    <p><strong>Description:</strong> ${clubDescription}</p>
                    <p><strong>Leader:</strong> ${clubLeader}</p>
                `;
                // Append the new club box to the club list container
                clubListContainer.appendChild(clubBox);
                // Reset the form and hide it
                clubForm.reset();
                formContainer.style.display = 'none';
            } else {
                alert("Please fill out all fields!");
            }
        });
    </script>
</body>
</html>

---

<button class="navigate-btn" onclick="window.location.href='navigation/shared_interests/agk/chatroom1.html'">Go to Chatroom</button>
