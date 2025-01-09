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
</style>

<body>
    <div class="header">
        Welcome to Club Hub
        <p>Your platform for exploring extracurricular activities!</p>
    </div>

<div class="container">
    <h2>Cyber Club</h2>
    <div class="category">
        <div class="post">
            <h3>Weekly Meeting Update</h3>
            <p>Join us every Monday at 4 PM in Room A101 to discuss upcoming events.</p>
        </div>
        <div class="post">
            <h3>New Competition Announced!</h3>
            <p>We're excited to announce that the next CyberPatriot competition will be held on January 25th. Prepare your teams!</p>
        </div>
    </div>
    <h2>Robotics Club</h2>
    <div class="category">
        <div class="post">
            <h3>Weekly Meeting Update</h3>
            <p>Join us every Tuesday immediately after school in Room A107 to work on the robot.</p>
        </div>
        <div class="post">
            <h3>New Competition Announced!</h3>
            <p>We're excited to announce that the next FRC competition will be held on December 12th. Prepare your robots!</p>
        </div>
    </div>
</div>

<div class="container form-container">
    <h2>Add New Post</h2>
    <form id="postForm">
        <label for="title">Title:</label>
        <input type="text" id="title" name="title" required>
        <label for="comment">Comment:</label>
        <textarea id="comment" name="comment" rows="4" required></textarea>
        <button type="submit">Add Post</button>
    </form>
</div>

<div class="container form-container">
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

<h1>Create a Club</h1>
<button class="show-form-btn" id="showFormBtn">Start a New Club</button>
<div class="form-container" id="formContainer" style="display:none;">
    <h2>Club Registration Form</h2>
    <form id="clubForm">
        <label for="clubName">Club Name</label>
        <input type="text" id="clubName" placeholder="Enter club name" required>
        <label for="clubDescription">Club Description</label>
        <input type="text" id="clubDescription" placeholder="Describe your club" required>
        <label for="clubLeader">Club Leader Name</label>
        <input type="text" id="clubLeader" placeholder="Enter leader's name" required>
        <button type="submit" class="submit-btn">Create Club</button>
    </form>
</div>
<div id="clubListContainer"></div>
</body>




<script type="module">
    // Import server URI and standard fetch options
    import { pythonURI, fetchOptions } from '{{ site.baseurl }}/assets/js/api/config.js';
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
document.getElementById('group_id').addEventListener('change', function() {
    const groupName = this.value;
    if (groupName) {
        fetchChannels(groupName);
    } else {
        document.getElementById('channel_id').innerHTML = '<option value="">Select a channel</option>'; // Reset channels
    }
});
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
document.getElementById('postForm').addEventListener('submit', async function(event) {
    event.preventDefault();
    const title = document.getElementById('title').value;
    const comment = document.getElementById('comment').value;
    const channelId = document.getElementById('channel_id').value;
    const postData = {
        title: title,
        comment: comment,
        channel_id: channelId
    };
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
fetchGroups();
</script>


<button class="navigate-btn" onclick="window.location.href='navigation/shared_interests/agk/chatroom1.html'">Go to Chatroom</button>
