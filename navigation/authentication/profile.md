---
layout: post
title: Profile Settings
permalink: /profile
menu: nav/home.html
search_exclude: true
show_reading_time: false
---


<div class="profile-container">
    <div class="card">
        <form id="profileForm">
            <div>
                <label for="newUid">Enter New UID:</label>
                <input type="text" id="newUid" name="uid" placeholder="New UID">
            </div>
            <div>
                <label for="newName">Enter New Name:</label>
                <input type="text" id="newName" name="name" placeholder="New Name">
            </div>
            <div>
                <label for="newPassword">Enter New Password:</label>
                <input type="password" id="newPassword" name="password" placeholder="New Password">
            </div>
            <div>
                <label for="newBio">Enter Bio:</label>
                <input type="text" id="newBio" name="bio" placeholder="Enter Bio">
            </div>
            <br>
            <label for="profilePicture" class="file-icon"> Upload Profile Picture <i class="fas fa-upload"></i></label>
            <input type="file" id="profilePicture" accept="image/*">
            <div class="image-container" id="profileImageBox"></div>
            <p id="profile-message" style="color: red;"></p>
            <br>

            <button type="submit" id="submitProfile" 
                style="width: 100%; padding: 15px; background: linear-gradient(to right, #FF4B2B, #FF416C);
                color: white; font-size: 1.2em; font-weight: bold; border: none; border-radius: 8px; 
                cursor: pointer; transition: background 0.3s ease, transform 0.2s ease;">
                Submit
            </button>
        </form>

        <div id="profileDisplay" style="display: none; margin-top: 20px; border: 2px solid blue; padding: 20px; display: flex; align-items: center;">
            <div style="flex-grow: 1;">
                <h3>Your Profile</h3>
                <div id="bioBox">
                    <p><strong>Bio:</strong> <span id="bioText"></span></p>
                    <p><strong>Name:</strong> <span id="nameText"></span></p>
                    <p><strong>UID:</strong> <span id="uidText"></span></p>
                </div>
            </div>
            <div id="profileImageBox" style="margin-left: 20px;">
                <img id="profileImage" src="{{ url_for('uploaded_file', filename='profile_picture.png') }}" 
                     alt="Profile Picture" style="max-width: 150px; border-radius: 10px;">
            </div>
        </div>
    </div>
</div>


<script type="module">
// Import fetchOptions and necessary functions from external files
import { pythonURI, fetchOptions } from '{{site.baseurl}}/assets/js/api/config.js';
import { putUpdate } from "{{site.baseurl}}/assets/js/api/profile.js";

// Handle form submission
document.getElementById('profileForm').addEventListener('submit', async function (e) {
    e.preventDefault(); // Prevent default form submission behavior

    // Gather form data
    const uid = document.getElementById('newUid').value;
    const name = document.getElementById('newName').value;
    const password = document.getElementById('newPassword').value;
    const bio = document.getElementById('newBio').value;
    const profilePictureInput = document.getElementById('profilePicture');
    let profilePicture = null;

    if (profilePictureInput.files.length > 0) {
        profilePicture = await convertToBase64(profilePictureInput.files[0]);
    }

    // Create payload to send to backend
    const payload = {
        uid,
        name,
        password,
        bio,
        profilePicture,
    };

    console.log('Submitting form data:', payload); // Debugging

    // Send data to the backend
    try {
        const URL = pythonURI + "/api/user/profile"; // Adjust this endpoint as per your backend
        const options = {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(payload),
        };

        const response = await fetch(URL, options);
        if (response.ok) {
            const result = await response.json();
            console.log('Profile updated successfully:', result);
                // Store in localStorage
            localStorage.setItem('bio', bio);
            localStorage.setItem('name', name);
            localStorage.setItem('uid', uid);
            if (profilePicture) {
              localStorage.setItem('profilePicture', `data:image/png;base64,${profilePicture}`);
            }
            document.getElementById('profile-message').textContent = 'Profile updated successfully!';
            document.getElementById('bioText').textContent = bio;
            document.getElementById('nameText').textContent = name;
            document.getElementById('uidText').textContent = uid;
            if (profilePicture) {
                const profileImage = document.getElementById('profileImage');
                profileImage.src = `data:image/png;base64,${profilePicture}`; // Assuming base64 image
            }

            document.getElementById('profileDisplay').style.display = 'block'; // Show profile section
            document.getElementById('profile-message').textContent = 'Profile updated successfully!';
        } else {
            const error = await response.json();
            console.error('Error updating profile:', error);
            document.getElementById('profile-message').textContent = error.message || 'Failed to update profile.';
        }
    } catch (error) {
        console.error('Error:', error.message);
        document.getElementById('profile-message').textContent = 'Error submitting profile: ' + error.message;
    }
});

// Function to convert file to base64
async function convertToBase64(file) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result.split(',')[1]); // Remove the prefix
        reader.onerror = error => reject(error);
        reader.readAsDataURL(file);
    });
}

async function fetchProfilePicture() {
    const token = localStorage.getItem('token'); // Get token from localStorage

    if (!token) {
        console.log('User not logged in');
        return;
    }

    try {
        const response = await fetch('/api/id', {
            method: 'GET',
            headers: {
                'Authorization': `Bearer ${token}`,
                'Content-Type': 'application/json',
            }
        });

        if (!response.ok) {
            throw new Error("Failed to fetch user data.");
        }

        const data = await response.json();
        console.log('User UID:', data.uid);  // Log the UID
        // You can now use the `uid` or display the user info
    } catch (error) {
        console.error("Error fetching profile picture:", error);
    }
}

fetchProfilePicture();

function loadProfileFromLocalStorage() {
    const storedBio = localStorage.getItem('bio');
    const storedName = localStorage.getItem('name');
    const storedUid = localStorage.getItem('uid');
    const storedProfilePicture = localStorage.getItem('profilePicture');

    if (storedBio) {
        document.getElementById('bioText').textContent = storedBio;
    }
    if (storedName) {
        document.getElementById('nameText').textContent = storedName;
    }
    if (storedUid) {
        document.getElementById('uidText').textContent = storedUid;
    }
    if (storedProfilePicture) {
        document.getElementById('profileImage').src = storedProfilePicture;
    }

    // Show the profile section if data is found
    if (storedBio || storedName || storedUid || storedProfilePicture) {
        document.getElementById('profileDisplay').style.display = 'block';
    }
}

// Call the function on page load
document.addEventListener('DOMContentLoaded', loadProfileFromLocalStorage);

</script>

