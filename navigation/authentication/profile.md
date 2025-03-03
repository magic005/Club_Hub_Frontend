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
                <label for="newBio">Enter Bio:</label>
                <input type="text" id="newBio" name="bio" placeholder="Enter Bio">
            </div>
            <br>
            
            <!-- Custom File Upload Button -->
            <label class="file-upload-btn">
                <input type="file" id="profilePicture" accept="image/*" hidden>
                <span id="uploadText">Upload Profile Picture</span>
            </label>
            <span id="fileName" style="margin-left: 10px; font-style: italic;"></span>

            <br><br>
            <button type="submit" id="submitProfile">Submit</button>
        </form>

        <div id="profilesContainer" style="margin-top: 20px;"></div>
    </div>
</div>

<style>
    .file-upload-btn {
        display: inline-block;
        background:rgb(255, 0, 85);
        color: white;
        padding: 10px 15px;
        border-radius: 5px;
        cursor: pointer;
        text-align: center;
    }
    .file-upload-btn:hover {
        background: #0056b3;
    }
</style>

<script>
document.getElementById('profilePicture').addEventListener('change', function () {
    const fileName = this.files.length > 0 ? this.files[0].name : "No file chosen";
    document.getElementById('fileName').textContent = fileName;
});

document.getElementById('profileForm').addEventListener('submit', async function (e) {
    e.preventDefault();

    const uid = document.getElementById('newUid').value.trim();
    const name = document.getElementById('newName').value.trim();
    const bio = document.getElementById('newBio').value.trim();
    const profilePictureInput = document.getElementById('profilePicture');

    if (!uid || !name || !bio) {
        alert("Please fill in all fields.");
        return;
    }

    let profiles = JSON.parse(localStorage.getItem('profiles')) || [];

    let existingProfile = profiles.find(profile => profile.uid === uid);
    if (existingProfile) {
        if (profilePictureInput.files.length > 0) {
            const imageBase64 = await convertToBase64(profilePictureInput.files[0]);
            existingProfile.images.push(imageBase64);
        }
    } else {
        let profilePictures = [];
        if (profilePictureInput.files.length > 0) {
            const imageBase64 = await convertToBase64(profilePictureInput.files[0]);
            profilePictures.push(imageBase64);
        }
        profiles.push({ uid, name, bio, images: profilePictures });
    }

    localStorage.setItem('profiles', JSON.stringify(profiles));
    loadProfiles();
});

function loadProfiles() {
    const profilesContainer = document.getElementById('profilesContainer');
    profilesContainer.innerHTML = '';

    let profiles = JSON.parse(localStorage.getItem('profiles')) || [];

    profiles.forEach((profile, index) => {
        const profileCard = document.createElement('div');
        profileCard.style = 'display: flex; align-items: center; border: 2px solid red; padding: 10px; margin-bottom: 10px;';

        // Profile Text
        const textContainer = document.createElement('div');
        textContainer.style = 'flex-grow: 1; margin-right: 20px;';
        textContainer.innerHTML = `
            <p><strong>UID:</strong> ${profile.uid}</p>
            <p><strong>Name:</strong> ${profile.name}</p>
            <p><strong>Bio:</strong> ${profile.bio}</p>
        `;

        // Images
        const imageContainer = document.createElement('div');
        imageContainer.style = 'display: flex; flex-wrap: wrap; gap: 10px;';
        profile.images.forEach((imageData) => {
            const imgWrapper = document.createElement('div');
            imgWrapper.style = 'position: relative; display: inline-block;';

            const imgElement = document.createElement('img');
            imgElement.src = `data:image/png;base64,${imageData}`;
            imgElement.style = 'width: 100px; border-radius: 5px;';

            imgWrapper.appendChild(imgElement);
            imageContainer.appendChild(imgWrapper);
        });

        // Delete Button (Deletes Entire Profile)
        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete Profile';
        deleteButton.style = 'background: red; color: white; padding: 5px 10px; margin-left: 10px;';
        deleteButton.onclick = () => deleteProfile(index);

        profileCard.appendChild(textContainer);
        profileCard.appendChild(imageContainer);
        profileCard.appendChild(deleteButton);
        profilesContainer.appendChild(profileCard);
    });
}

function deleteProfile(index) {
    let profiles = JSON.parse(localStorage.getItem('profiles')) || [];
    profiles.splice(index, 1);
    localStorage.setItem('profiles', JSON.stringify(profiles));
    loadProfiles();
}

async function convertToBase64(file) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result.split(',')[1]);
        reader.onerror = error => reject(error);
        reader.readAsDataURL(file);
    });
}

// Load profiles on page load
window.onload = loadProfiles;
</script>
