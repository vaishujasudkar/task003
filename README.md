# task003
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fitness Tracker App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Fitness Tracker Application -->
  <div class="fitness-app">
    <h1>Fitness Tracker</h1>

    <!-- Workout Logging Section -->
    <section class="log-section">
      <h2>Log Your Workout</h2>
      <label for="workoutType">Workout Type:</label>
      <input type="text" id="workoutType" placeholder="e.g., Running, Cycling" required>

      <label for="duration">Duration (minutes):</label>
      <input type="number" id="duration" placeholder="e.g., 45" min="1" required>

      <label for="calories">Calories Burned:</label>
      <input type="number" id="calories" placeholder="e.g., 300" min="1" required>

      <button onclick="logWorkout()">Add Workout</button>
    </section>

    <!-- Workout Log Display Section -->
    <section class="log-display">
      <h2>Your Workout Log</h2>
      <ul id="workoutList">cardio ,Running,
 Jogging,Wight lifting</ul>
    </section>

    <!-- Summary Section -->
    <section class="summary-section">
      <h2>Summary</h2>
      <p>Total Workouts: <span id="totalWorkouts">2</span></p>
      <p>Total Duration: <span id="totalDuration">30</span> minutes</p>
      <p>Total Calories Burned: <span id="totalCalories">200</span> kcal</p>
    </section>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  background-color: #f4f6f9;
}

.fitness-app {
  max-width: 500px;
  padding: 20px;
  border-radius: 10px;
  background-color: #fff;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  color: #333;
  font-size: 1.8em;
}

h2 {
  color: #4CAF50;
  font-size: 1.5em;
  margin-top: 20px;
}

label {
  display: block;
  margin: 10px 0 5px;
  font-weight: bold;
  color: #333;
}

input[type="number"], 
input[type="text"] {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 1em;
  box-sizing: border-box;
}

button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #45a049;
}

#workoutList {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

#workoutList li {
  background-color: #f1f1f1;
  margin: 5px 0;
  padding: 10px;
  border-radius: 5px;
  color: #333;
}

.summary-section p {
  font-size: 1.1em;
  color: #555;
}
// Array to store workout logs
let workouts = [];

// Totals for the summary section
let totalWorkouts = 0;
let totalDuration = 0; // Total minutes across all workouts
let totalCalories = 0; // Total calories burned across all workouts

// Function to log a new workout entry
function logWorkout() {
  const workoutType = document.getElementById("workoutType").value.trim(); // Get the workout type input
  const duration = parseInt(document.getElementById("duration").value); // Get the duration as integer
  const calories = parseInt(document.getElementById("calories").value); // Get the calories burned as integer

  // Input validation to ensure all fields are filled and contain valid data
  if (!workoutType || isNaN(duration) || duration <= 0 || isNaN(calories) || calories <= 0) {
    alert("Please enter valid workout details for type, duration (positive minutes), and calories (positive value).");
    return;
  }

  // Create a workout object and add it to the workouts array
  const workout = {
    type: workoutType,
    duration: duration, // Duration of workout in minutes
    calories: calories, // Calories burned
    date: new Date().toLocaleDateString() // Date of workout in readable format
  };
  
  workouts.push(workout); // Add the new workout entry to the workouts array
  updateSummary();         // Update the summary section with totals
  displayWorkouts();       // Display the full list of workouts

  // Clear the input fields after successfully logging the workout
  document.getElementById("workoutType").value = "";
  document.getElementById("duration").value = "";
  document.getElementById("calories").value = "";
}

// Function to display each workout in the log
function displayWorkouts() {
  const workoutList = document.getElementById("workoutList");
  workoutList.innerHTML = ""; // Clear previous entries to prevent duplication

  workouts.forEach((workout) => {
    const workoutItem = document.createElement("li"); // Create a list item for each workout
    workoutItem.textContent = `${workout.date} - ${workout.type}: ${workout.duration} mins, ${workout.calories} kcal burned.`; // Format the workout details
    workoutList.appendChild(workoutItem); // Append the formatted workout item to the list
  });
}

// Function to update the summary section
function updateSummary() {
  // Calculate total workouts, duration, and calories burned
  totalWorkouts = workouts.length;
  totalDuration = workouts.reduce((acc, workout) => acc + workout.duration, 0);
  totalCalories = workouts.reduce((acc, workout) => acc + workout.calories, 0);

  // Display updated summary values
  document.getElementById("totalWorkouts").textContent = totalWorkouts;
  document.getElementById("totalDuration").textContent = totalDuration;
  document.getElementById("totalCalories").textContent = totalCalories;
}
# Output
The Fitness Tracker App allows users to:

Log Workouts: Users can input the workout type, duration (in minutes), and calories burned, then click "Add Workout" to save the entry.
View Workout Log: Each workout entry appears in a list, showing the date, type, duration, and calories burned.
Summary: The app provides a summary section displaying:
Total number of workouts
Total duration (minutes)
Total calories burned
