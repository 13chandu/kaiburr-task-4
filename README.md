# kaiburr-task-4
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Record Management</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Record Management</h1>
    
    <!-- Form for adding records -->
    <form id="record-form">
        <label for="name">Name:</label>
        <input type="text" id="name" required>
        <label for="description">Description:</label>
        <input type="text" id="description" required>
        <button type="submit">Add Record</button>
    </form>

    <!-- Table to display records -->
    <table id="record-table">
        <thead>
            <tr>
                <th>Name</th>
                <th>Description</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <!-- Records will be displayed here -->
        </tbody>
    </table>

    <script src="script.js"></script>
</body>
</html>
// Sample data store for records
let records = [];

const recordForm = document.getElementById("record-form");
const recordTable = document.getElementById("record-table").getElementsByTagName("tbody")[0];

// Function to add a record
function addRecord() {
    const name = document.getElementById("name").value;
    const description = document.getElementById("description").value;

    // Add the record to the data store
    records.push({ name, description });

    // Clear form fields
    document.getElementById("name").value = "";
    document.getElementById("description").value = "";

    // Refresh the table
    displayRecords();
}

// Function to display records in the table
function displayRecords() {
    recordTable.innerHTML = "";
    records.forEach((record, index) => {
        const row = recordTable.insertRow();
        const cell1 = row.insertCell(0);
        const cell2 = row.insertCell(1);
        const cell3 = row.insertCell(2);

        cell1.innerHTML = record.name;
        cell2.innerHTML = record.description;

        // Add a delete button
        const deleteButton = document.createElement("button");
        deleteButton.innerHTML = "Delete";
        deleteButton.addEventListener("click", () => deleteRecord(index));
        cell3.appendChild(deleteButton);
    });
}

// Function to delete a record
function deleteRecord(index) {
    records.splice(index, 1);
    displayRecords();
}

// Event listener for form submission
recordForm.addEventListener("submit", function (e) {
    e.preventDefault();
    addRecord();
});

// Initial display of records
displayRecords();
