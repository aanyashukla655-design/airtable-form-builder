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
UI is intentionally plain because logic matters more here.

