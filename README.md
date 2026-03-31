# Ai
<!DOCTYPE html>
<html>
<head>
  <title>AI Betting Analyzer</title>
  <style>
    body {
      background: #0f0f1a;
      color: white;
      font-family: Arial;
      text-align: center;
    }

    h1 {
      color: #00ffe1;
    }

    input {
      padding: 10px;
      margin: 5px;
      width: 50px;
      font-size: 18px;
      text-align: center;
      border-radius: 10px;
      border: none;
    }

    button {
      padding: 12px 25px;
      margin-top: 20px;
      border: none;
      border-radius: 25px;
      background: #00ffe1;
      color: black;
      font-size: 18px;
      cursor: pointer;
    }

    #result {
      margin-top: 30px;
      font-size: 22px;
      font-weight: bold;
    }
  </style>
</head>

<body>

<h1>AI Betting Analyzer</h1>

<p>Enter Last 5 Numbers</p>

<input type="number" id="n1">
<input type="number" id="n2">
<input type="number" id="n3">
<input type="number" id="n4">
<input type="number" id="n5">

<br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

<script>
function analyze() {
  let nums = [
    Number(n1.value),
    Number(n2.value),
    Number(n3.value),
    Number(n4.value),
    Number(n5.value)
  ];

  let types = nums.map(n => n >= 5 ? "B" : "S");

  let score = 0;

  // Trend detection
  for (let i = 1; i < types.length; i++) {
    if (types[i] === types[i-1]) score++;
    else score--;
  }

  // Momentum
  let last = types[types.length - 1];
  let sameCount = types.filter(t => t === last).length;

  if (sameCount >= 3) score += 2;

  // Randomness check
  let changes = 0;
  for (let i = 1; i < types.length; i++) {
    if (types[i] !== types[i-1]) changes++;
  }

  if (changes >= 3) score -= 2;

  let result = "";

  if (score >= 2) {
    result = "🔥 HIGH CHANCE: " + (last === "B" ? "BIG" : "SMALL");
  } else if (score <= -2) {
    result = "🔥 HIGH CHANCE: " + (last === "B" ? "SMALL" : "BIG");
  } else {
    result = "⚠️ SKIP (No clear pattern)";
  }

  document.getElementById("result").innerText = result;
}
</script>

</body>
</html>
