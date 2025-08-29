# MWAD-EX_03-To-Do-List-using-JavaScript
## Date:

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM

index.html
```
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="todo-container">
    <h1>✅ To-Do List</h1>
    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Add a new task...">
      <button id="addTaskBtn">Add</button>
    </div>

    <ul id="taskList"></ul>

    <div class="filters">
      <button data-filter="all" class="filter active">All</button>
      <button data-filter="active" class="filter">Active</button>
      <button data-filter="completed" class="filter">Completed</button>
    </div>

    <button id="clearCompleted">Clear Completed</button>
  </div>
  <script src="script.js"></script>
</body>
</html>
```
style.css
```
/* Global Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  background: linear-gradient(135deg, #7ed2e3, #8823ed);
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

/* Container */
.todo-container {
  background: #fff;
  padding: 25px 30px;
  border-radius: 20px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
  width: 400px;
  text-align: center;
  transition: transform 0.3s ease-in-out;
}

.todo-container:hover {
  transform: translateY(-5px);
}

/* Heading */
h1 {
  margin-bottom: 20px;
  color: #333;
  font-size: 28px;
  font-weight: 600;
}

/* Input Group */
.input-group {
  display: flex;
  margin-bottom: 20px;
}

#taskInput {
  flex: 1;
  padding: 10px 12px;
  border: 2px solid #ddd;
  border-radius: 12px;
  outline: none;
  font-size: 14px;
  transition: 0.3s;
}

#taskInput:focus {
  border-color: #667eea;
  box-shadow: 0 0 6px rgba(102,126,234,0.5);
}

#addTaskBtn {
  padding: 10px 14px;
  margin-left: 10px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: 0.3s;
  font-weight: 500;
}

#addTaskBtn:hover {
  background: linear-gradient(135deg, #5a6dd6, #6a3d94);
}

/* Task List */
#taskList {
  list-style: none;
  margin-top: 15px;
  padding: 0;
  max-height: 300px;
  overflow-y: auto;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px;
  border-radius: 12px;
  background: #f8f8f8;
  margin-bottom: 10px;
  transition: 0.3s;
}

.task:hover {
  background: #f0f0f0;
  transform: scale(1.02);
}

.task.completed span {
  text-decoration: line-through;
  color: gray;
  opacity: 0.7;
}

.task span {
  flex: 1;
  text-align: left;
  font-size: 15px;
  cursor: pointer;
  user-select: none;
}

.delete-btn {
  background: #ff4d4d;
  color: white;
  border: none;
  border-radius: 10px;
  padding: 6px 10px;
  cursor: pointer;
  font-size: 13px;
  transition: 0.3s;
}

.delete-btn:hover {
  background: #e60000;
}

/* Filters */
.filters {
  margin-top: 20px;
}

.filter {
  margin: 0 5px;
  padding: 8px 14px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 500;
  background: #eee;
  transition: 0.3s;
}

.filter.active {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
}

.filter:hover {
  background: #ddd;
}

/* Clear Completed */
#clearCompleted {
  margin-top: 20px;
  padding: 10px;
  width: 100%;
  border: none;
  background: #ff9800;
  color: white;
  border-radius: 12px;
  cursor: pointer;
  font-weight: 500;
  transition: 0.3s;
}

#clearCompleted:hover {
  background: #e68900;
}

```
script.js
```
const taskInput = document.getElementById("taskInput");
const addTaskBtn = document.getElementById("addTaskBtn");
const taskList = document.getElementById("taskList");
const filters = document.querySelectorAll(".filter");
const clearCompleted = document.getElementById("clearCompleted");

let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
let currentFilter = "all";

function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

function renderTasks() {
  taskList.innerHTML = "";

  let filteredTasks = tasks.filter(task => {
    if (currentFilter === "active") return !task.completed;
    if (currentFilter === "completed") return task.completed;
    return true;
  });

  filteredTasks.forEach((task, index) => {
    const li = document.createElement("li");
    li.className = "task" + (task.completed ? " completed" : "");

    const span = document.createElement("span");
    span.textContent = task.text;
    span.contentEditable = false;

    span.addEventListener("click", () => {
      task.completed = !task.completed;
      saveTasks();
      renderTasks();
    });

    span.addEventListener("dblclick", () => {
      span.contentEditable = true;
      span.focus();
    });

    span.addEventListener("blur", () => {
      span.contentEditable = false;
      task.text = span.textContent;
      saveTasks();
      renderTasks();
    });

    const deleteBtn = document.createElement("button");
    deleteBtn.textContent = "X";
    deleteBtn.className = "delete-btn";
    deleteBtn.addEventListener("click", () => {
      tasks.splice(index, 1);
      saveTasks();
      renderTasks();
    });

    li.appendChild(span);
    li.appendChild(deleteBtn);
    taskList.appendChild(li);
  });
}

function addTask() {
  const text = taskInput.value.trim();
  if (text) {
    tasks.push({ text, completed: false });
    taskInput.value = "";
    saveTasks();
    renderTasks();
  }
}

addTaskBtn.addEventListener("click", addTask);
taskInput.addEventListener("keypress", (e) => {
  if (e.key === "Enter") addTask();
});

filters.forEach(button => {
  button.addEventListener("click", () => {
    filters.forEach(btn => btn.classList.remove("active"));
    button.classList.add("active");
    currentFilter = button.dataset.filter;
    renderTasks();
  });
});

clearCompleted.addEventListener("click", () => {
  tasks = tasks.filter(task => !task.completed);
  saveTasks();
  renderTasks();
});

renderTasks();
```


## OUTPUT
<img width="1919" height="1015" alt="Screenshot 2025-08-29 155041" src="https://github.com/user-attachments/assets/bdff3c00-0f85-472b-9135-02656157a03e" />



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
