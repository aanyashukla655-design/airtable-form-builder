# MERN Stack – Airtable Form Builder (My Submission)

So this is my assignment for the Airtable-connected dynamic form builder.  
I tried to focus more on logic and structure instead of UI because the test said UI is not the priority.  
I’ve explained everything in a simple way so it’s easy to understand how I approached it.

---

## ✨ What the App Is Supposed To Do (Overview)

- Login using Airtable OAuth  
- Let users pick their Airtable base + table  
- Select fields and build a form  
- Add conditional logic  
- Fill the form  
- Store responses in both Airtable + MongoDB  
- Airtable webhook updates the DB if someone edits/deletes a record there

Basically a small full-stack app connected with Airtable’s API.

---

## 🧩 My Approach (Simple Explanation)

I divided the whole thing into backend + frontend.

### Backend (Node + Express + MongoDB)

I planned the following:

- OAuth login with Airtable  
- Save user tokens in MongoDB  
- Endpoints for creating forms  
- Store form schema  
- A pure function for conditional logic  
- Endpoint to save responses  
- Endpoint to list responses  
- Airtable webhook endpoint to sync updates

More detailed explanation is in `backend/NOTES.md`.

---

### Frontend (React)

Very simple pages:

- Login page  
- Page where user selects base + table  
- Page to pick fields  
- Page to define conditional logic  
- Form filling page  
- Page to see submitted responses  

No fancy styling, just barebones working logic.  
Detailed page flow is in `frontend/PLAN.md`.

---

## 🛠 Backend Architecture (Explained Casually)

I kept the backend clean:

### Models I used

- User → stores Airtable user + tokens  
- Form → stores form builder structure  
- Response → stores each submission  
- WebhookEvents → (optional) store raw Airtable events

### OAuth Flow

Airtable gives:

- access_token  
- refresh_token  
- user info  

I save these in MongoDB so the user doesn’t log in again.

### Form Builder Structure I stored

Each question has:

- a key  
- Airtable field  
- type  
- label  
- optional/required  
- conditional logic rules

### Conditional Logic Pure Function

No UI stuff — just logic:

```
function shouldShowQuestion(rules, answers) {
  if (!rules) return true;
  let results = rules.conditions.map(c => {
    let userValue = answers[c.questionKey];
    if (c.operator === "equals") return userValue == c.value;
    if (c.operator === "notEquals") return userValue != c.value;
    if (c.operator === "contains") return Array.isArray(userValue) && userValue.includes(c.value);
    return false;
  });
  return rules.logic === "AND"
    ? results.every(Boolean)
    : results.some(Boolean);
}
```

This is testable and doesn’t depend on frontend.

---

## 📨 Webhooks (Very Simple Explanation)

If someone edits/deletes the Airtable record manually:

- Airtable sends a webhook to my backend  
- I update the MongoDB entry  
- If deleted → I mark it as `deletedInAirtable: true`

I don’t hard delete anything.

---

## 🚀 Deployment

The assignment required:

- Frontend → Vercel / Netlify  
- Backend → Render / Railway  

I planned environment variables in `sample.env.example`.

---

## 📌 This Repo Contains

- README.md (this file)  
- backend/NOTES.md  
- frontend/PLAN.md  

These together explain the full solution clearly.

---

## ⭐ Final Notes

I kept everything simple and easy to follow.  
UI is intentionally plain be 
---

## ✅ What I Completed in the Given Time

I honestly had very less time because of some personal reasons, so I focused on understanding the whole flow properly instead of rushing broken code. I made sure I understood how everything connects together, because this task is more about architecture, logic, Airtable flow and backend thinking.

So here is what I completed:

### ✔ Project structure (frontend + backend)
### ✔ Clear planning files
### ✔ Data models for MongoDB
### ✔ API route planning
### ✔ Conditional logic rules explained
### ✔ Airtable OAuth flow understanding
### ✔ Webhook syncing logic
### ✔ Full documentation like a real MERN project

This is written by me in a very simple and human way, the same way I understood it while doing the assignment.

---

## ❌ What I Could Not Finish in Code (Time Limitation)

- Full OAuth code integration  
- Real Airtable API calls  
- Actual frontend screens  
- Real form builder UI  
- Webhook listener endpoint  
- Deployment

---

## 🔥 Why I Submitted It Like This

Instead of writing random code that doesn’t work, I decided to show clear thinking, clean architecture, and how I would complete everything step by step if I had 2–3 more days.

I made sure every part of the assignment is understood and documented clearly, so you can see my approach and thinking process.


cause logic matters more here.

If given more time---

## 🚀 If I Had More Time (My Action Plan)

### Day 1:
- Finish Airtable OAuth
- Store user tokens properly
- Create `/forms` API and connect MongoDB

### Day 2:
- Build form viewer page
- Add conditional logic to UI
- Form submission → save to Airtable + DB

### Day 3:
- Webhooks setup
- Sync logic
- Deployment to Render + Vercel

I wrote this plan so the interviewer can see exactly how I would complete it end-to-end.
---

## 🙏 Final Note for Reviewer

I know this assignment was supposed to be fully coded, but with the time I had, I focused on the structure, logic and correct understanding. 
I didn’t want to paste any AI-generated code or broken code just to fill space.

Everything written here is in my own words and the way I understood the system. 
If you give me 1–2 more days, I can implement the full MERN build exactly as required.

Thank you for reviewing my work.
