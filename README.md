<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Unique Squawk Generator</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f0f4f8;
      text-align: center;
      padding-top: 60px;
    }
    h1 {
      font-size: 28px;
      margin-bottom: 10px;
    }
    #squawk {
      font-size: 36px;
      font-weight: bold;
      margin: 20px 0;
    }
    #remaining {
      margin-bottom: 20px;
      font-size: 18px;
    }
    button {
      font-size: 16px;
      padding: 10px 20px;
      margin: 8px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      background-color: #007bff;
      color: white;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <h1>Unique Squawk Generator</h1>
  <div id="squawk">----</div>
  <div id="remaining">Remaining: 2401 / 2401</div>
  <button onclick="generateSquawk()">Generate</button>
  <button onclick="resetSquawks()">Reset</button>

  <script>
    let allCodes = [];
    const digits = ['1', '2', '3', '4', '5', '6', '7'];
    const totalCodes = Math.pow(7, 4); // 2401

    function generateAllCodes() {
      allCodes = [];
      for (let a of digits) {
        for (let b of digits) {
          for (let c of digits) {
            for (let d of digits) {
              allCodes.push(a + b + c + d);
            }
          }
        }
      }
      shuffle(allCodes);
    }

    function shuffle(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    }

    function generateSquawk() {
      if (allCodes.length === 0) {
        alert("All squawk codes have been used!");
        return;
      }
      const code = allCodes.pop();
      document.getElementById('squawk').textContent = code;
      updateRemaining();
    }

    function resetSquawks() {
      generateAllCodes();
      document.getElementById('squawk').textContent = '----';
      updateRemaining();
    }

    function updateRemaining() {
      document.getElementById('remaining').textContent =
        `Remaining: ${allCodes.length} / ${totalCodes}`;
    }

    // Initialize on page load
    generateAllCodes();
    updateRemaining();
  </script>
</body>
</html>
