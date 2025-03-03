---
layout: post
title: Final Review Blog - Ansh
permalink: /final_ansh
menu: nav/home.html
show_reading_time: false
---


# Discover Page Feature Blog Write-Up + 5 Things I Did Over 12 Weeks

## Feature Blog Write-Up

### Purpose
The **Discover Page** was developed to address the need for a **centralized and personalized club exploration experience**. Many students struggle with finding the right clubs that match their interests, leading to missed opportunities and under-involvement. The Discover Page solves this issue by offering:
- A **recommendation system** based on user-selected interests.
- A visually appealing, **filterable list of clubs**.
- An **intuitive UI** to explore clubs through descriptions, categories, and student reviews.
- Integration with other ClubHub features, ensuring a seamless experience from discovery to joining.

I designed and developed this feature from **frontend to backend**, ensuring that it not only functioned smoothly but also integrated well into the overall **Club Hub ecosystem**.

I will now, briefly walk through the process of using this feature, 

---

## 5 Things I Did Over 12 Weeks

### 1. **Discover Page Frontend**
- Built the entire **Discover Page UI**, ensuring a clean and user-friendly interface.
- Integrated a **dynamic filtering system**, allowing users to sort by interests, club type, and popularity.
- Styled the page to maintain consistency with ClubHub’s theme, emphasizing usability and clarity.
- Optimized the **loading performance**, ensuring quick rendering of results.
- Used **JavaScript and Fetch API** to communicate efficiently with the backend.

#### Key Code Snippet:
```javascript
async function fetchClubs() {
    const response = await fetch('/api/clubs');
    const clubs = await response.json();
    displayClubs(clubs);
}
```

---

### 2. **Discover Page Backend**
- Designed and implemented the **API routes** for fetching club data dynamically.
- Optimized database queries to ensure **low-latency responses**.
- Integrated a **search algorithm** that prioritizes relevance based on user preferences.
- Created an **admin panel** for club leaders to manage visibility on the Discover Page.

#### Key Code Snippet:
```python
@app.route('/api/clubs', methods=['GET'])
def get_clubs():
    clubs = Club.query.order_by(Club.popularity.desc()).all()
    return jsonify([club.to_dict() for club in clubs])
```

---

### 3. **Peripheral & Base UI/UX Design for the Entire Site**
- Led the **site-wide design language**, ensuring consistency across all features.
- Developed **global CSS styling** and reusable UI components.
- Implemented **responsive layouts** to ensure a smooth experience on all devices.
- Created the **navigation system**, integrating routing between key pages.
- Standardized **color schemes, typography, and button styles**.

#### Example of Styling Standardization:
```css
.button-primary {
    background: linear-gradient(45deg, #FF4B2B, #FF416C);
    border-radius: 5px;
    color: white;
    padding: 10px 20px;
}
```

---

### 4. **Effective Use of KanBan & Issue Tracking**
- As **Scrum Master**, I ensured our team adhered to Agile principles.
- Maintained a **KanBan board**, assigning tasks based on priority and deadlines.
- Organized **sprint retrospectives**, adjusting our workflow for efficiency.
- Used **GitHub Issues** to track progress, ensuring all team members stayed aligned.

This can be seen here:

---

### 5. **Scrum Master & Project Coordination**
- Facilitated **stand-up meetings**, ensuring everyone was aligned on deliverables.
- Set milestones and deadlines, keeping the team on track.
- Resolved bottlenecks by helping debug, reviewing pull requests, and mentoring teammates.
- Ensured the **CI/CD pipeline** ran smoothly, maintaining project integrity.

---

## How I Met CPT Requirements

### **Big Idea 1.1 & 1.2 - Collaboration, Program Function, and Purpose**
- Used Agile methodologies to **divide and manage tasks** across team members.
- Collaborated through **code reviews, Git branches, and real-time debugging**.
- Designed the Discover Page to **enhance user experience and club engagement**.

### **Big Idea 1.3 - Program Design and Development**
- Ensured seamless **frontend-backend integration**, using RESTful APIs.
- Created a **modular, scalable design** to accommodate future feature additions.
- **Documented design decisions** using flowcharts and markdown-based technical specs.

### **Big Idea 1.4 - Debugging Code and Fixing Errors**
- Used **Postman to test API endpoints** for the Discover Page.
- Fixed CSS inconsistencies and **optimized JavaScript performance**.
- Debugged backend SQL queries to **reduce response times**.

### **Big Idea 2 - Data and Database Management**
- Designed the **Club table schema** in SQLAlchemy for efficiency.
- Implemented **data backup and restore functionality**.
- Optimized queries for fast search and filtering performance.

### **Big Idea 4 - Internet & Security**
- Used **JWT authentication** to secure API requests.
- Implemented **role-based access controls** for Discover Page admin features.
- Followed **best practices for API security** to prevent vulnerabilities.

---

## Final Thoughts

Over the course of 12 weeks, I played a crucial role in developing ClubHub, particularly through the **Discover Page, site-wide UI design, Scrum leadership, and efficient project tracking**. The event at Night at the Museum was an excellent opportunity to showcase my work and receive feedback for future improvements. This experience solidified my ability to lead a development project and coordinate effectively with a team.



# Self Grading

| **Category** | **Points** | **Description** | **Self Grade** |
|-------------|-----------|----------------|---------------|
| **Five tasks over 12 weeks** | 5 | List five things completed, including issues addressed, burndown tracking, and presentation work. | 4.5 |
| **Full Stack Project Demo** | 2 | Demonstrate the project, highlight CPT requirements | 1.8 |
| **Project Feature Blog Write-up** | 1 | Use CPT/FRQ language to write a structured blog post on project features. | 0.9 |
| **MCQ Completion** | 1 | Successfully complete and reflect on multiple-choice questions. | 1 |
| **Retrospective Reflection** | 1 | Reflect on strengths and weaknesses, next steps, engagement with peers, future career thoughts, and final exam prep. | 0.9 |
| **Total** | 10 | Maximum possible score. | 9.1 |

---

## **Retrospective Reflection Criteria**

- **Reflect on strengths and weaknesses**
- **Create next steps plans for improvement**
- **Engage with peer projects and document interests**
- **Think about future steps in CompSci, classes, college, internships, or career**
- **Help a new peer with final exam prep or conduct a live review with Ms. Pataki**
- **Send a detailed summary of review points 24 hours in advance, including a self-grade assessment**
- **Highlight all 10 points in 3 minutes of Live Review**

---

## **Final Self-Assessment Notes**

I think I my composition reflected my learnings over the course of the trimester fairly well, though, I did come short at a few points in the process. Overall, I think I could have definitely done better in doing an effective demo, as (at least while practicing) it felt a bit boring. The 5 tasks I completed, although strong, aren't necessarily as strong as they could possibly be in that I didn't contribute such an excessive amount that I could generalize every aspect of my contribution and still have 5 total. So, even though I do feel that my reflection is quite strong, I think I could present it better and live up to some more contribution. 



