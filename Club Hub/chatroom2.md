---
layout: post
title: Club Hub Gemini Integration
permalink: /chatroom2
menu: nav/home.html
show_reading_time: false
---


<button class="navigate-btn" onclick="window.location.href='navigation/shared_interests/agk/chatroom1.html'">Chatroom<button>

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #e69650;
    }
    .chatroom-container {
        max-width: 600px;
        margin: 0 auto;
        padding: 20px;
        border: 2px solid #360000;
        border-radius: 8px;
        background-color: #A9A9A9;
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
        flex-direction: column; /* Align messages vertically */
    }
    .message {
        max-width: 80%;
        margin: 10px 0;
        padding: 10px;
        border-radius: 20px;
        position: relative;
    }
    .message.sent {
        background-color: #FFFFFF;
        color: black;
        align-self: flex-end;
        position: relative;
    }
    .message.received {
        background-color: #0077BE;
        color: white;
        align-self: flex-start;
        position: relative;
    }
    .message-form {
        display: flex;
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
</style>

<div class="chatroom-container">
    <header class="chatroom-header">
        <h1>Activity Chatroom</h1>
        <p>Discuss your favorite activities!</p>
    </header>
    <div class="chat-area" id="chatArea">
        <!-- Messages will appear here -->
    </div>
    <form class="message-form" id="messageForm">
        <input type="text" id="messageInput" placeholder="Enter your message..." required>
        <button type="submit">Send</button>
    </form>
    <a href="#" class="chatroom-link">Back to Home</a>
    <div id="output"></div>
</div>

<script type="module">
    import { pythonURI, fetchOptions } from '/Club_Hub_Frontend/assets/js/api/config.js';
    const chatArea = document.getElementById('chatArea');
    const messageForm = document.getElementById('messageForm');
    const messageInput = document.getElementById('messageInput');
    const apiBaseURL = location.hostname === "localhost" || location.hostname === "127.0.0.1"
        ? "http://127.0.0.1:8887"
        : "https://flocker.nighthawkcodingsociety.com";

    let messages = [];
    messageForm.addEventListener('submit', async function (e) {
        e.preventDefault();

        const userMessage = messageInput.value.trim();
        if (!userMessage) return;

        // Display user message
        displayMessage(userMessage, "sent");
        //messages.push([userMessage, "sent"]);

        try {
            // Send message to the backend
            const response = await fetch(`${apiBaseURL}/api/ai/help`, {
            //const response = await fetch(`https://flocker.nighthawkcodingsociety.com/api/ai/help`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({ question: userMessage }),
            });

            const data = await response.json();

            // Handle AI response
            const aiMessage = data.response || "Sorry, I couldn't understand that.";
            //const aiMessage = data.response || JSON.stringify(data);
            displayMessage(aiMessage, "received");
            //messages.push([aiMessage, "received"]);
        } catch (error) {
            console.error("Error communicating with the server:", error);
            displayMessage("Error: Unable to connect to the server.", "received");
        } finally {
            messageInput.value = "";
            chatArea.scrollTop = chatArea.scrollHeight; // Auto-scroll to the newest message
            //displayMessages();
        }
    });
/*
    function displayMessages() {
        //console.log(messages);
        // loop over messages and czll displayMemssage


  } */
    function displayMessage(text, type) {
        makePost(text);
        const messageElement = document.createElement('div');
        messageElement.classList.add('message', type);
        messageElement.textContent = text;
        chatArea.appendChild(messageElement);
    }

    async function makePost(message) {
            const postTitle = 'Post';
            const postComment = message;
            const postChannelId = 1;

            const postData = {
                title: postTitle,
                comment: postComment,
                channel_id: postChannelId
            };

            try {
                const response = await fetch(`${pythonURI}/api/post`, {
                    ...fetchOptions,
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(postData)
                });

                if (!response.ok) {
                    throw new Error('Failed to add channel: ' + response.statusText);
                }
            } catch (error) {
                console.error('Error adding channel:', error);
                alert('Error adding channel: ' + error.message);
            }    
    }
</script>

