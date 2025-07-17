# 📚 Educational Assistant AI Agent – n8n Workflow

## 🧠 Overview

This n8n workflow acts as an AI-powered **educational assistant** that intelligently responds to student questions. It identifies whether a question is suited for **below 5th grade** or **above 5th grade**, summarizes a relevant answer, generates related follow-up questions, and sends the complete response back via webhook.

---

## ⮏ How It Works

### 🔹 1. Webhook Trigger

* Listens for incoming user questions via HTTP POST.
* The question is passed as JSON.

### 🔹 2. AI/Code Node – Grade Level Classifier

* The AI agent analyzes the question text and determines:

  * ✅ If it's for **below 5th grade** → returns `true`
  * ❌ If it's for **above 5th grade** → returns `false`

### 🔹 3. IF Node – Conditional Branching

* If condition is `true`: Routes to **basic summarizer**
* If condition is `false`: Routes to **advanced summarizer**

### 🔹 4. AI Agent – Answer Summarizer

* Generates a concise, friendly, and grade-appropriate summary of the answer.

### 🔹 5. AI Agent – Related Question Generator

* Forms 2–3 follow-up questions based on the topic.

### 🔹 6. Webhook Response

* Responds with a structured JSON containing:

  * The summarized answer
  * Related questions

---

## 📕 How to Use This Workflow

1. **Import the workflow** into your n8n editor.
2. **Set up the Webhook node** and copy the generated URL.
3. **Configure the AI Agent nodes** with your OpenAI (or other AI) credentials.
4. **Deploy the workflow** by clicking *Activate* in the editor.
5. **Send a POST request** with the question field to the webhook URL:

```json
{
  "question": "What is the difference between evaporation and condensation?"
}
```

6. **Receive the AI response** with summarized content and related questions as JSON.

---

## 📥 Example Input (via Webhook)

```json
{
  "question": "What is the difference between evaporation and condensation?"
}
```

---

## 📤 Example Output (via Webhook Response)

```json
{
  "summary": "Evaporation is when water turns into gas, while condensation is when gas turns back into water.",
  "relatedQuestions": [
    "What causes evaporation?",
    "Where can we see condensation in real life?",
    "How is the water cycle connected to these processes?"
  ]
}
```

---

## 🛠️ Components Used

| Component        | Purpose                                           |
| ---------------- | ------------------------------------------------- |
| Webhook Node     | Entry and response point for questions            |
| AI Agent Node    | Classify grade, summarize, and generate questions |
| IF Node          | Route based on grade level                        |
| Code Node (opt.) | For custom logic or fallback handling             |

---

## ✅ Use Cases

* EdTech apps and chatbots
* School learning platforms
* AI-based Q\&A tutors
* Interactive classroom assistants

---

## 🧠 Smart Logic Sample (Classification Prompt Logic)

> Given a question, classify whether it is appropriate for students below or above 5th grade.
> If it uses simple concepts or basic definitions → "true"
> If it involves deeper theory, reasoning, or technical terms → "false"

---

## 🌐 API/Webhook Notes

* **Webhook URL**: Use the webhook node to expose your endpoint.
* **Method**: `POST`
* **Content-Type**: `application/json`

---

## 📌 Tips

* Add error handling for missing `question` field.
* You can enhance classification with keyword detection for grade level.
* Customize AI prompts based on your tone (friendly, formal, kid-friendly, etc.).

---

## 📷 Optional: Visual Flow Example (describe in n8n)

```
[Webhook] → [Classifier] → [IF Node] → [Summarizer] → [Question Generator] → [Webhook Response]
```

---

## 🚀 Ready to Deploy!

You now have a smart educational AI agent in n8n that:

* Understands question levels
* Answers intelligently
* Engages learners with follow-ups

> Enhance learning. Automate answers. Educate better.

---

