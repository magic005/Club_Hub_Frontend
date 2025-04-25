<script>
    // this function fetches a list of clubs from a backend and filters them
    // based on the user's selected interests, and displays matched clubs visually
   
    // try/catch structure and error alerting adapted with help from ChatGPT examples for troubleshooting

    async function fetchAndDisplayClubs(userInterests) {
        try {
            const URL = `${pythonURI}/api/club`; // api endpoint to get the club data ()

            // structure for the fetch request adapted from 'Nighthawk Coders' repository (https://github.com/nighthawkcoders/flocker_frontend)
            const response = await fetch(URL, {
                method: 'GET',
                headers: { 'Authorization': getToken() }, // input (authorization token (user input from storage))
            });

            if (!response.ok) throw new Error('Failed to fetch clubs'); // selection (error handling, output)

            const clubs = await response.json(); // parses the json list of club objects (input; online data stream)
            const clubsContainer = document.getElementById('clubs-container'); // Output target (visual output)
            clubsContainer.innerHTML = ''; // Clear old results

            // algorithm using .map, .filter, .sort to process userInterests (list), adapted with assistance from ChatGPT
            const matchedClubs = clubs.map(club => {
                const matchCount = club.topics.filter(topic => userInterests.includes(topic)).length; // list intersection
                return { ...club, matchCount }; // attach match count to each club object
            }).filter(club => club.matchCount > 0) // selection (only keep clubs with shared interests)
            .sort((a, b) => b.matchCount - a.matchCount); // sorting (algorithmic sequencing)

            if (matchedClubs.length > 0) { // selection
                matchedClubs.forEach(club => { // iteration
                    const clubCard = document.createElement('div'); // creates a visual output
                    clubCard.classList.add('club-card');
                    clubCard.innerHTML = `
                        <div class="club-title">${club.name}</div>
                        <div class="club-description">${club.description}</div>
                        <div class="club-founder">Founded by: ${club.user_id}</div>
                        <div class="matched-interests">Matches ${club.matchCount} of your interests</div>
                    `;
                    clubsContainer.appendChild(clubCard); // output to dom (visual output on the project frontend)
                });
                document.getElementById('club-results').style.display = 'block'; // show results container
            } else {
                // when no matches found --> show the aappropriate output message
                clubsContainer.innerHTML = `<div class="no-matches">No clubs match your interests. Try selecting more!</div>`;
                document.getElementById('club-results').style.display = 'block';
            }
        } catch (error) {
            // error handling: output error and alert
            console.error('Error fetching clubs:', error); // output (in the console)
            alert('Error fetching clubs.'); // output (textual alert for errors)
        }
    } // end of fetchAndDisplayClubs()
</script>