# 🎥 Project 3: YouTube Quiz Bot (NumericHub)

## 🧩 The Business Problem
Running an educational YouTube channel means regularly engaging the audience.  
For *NumericHub*, that meant posting **2 math quizzes per day** on the Community tab.  

Doing this manually required:
- Coming up with new questions
- Avoiding duplicates
- Formatting posts
- Getting final approval before publishing  

It was repetitive and slowed down content output.

---

## 🚀 The Automated Solution
This workflow automates the entire quiz pipeline:
1. Pulls past quiz questions from Google Sheets  
2. Selects 3 random rows to guide AI generation  
3. Sends a custom prompt to an AI model → new question + options generated  
4. Formats the response using Code nodes  
5. Sends the question to the channel owner’s Gmail for **approval**  
6. Webhook waits for the response:  
   - If rejected → regenerate question until approved  
   - If approved → save in Google Sheets and publish to YouTube  

---

## 🔄 Workflow Flow
1. **Trigger**: Cron (runs twice daily)  
2. **Google Sheets**: Read past questions  
3. **Random Selection**: Pick 3 random rows (Code node)  
4. **AI Generation**: Generate new question + options  
5. **Format**: Structure options (A, B, C, D)  
6. **Gmail Approval**: Send to owner  
7. **Webhook Wait**: Capture response (approve/reject)  
8. **Loop if Rejected**: Repeat AI generation  
9. **On Approval**: Save + Post to YouTube  

---

## 🛠 Tools & Nodes
- **Cron** – schedule runs  
- **Google Sheets** – store & check duplicates  
- **Code** – random selection + formatting  
- **AI API** – question generation  
- **Gmail** – approval step  
- **Webhook** – wait for response  
- **YouTube API** – publish quiz  

---

## 💻 Pseudocode Example
```js
// Random question selection
const rows = getRowsFromSheet()
const picked = []
while (picked.length < 3) {
    const idx = randomIndex(rows)
    if (!picked.includes(idx)) picked.push(idx)
}
return picked.map(i => rows[i])
