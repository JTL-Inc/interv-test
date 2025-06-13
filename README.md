# 🧠 Algorithm Challenge: Event RSVP Tracker

## Overview

You are building a system to track RSVPs for events on a ticketing platform. Each RSVP action is logged as a record, but users may update or cancel their RSVP later.

Your task is to determine which users currently have a valid RSVP for a given event, based on the latest action they've taken.

---

## 🧾 Problem Statement

You are given a list of RSVP actions, where each action is represented as a JavaScript object with the following structure:

```js
{
  userId: Number,
  eventId: Number,
  action: 'RSVP' | 'CANCEL'
}
Your goal is to write a function that, for a given eventId, returns a list of userIds who have a current valid RSVP — meaning the user's most recent action was 'RSVP'.

🧪 Example Input
js
Copy
Edit
const actions = [
  { userId: 1, eventId: 101, action: 'RSVP' },
  { userId: 2, eventId: 101, action: 'RSVP' },
  { userId: 1, eventId: 101, action: 'CANCEL' },
  { userId: 3, eventId: 101, action: 'RSVP' },
  { userId: 2, eventId: 101, action: 'CANCEL' },
  { userId: 4, eventId: 101, action: 'RSVP' }
];
Expected Output
js
Copy
Edit
getCurrentRSVPs(actions, 101);
// ➞ [3, 4]
🧑‍💻 Function Signature
js
Copy
Edit
/**
 * Returns a sorted array of userIds who currently have a valid RSVP for the event.
 *
 * @param {Array} actions - An array of RSVP action objects.
 * @param {number} eventId - The ID of the event to filter actions for.
 * @returns {number[]} - Sorted list of userIds with valid RSVPs.
 */
function getCurrentRSVPs(actions, eventId) {
  const latestActionMap = new Map();

  for (const action of actions) {
    if (action.eventId !== eventId) continue;
    latestActionMap.set(action.userId, action.action);
  }

  return Array.from(latestActionMap.entries())
    .filter(([_, action]) => action === 'RSVP')
    .map(([userId]) => userId)
    .sort((a, b) => a - b);
}
✅ Requirements
Only the most recent action per user for the given event should count.

Return the list of user IDs sorted in ascending order.

Optimize for performance — assume the actions list can have tens of thousands of entries.

🔄 Bonus Questions (Optional)
How would you extend this to support tracking multiple events efficiently?

What is the time and space complexity of your solution?

How would you implement this using a SQL query or in a production backend system?

🧰 Running Locally (Optional)
You can copy the code into any JavaScript runtime or editor:

Node.js

CodeSandbox

Replit

JSFiddle

Example usage:

js
Copy
Edit
console.log(getCurrentRSVPs(actions, 101)); // [3, 4]
Good luck! 🚀
