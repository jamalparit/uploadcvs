We can upload excel sheet data to mysql database table using php that is very simple. 
For that you have to follow the following steps.

If you follow the below steps end of the this blog you achieve the target.

1. First you have to create mysql database.
EX:create database import_exceldata

2. Create table in your choosen database.

EX: CREATE TABLE IF NOT EXISTS `mytask` (
`id` int(11) NOT NULL AUTO_INCREMENT,
`name` varchar(11) COLLATE utf8_unicode_ci NOT NULL,
`project` varchar(11) COLLATE utf8_unicode_ci NOT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=15 ;

3.create your php excelsheet data uploading file.
EX:import_excel.php

write code in that file(import_excel.php)
—————————————————————
<?php
$hostname = “localhost”;
$username = “root”;
$password = “”;
$database = “import_exceldata”;
$conn = mysql_connect(“$hostname”,”$username”,”$password”) or die(mysql_error());
mysql_select_db(“$database”, $conn) or die(mysql_error());
?>
<html>
<head>
<style type=”text/css”>
body
{
margin: 0;
padding: 0;
background-color:#FFFFFF;
text-align:center;
}
.top-bar
{
width: 100%;
height: auto;
text-align: center;
background-color:#FFF;
border-bottom: 1px solid #000;
margin-bottom: 20px;
}
.inside-top-bar
{
margin-top: 5px;
margin-bottom: 5px;
}
.link
{
font-size: 18px;
text-decoration: none;
background-color: #000;
color: #FFF;
padding: 5px;
}
.link:hover
{
background-color: #FCF3F3;
}
</style>

</head>
<body>
<div class=”top-bar”>
<div class=”inside-top-bar”>Import Excelsheet Data in mysql table<br><br>
</div>
</div>
<div style=”text-align:left; border:1px solid #333333; width:300px; margin:0 auto; padding:10px;”>

<form name=”import” method=”post” enctype=”multipart/form-data”>
<input type=”file” name=”file” /><br />
<input type=”submit” name=”submit” value=”Submit” />
</form>
<?php
if(isset($_POST[“submit”]))
{
$file = $_FILES[‘file’][‘tmp_name’];
$handle = fopen($file, “r”);
$c = 0;
while(($filesop = fgetcsv($handle, 1000, “,”)) !== false)
{
$name = $filesop[0];
$project = $filesop[1];

$sql = mysql_query(“INSERT INTO mytask (name, project) VALUES (‘$name’,’$project’)”);
$c = $c + 1;
}

if($sql){
echo “You database has imported successfully. You have inserted “. $c .” recoreds”;
}else{
echo “Sorry! There is some problem.”;
}

}
?>
</div>
</body>
</html>