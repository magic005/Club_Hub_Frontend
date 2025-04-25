<script>
async function fetchAndDisplayClubs(userInterests) {
    try {
        const URL = `${pythonURI}/api/club`;
        const response = await fetch(URL, {
            method: 'GET',
            headers: { 'Authorization': getToken() },
        });

        if (!response.ok) throw new Error('Failed to fetch clubs');

        const clubs = await response.json();
        const clubsContainer = document.getElementById('clubs-container');
        clubsContainer.innerHTML = '';

        const matchedClubs = clubs.map(club => {
            const matchCount = club.topics.filter(topic => userInterests.includes(topic)).length;
            return { ...club, matchCount };
        }).filter(club => club.matchCount > 0)
          .sort((a, b) => b.matchCount - a.matchCount);

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
<script>