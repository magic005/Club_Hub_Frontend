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
     <!-- Submit Button -->
     <button type="submit" id="submitProfile">Submit</button>
   </form>
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
</script>
// testing