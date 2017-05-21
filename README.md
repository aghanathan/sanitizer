# Sanitizer
Sanitize your Login form for more secure

<strong><u>Sanitize $_GET or $_POST parameters to avoid XSS and other attacks</u></strong>

<pre>
// Sanitize $_POST parameters to avoid XSS and other attacks
$user = preg_replace('/[^-a-zA-Z0-9_]/', '', $_POST['username']);
$pass = preg_replace('/[^-a-zA-Z0-9_]/', '', $_POST['password']);

if ($user AND $pass){
	$login = mysqli_query($con,"SELECT * FROM users WHERE username = '$user' AND password = '$pass'");
	$match = mysqli_num_rows($login);
	$r     = mysqli_fetch_array($login);
	mysqli_close($con);
	if ($match > 0){
		session_start();
		$_SESSION[username] = $r[username];
		$_SESSION[password] = $r[password];
		echo "<script>window.location='./secure.php'</script>";
	} else {
		echo "<script>window.alert('wrong username or password');</script>";
	}
}
</pre>
