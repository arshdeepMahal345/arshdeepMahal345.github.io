<?php
// game.php
session_start();
if ( ! isset($_SESSION['who']) ) {
    header('Location: login.php');
    return;
}

$plays = array('Rock','Paper','Scissors');

function checkResult($human, $computer) {
    if ($human == $computer) return "Tie";
    if ($human == "Rock" && $computer == "Scissors") return "You Win";
    if ($human == "Paper" && $computer == "Rock") return "You Win";
    if ($human == "Scissors" && $computer == "Paper") return "You Win";
    return "You Lose";
}

$human = false;
$computer = false;
$result = false;

if ( isset($_POST['play']) ) {
    $human = $_POST['play'];
    if ( in_array($human, $plays) ) {
        $computer = $plays[array_rand($plays)];
        $result = checkResult($human, $computer);
    }
}
?>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Game - 62c880f7</title>
</head>
<body>
<h1>Rock Paper Scissors</h1>
<p>Logged in as: <strong><?php echo htmlspecialchars($_SESSION['who']); ?></strong></p>

<form method="post">
<input type="submit" name="play" value="Rock">
<input type="submit" name="play" value="Paper">
<input type="submit" name="play" value="Scissors">
</form>

<?php
if ( $result !== false ) {
    echo "<p>Your Play=$human Computer Play=$computer Result=$result</p>\n";
}
?>

<p><a href="login.php?logout=1">Log out</a></p>
<p><a href="index.php">Home</a></p>
</body>
</html>
