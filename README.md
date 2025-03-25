<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Input Username dan Password</title>
    <link rel="stylesheet" href="style.css"
</head>
<body>

<h2>Form Input Username dan Password</h2>

<?php
$message = '';
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'];
    $password = $_POST['password'];
    $isValid = true;

    
    if (strlen($username) > 7) {
        $message .= 'Username tidak boleh lebih dari 7 karakter.<br>';
        $isValid = false;
    }

    
    $passwordRegex = '/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{10,}$/';
    if (!preg_match($passwordRegex, $password)) {
        $message .= 'Password harus terdiri dari huruf kapital, huruf kecil, angka, dan karakter khusus, serta minimal 10 karakter.<br>';
        $isValid = false;
    }

    
    if ($isValid) {
        $message = 'Form berhasil disubmit!';
        
    }
}
?>

<form method="post" action="">
    <label for="username">Username (max 7 karakter):</label><br>
    <input type="text" id="username" name="username" required><br><br>
    
    <label for="password">Password (min 10 karakter, harus ada huruf kapital, huruf kecil, angka, dan karakter khusus):</label><br>
    <input type="password" id="password" name="password" required><br><br>
    
    <input type="submit" value="Submit">
</form>

<p class="error"><?php echo $message; ?></p>

</body>
</html>
