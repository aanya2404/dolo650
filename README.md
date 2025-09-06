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
