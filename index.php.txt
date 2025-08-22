<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Syntego | Login</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
    }

    body {
      background-color: #121212;
      color: #ffffff;
      display: flex;
      min-height: 100vh;
    }

    .sidebar {
      width: 220px;
      background-color: #1f1f1f;
      padding: 40px 20px;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    .sidebar a {
      color: #ccc;
      text-decoration: none;
      font-size: 16px;
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px;
      border-radius: 8px;
      transition: background 0.3s;
    }

    .sidebar a:hover {
      background-color: #2a2a2a;
      color: #fff;
    }

    .container {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .login-card {
      background-color: #1e1e1e;
      padding: 40px;
      border-radius: 16px;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 0 20px rgba(255, 0, 0, 0.2);
    }

    .login-card h1 {
      font-size: 32px;
      color: #fff;
    }

    .login-card p {
      font-size: 14px;
      color: #aaa;
      margin-bottom: 30px;
    }

    .tabs {
      display: flex;
      gap: 20px;
      margin-bottom: 30px;
    }

    .tab {
      cursor: pointer;
      color: #aaa;
      border-bottom: 2px solid transparent;
      padding-bottom: 6px;
    }

    .tab.active {
      color: #ff4c4c;
      border-color: #ff4c4c;
    }

    .input-group {
      position: relative;
      margin-bottom: 20px;
    }

    .input-group input {
      width: 100%;
      padding: 12px 40px 12px 12px;
      background-color: #2a2a2a;
      border: 1px solid #444;
      border-radius: 8px;
      color: #fff;
      transition: 0.3s;
    }

    .input-group input:invalid {
      border-color: #ff4c4c;
    }

    .input-group .eye-icon {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      font-size: 16px;
      color: #aaa;
    }

    .login-btn {
      width: 100%;
      padding: 12px;
      background: #ff4c4c;
      border: none;
      color: #fff;
      border-radius: 8px;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s ease;
      box-shadow: 0 0 10px rgba(255, 76, 76, 0.3);
    }

    .login-btn:hover {
      background: #ff6666;
      box-shadow: 0 0 15px rgba(255, 100, 100, 0.5);
    }

    @media (max-width: 768px) {
      .sidebar {
        display: none;
      }

      .container {
        padding: 10px;
      }

      .login-card {
        padding: 30px 20px;
      }
    }
  </style>
</head>
<body>

  <div class="sidebar">
    <a href="#"><span>🏠</span> Home</a>
    <a href="#"><span>➕</span> Transaction Log</a>
    <a href="#"><span>📘</span> View Expenses</a>
    <a href="#"><span>📊</span> Report</a>
  </div>

  <div class="container">
    <div class="login-card">
      <h1>Syntego</h1>
      <p>An AI-powered finance tracker.</p>

      <div class="tabs">
        <div class="tab active" onclick="activateTab(this)">Login</div>
        <div class="tab" onclick="activateTab(this)">Register</div>
      </div>

      <form>
        <div class="input-group">
          <input type="email" placeholder="Email" required />
        </div>
        <div class="input-group">
          <input type="password" id="password" placeholder="Password" required />
          <span class="eye-icon" onclick="togglePassword()">👁️</span>
        </div>
        <button type="submit" class="login-btn">Login</button>
      </form>
    </div>
  </div>

  <script>
    function togglePassword() {
      const passwordField = document.getElementById("password");
      const type = passwordField.getAttribute("type") === "password" ? "text" : "password";
      passwordField.setAttribute("type", type);
    }

    function activateTab(tab) {
      document.querySelectorAll('.tab').forEach(el => el.classList.remove('active'));
      tab.classList.add('active');
    }
  </script>

</body>
</html>
<?php
session_start();

$questions = [
    "What is the capital of France?" => "Paris",
    "2 + 2 = ?" => "4",
    "Which language runs in a web browser?" => "JavaScript"
];

$score = 0;
$message = "";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    foreach ($questions as $q => $answer) {
        if (isset($_POST[$q]) && strtolower($_POST[$q]) == strtolower($answer)) {
            $score++;
        }
    }
    $_SESSION['score'] = $score;
    $message = "You scored $score / " . count($questions) . " 🎉";
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>PHP Quiz</title>
    <style>
        body { font-family: Arial; background: #f3f4f6; display: flex; justify-content: center; align-items: center; height: 100vh; }
        .quiz { background: white; padding: 20px; border-radius: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); width: 400px; }
        h2 { color: #2563eb; }
        input[type="text"] { width: 90%; padding: 8px; margin: 10px 0; }
        input[type="submit"] { background: #2563eb; color: white; border: none; padding: 10px; border-radius: 6px; cursor: pointer; }
        .message { margin-top: 15px; color: #16a34a; font-weight: bold; }
    </style>
</head>
<body>
<div class="quiz">
    <h2>Simple PHP Quiz</h2>
    <form method="post">
        <?php foreach ($questions as $q => $answer): ?>
            <p><?= $q ?></p>
            <input type="text" name="<?= $q ?>" required>
        <?php endforeach; ?>
        <br>
        <input type="submit" value="Submit Answers">
    </form>
    <?php if ($message): ?>
        <div class="message"><?= $message ?></div>
    <?php endif; ?>
</div>
</body>
</html>
