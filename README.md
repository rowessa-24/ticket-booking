<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BOOKING Tickets</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
<?php
session_start();
$conn = new mysqli("localhost", "root", "", "event_management");

if (!isset($_SESSION['user_id'])) {
    die("Login required!");
}

if (!isset($_GET['event_id'])) {
    die("Event ID is required!");
}

$user_id = $_SESSION['user_id'];
$event_id = $_GET['event_id'];

// Check if the event_id exists in the events table
$event_check_sql = "SELECT id FROM events WHERE id = '$event_id'";
$event_check_result = $conn->query($event_check_sql);

if ($event_check_result->num_rows == 0) {
    die("Invalid event ID!");
}

$sql = "INSERT INTO bookings (user_id, event_id) VALUES ('$user_id', '$event_id')";
if ($conn->query($sql)) {
    echo "Ticket booked successfully!";
} else {
    echo "Error: " . $conn->error;
}
?>
  <a href="index.php">BACK MENU</a>  
</body>
</html>
