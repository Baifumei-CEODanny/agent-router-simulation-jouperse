# AgentRouter.js Simulation – Plugin Deployment Router

---

## 🧠 Objective

Simulate a JavaScript routing system that mimics how AI agents will deploy plugins in the future. This tool will:

- Fetch tasks
- Match them to plugin directories
- Trigger mock deployments via webhook/API  
  Includes retry logic, logging, and modularity.

---

## 📦 Scope & Requirements

### 🔁 Polling System

- Check a static `tasks.json` or API endpoint every X seconds.
- Parse task payloads.

### 🔌 Plugin Mapping

- Match each task to a plugin folder inside `/repos/` (e.g. `b2b-plugins/top-carousel/`).
- Use logic based on the `target` key in the task.

### 🚀 Trigger Deployment

Send POST request to a mock webhook:

```http
POST /deploy
{
  "plugin": "top-carousel",
  "version": "v1.2.0"
}
```

- Handle response: success/failure.
- Retry 3 times if it fails, with exponential backoff.

### 📝 Logging

- Console logs + write to `deploy-log.txt` each time a task runs.
- Log result status: `SUCCESS` or `FAILURE`.

### ⚠️ Error Handling

- Handle corrupted JSON.
- Skip unknown plugin references.
- Validate basic schema before sending payload.

---

## 🛠 Tech Stack

- Node.js
- Axios or native `fetch`
- `fs` module for logging
- `setInterval` or async loop for polling

---

## ✅ Evaluation Criteria

- Correct routing logic: **Task → Folder → Webhook**
- Code modularity: Clean separation of fetch, match, deploy
- Stability: Handles edge cases, logs, retries
- Readability and comments
- Efficiency of logic (minimal assumptions, scalable)

---

## 🌟 Stretch Goals (Optional)

- Build a CLI menu to simulate manual overrides  
  _Example_: `node agentRouter.js --task=xyz`
- Add basic `.env` config for endpoint and polling time

---

## ▶️ How to Run

Run via Node.js:

```bash
node agentRouter.js
```

---

## ❓ AgentRouter.js Test – FAQ & Expectations

### What’s the goal of this test?

We’re assessing your JavaScript logic and system thinking. You’ll build a simulation of a lightweight deployment router using Node.js — no UI, no frameworks, just logic and structure.

### Do I need a real webhook or backend?

No. You can:

- Use `console.log` to simulate sending POST requests
- Or test against a tool like [https://webhook.site](https://webhook.site) to observe the request payload

### How do I simulate the plugin directories?

Just create local folders such as `/repos/b2b-plugins/top-carousel/` or similar. No real code is needed in these folders — it’s to validate your directory matching logic.

### What libraries can I use?

You can use:

- Node.js core modules (`fs`, `path`, `setInterval`, etc.)
- Either `axios` or `node-fetch` for sending HTTP requests

Avoid frontend frameworks, bundlers, or any unnecessary packages.

### How do I run the script?

Run it using Node:

```bash
node agentRouter.js
```

It should:

- Read and parse a task from `tasks.json`
- Match it to a folder
- Send a simulated POST request
- Retry if the request fails
- Log the result (both to console and to a `.txt` file)

### What should I focus on?

- Clean, modular code — functions should be separated clearly
- Retry logic with exponential backoff
- Edge case handling: invalid JSON, unknown plugin name, failed response
- Clear logs for both success and failure cases

### How long should this take?

2–4 hours maximum.  
If it takes longer, simplify and focus on working logic, not overengineering.

### What do I need to submit?

Submit a `.zip` or GitHub repo containing:

- `agentRouter.js`
- `tasks.json`
- Any helper modules
- A short README with basic run instructions

---
