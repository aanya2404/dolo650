<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Reminder and Tracker</title>
  <link rel="stylesheet" href="reminder.css">
</head>
<body>
  <div class="container">
    <h1>Reminder Tracker</h1>
    <form id="reminder-form">
      <label for="reminder-type">Reminder Type</label>
      <select id="reminder-type" required>
        <option value="Medication">Medication</option>
        <option value="Doctor Appointment">Doctor Appointment</option>
      </select>

      <label for="reminder-name">Name</label>
      <input type="text" id="reminder-name" placeholder="e.g., Aspirin or Dr. Smith" required>

      <label for="details">Details</label>
      <input type="text" id="details" placeholder="e.g., 500mg or Clinic Room 2" required>

      <label for="date">Date</label>
      <input type="date" id="date" required>

      <label for="time">Time</label>
      <input type="time" id="time" required>

      <button type="submit">Add Reminder</button>
    </form>

    <ul class="reminder-list" id="reminder-list"></ul>

    <div id="notifications" class="notification" style="display: none;">
      Reminder Alert!
    </div>
  </div>
  <script src="reminder.js"></script>
</body>
</html>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body {
  background: linear-gradient(135deg, #fbc2eb, #a6c1ee, #d1c4e9);
  color: #333;
  line-height: 1.6;
  padding: 20px;
}

.container {
  max-width: 600px;
  margin: auto;
  background: #fff;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #9c27b0; /* purple */
}

form {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #6a1b9a;
}

input, select, button {
  width: 100%;
  padding: 10px;
  margin-bottom: 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
}

button {
  background: linear-gradient(135deg, #f48fb1, #9575cd, #64b5f6);
  color: #fff;
  border: none;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background: linear-gradient(135deg, #ec407a, #7e57c2, #42a5f5);
}

.reminder-list {
  list-style: none;
  padding: 0;
}

.reminder-item {
  background: #f3e5f5;
  margin-bottom: 10px;
  padding: 12px;
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.reminder-item span {
  font-size: 14px;
}

.delete-btn {
  background-color: #ef5350;
  color: #fff;
  border: none;
  padding: 6px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-btn:hover {
  background-color: #c62828;
}

.notification {
  background: #ffcc80;
  padding: 12px;
  border-radius: 6px;
  margin-bottom: 20px;
  text-align: center;
  font-weight: bold;
  color: #4e342e;
}

@media (max-width: 480px) {
  .container {
    padding: 15px;
  }

  h1 {
    font-size: 22px;
  }
}
const reminderForm = document.getElementById('reminder-form');
const reminderList = document.getElementById('reminder-list');
const notifications = document.getElementById('notifications');

let reminders = [];

// Render reminder list
function renderReminders() {
  reminderList.innerHTML = '';
  reminders.forEach((rem, index) => {
    const li = document.createElement('li');
    li.className = 'reminder-item';
    li.innerHTML = `
      <span><strong>${rem.type}:</strong> ${rem.name} - ${rem.details} on ${rem.date} at ${rem.time}</span>
      <button class="delete-btn" onclick="deleteReminder(${index})">Delete</button>
    `;
    reminderList.appendChild(li);
  });
}

// Add reminder
reminderForm.addEventListener('submit', (e) => {
  e.preventDefault();
  const type = document.getElementById('reminder-type').value;
  const name = document.getElementById('reminder-name').value;
  const details = document.getElementById('details').value;
  const date = document.getElementById('date').value;
  const time = document.getElementById('time').value;

  reminders.push({ type, name, details, date, time });
  renderReminders();
  reminderForm.reset();
});

// Delete reminder
function deleteReminder(index) {
  reminders.splice(index, 1);
  renderReminders();
}

// Check for notifications every minute
setInterval(() => {
  const now = new Date();
  const currentDate = now.toISOString().slice(0, 10); // YYYY-MM-DD
  const currentTime = now.toTimeString().slice(0, 5); // HH:MM

  reminders.forEach((rem) => {
    if (rem.date === currentDate && rem.time === currentTime) {
      notifications.textContent = `Reminder: ${rem.type} - ${rem.name} (${rem.details})`;
      notifications.style.display = 'block';
      setTimeout(() => {
        notifications.style.display = 'none';
      }, 5000);
    }
  });
}, 60000);
