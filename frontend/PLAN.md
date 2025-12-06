# Frontend Plan (React)

I kept the frontend design minimal because the assignment says UI is not priority. My goal was to make the flow understandable.

---

## Pages I Designed

### 1. Login Page
Very basic → button → redirects to Airtable OAuth.

### 2. Select Base + Table Page
After login:
- Fetch user bases
- User chooses a base
- Then chooses a table

### 3. Select Fields Page
List of Airtable fields appears.
User selects:
- which fields become questions
- rename labels
- mark required/optional

Unsupported types: ignored.

### 4. Conditional Logic Page
Simple dropdowns:
- IF field A equals something → show field B

Multiple conditions allowed.

### 5. Fill Form Page
Loads the form schema from backend.
As user types, conditional logic runs:
- show/hide fields real-time

### 6. Responses Page
Shows list of submissions from MongoDB only.

---

## Why UI Is Basic
I didn’t focus on animations/colors.  
I made it work logically first.
