# XSS against php ```GET``` parameter
## How to run the webserver
- download the files
- ```chmod 700 build-docker.sh```
- ```./build-docker.sh```
- connect to localhost on port 8080 => ```http://localhost:8080/```.....Use Chrome

## How to use website
- copy paste the script tag into each field
- the ```vulnerable field``` allows the script tag to run within the url request
- the ```detect field``` will not allow the script tag to run

## index.html
```
<html>
<body>

<center>

	<h1>XSS vulnerable field / sanitized field POC</h1>
	<h1>Please copy/paste into both fields</h1>
	<h1>
	&lt;Script Language=&quot;Javascript&quot;&gt;alert(&quot;You've been attacked!&quot;);&lt;/Script&gt;
	</h1>

	<form action="get.php" method="GET">
	<label>Vulenrable Field: </label>
	<input type="text" name="vul">
	<input type="submit" value="Submit">
	<input type="reset" value="Reset">
	</form>

	<form action="detect.php" method="GET">
	<label>Detect Field: </label>
	<input type="text" name="detect">
	<input type="submit" value="Submit">
	<input type="reset" value="Reset">
	</form>

</center>

</body>
</html>
```
## get.php => vulnerability
```
<html>
<body>

<?php
$vul = $_GET['vul'];
echo '<div><h1>'.$vul.'This code is vulnerable to XXS</h1></div>';
?>

</body>
</html>
```
- the ```$_GET['vul']``` grabs the value from the index.html form
- the echo command allowed the script tag to run

## detect.php => partial defense/sanitized to XSS 
```
<html>
<body>
<center>
	<h2>Identified invalid URL query string:
	<br/>
        <?php
 	  $detect = htmlentities($_GET['detect'], ENT_QUOTES, 'UTF-8');
          echo '<div>' .$detect.'</div>'
	?>
	<br/>
	Used htmlentities() to sanitize the script tag
        </h2>
</center>
</body>
</html>
```
- ```htmlentities($_GET['detect'], ENT_QUOTES, 'UTF-8');``` escapes all HTML characters in a string and renders the string safe.  
- ```ENT_QUOTES``` was used to encode single quotes

## SYNOPSIS:
I created a website with two forms. The first form is vulnerable to XSS by inputting ```<Script Language="Javascript">alert("You've been attacked!");</Script>```
and the alert window will pop up. An attacke can take advantage of these types of websites and run malicious scripts. To sanitize the input, we added the ```htmlentities($_GET['detect'], ENT_QUOTES, 'UTF-8')```

