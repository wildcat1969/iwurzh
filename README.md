# iwurzh
<html>
<head>
<style>
.error {color: #FF0000;}
</style>
</head>
<body>  

<?php
echo "jekgzxhurhgezhgi";
$servernam="localhost";
$usernam="root";
$passwor="";
$database="fg";


// define variables and set to empty values
$usernameErr = $emailErr = $passworderr="";
$username= $email = $password="";
//new mysqli

$con = mysqli_connect($servernam,$usernam,$passwor,$database) or die(mysqli_error($con));
session_start();



if ($_SERVER["REQUEST_METHOD"] == "POST") {
  if (empty($_POST["username"])) {
    $usernameErr = "Name is required";
  } else {
    $username = test_input($_POST["username"]);
    // check if name only contains letters and whitespace
    if (!preg_match("/^[a-zA-Z-' ]*$/",$username)) {
      $usernameErr = "Only letters and white space allowed";
    }
  }
  
  if (empty($_POST["email"])) {
    $emailErr = "Email is required";
  } else {
    $email = test_input($_POST["email"]);
    // check if e-mail address is well-formed
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
      $emailErr = "Invalid email format";
    }
  }
   if (empty($_POST["password"]))
   {
       $passworderr="password is required";
   }else{
       $password=test_input($_POST["password"]);
       
   }
  
}

function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}
?>

<h2>PHP Form Validation Example</h2>
<p><span class="error">* required field</span></p>
<form method="post" action="index.php">  
  Name: <input type="text" name="username" value="<?php echo $username;?>">
  <span class="error">* <?php echo $usernameErr;?></span>
  <br><br>
  E-mail: <input type="text" name="email" value="<?php echo $email;?>">
  <span class="error">* <?php echo $emailErr;?></span>
  <br><br>
  password:<input type="password" name="password" value="<?php echo $password;?>">
  <span class="error"> *<?php echo $passworderr ;?></span>
  <br><br>
  <input type="submit" name="submit" value="Submit"> 
</form>

<?php

$kt = "insert into t2 (email,username,password) values ('$email', '$username', '$password')";
$yt= mysqli_query($con, $kt) or die(mysqli_error($con));

?>

</body>
</html>
