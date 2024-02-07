# Chenoa 2024, for CSSA UdeM 2024 Chinese New Year event
## Based on html

### Base version
```html
<!DOCTYPE html>
<html lang="en">
<!--Chenoa, opensource Github liuchen37-->
<!--version 2b: Update disabled botton appearance-->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Random Draw App</title>
  <style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100vh;
    background-color: #FF3300;
    color: #FFF143;
  }

  h2 {
    font-size: 2em;
    margin: 0.5em 0;
    line-height: 1.2;
  }

  button {
    font-size: 1.5em;
    margin: 10px;
    padding: 10px 20px;
    background-color: #FFF;
    color: #FF3300;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #E62E00;
  }

  p {
    font-size: 1.2em;
    margin: 5px 0;
  }

  #firstPrize, #secondPrize, #participationPrizes {
    margin-bottom: 20px;
  }

  .prize-container {
    margin-top: 20px;
  }
    
    
    /* Updated style for disabled button */
    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

<div class="container">
  <h2>Joyeux Nouvel An chinois !</h2>
  <h2>中国新年快乐！</h2>

  <div class="prize-container">
    <button onclick="drawFirstPrize()">1er prix / 一等奖</button>
    <p id="firstPrize"></p>
  </div>

  <div class="prize-container">
    <button onclick="drawSecondPrize()">2ème prix / 二等奖</button>
    <p id="secondPrize"></p>
  </div>

  <div class="prize-container">
    <button onclick="drawParticipationRewards()">Prix de participation / 参与奖</button>
    <p id="participationPrizes"></p>
  </div>
</div>

<script>
const localNumberRanges = {
  '1-A': 100,
  '1-B': 35,
  '1-C': 96,
  '2-A': 100,
  '2-B': 100,
  '2-C': 100
};

function generateTicketNumber(exclude = []) {
  let ticketNumber;
  do {
    const levelNumber = Math.floor(Math.random() * 2) + 1; // 1 or 2
    const areaCodes = ['A', 'B', 'C'];
    const areaCode = areaCodes[Math.floor(Math.random() * areaCodes.length)];
    const maxLocalNumber = localNumberRanges[`${levelNumber}-${areaCode}`];
    const localNumber = Math.floor(Math.random() * maxLocalNumber) + 1; // 1 to maxLocalNumber
    ticketNumber = `${levelNumber}-${areaCode}-${localNumber.toString().padStart(3, '0')}`;
  } while (exclude.includes(ticketNumber)); // Ensure the ticket hasn't already been drawn
  return ticketNumber;
}

function drawPrizes(prizeCount, preventDuplicates = false) {
  let winners = [];
  let drawnTickets = [];

  for (let i = 0; i < prizeCount; i++) {
    let ticketNumber = generateTicketNumber(preventDuplicates ? drawnTickets : []);
    winners.push(ticketNumber);
    drawnTickets.push(ticketNumber); // Keep track of the drawn ticket
  }
  
  return winners;
}

function drawFirstPrize() {
  const firstPrize = drawPrizes(1);
  document.getElementById('firstPrize').textContent = `1st Prize: ${firstPrize}`;
}

function drawSecondPrize() {
  const secondPrize = drawPrizes(1);
  document.getElementById('secondPrize').textContent = `2nd Prize: ${secondPrize}`;
}

function drawParticipationRewards() {
  const participationWinners = drawPrizes(50, true); // Ensure unique winners
  document.getElementById('participationPrizes').textContent = `Participation Rewards: ${participationWinners.join(', ')}`;
}

// Update the draw functions to disable buttons
function drawFirstPrize() {
  const firstPrize = drawPrizes(1);
  document.getElementById('firstPrize').textContent = `1st Prize: ${firstPrize}`;
  document.querySelector("button[onclick='drawFirstPrize()']").disabled = true;
}

function drawSecondPrize() {
  const secondPrize = drawPrizes(1);
  document.getElementById('secondPrize').textContent = `2nd Prize: ${secondPrize}`;
  document.querySelector("button[onclick='drawSecondPrize()']").disabled = true;
}

function drawParticipationRewards() {
  const participationWinners = drawPrizes(50, true); // Ensure unique winners
  document.getElementById('participationPrizes').textContent = `Participation Rewards: ${participationWinners.join(', ')}`;
  document.querySelector("button[onclick='drawParticipationRewards()']").disabled = true;
}
</script>

</body>
</html>
```

### 1st and 2nd prizes only, with background
```html
<!DOCTYPE html>
<html lang="en">
<!--Chenoa, opensource Github liuchen37-->
<!--version 3.2a: 1st and 2nd prize only, updated appearances-->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>1st and 2nd Prizes Draw App</title>
<style>
body {
      background-image: url('https://github.com/liuchen37/Pics/blob/main/randomdrawbkgd.jpg?raw=true');
      background-size: cover; /* Cover the entire page */
      background-position: center; /* Center the image */
      background-repeat: no-repeat; /* Do not repeat the image */
      font-family: Arial, sans-serif;
      text-align: center;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      height: 100vh;
    }

  h2 {
    font-size: 2em;
    margin: 0.5em 0;
    line-height: 1.2;
  }

  button {
    font-size: 1.5em;
    margin: 10px;
    padding: 10px 20px;
    background-color: #FFF;
    color: #FF3300;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #E62E00;
  }

  p {
    font-size: 1.2em;
    margin: 5px 0;
  }

  /* Specific styles for the winning ticket numbers */
  #firstPrize, #secondPrize {
    color: yellow; /* Sets the text color to yellow */
  }

.container {
    color: #FF6666; /* light red */
    font-size: 1.5em; /* increases the text size */
  }

  .container h2 {
    font-size: 2em; /* even larger size for headings */
    /* Any other specific styles for h2 elements inside .container */
  }

  .prize-container {
    margin-top: 20px;
  }
    
    
    /* Updated style for disabled button */
    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

<div class="container">
  <h2>Joyeux Nouvel An chinois !</h2>
  <h2>中国新年快乐！</h2>

  <div class="prize-container">
    <button onclick="drawFirstPrize()">1er prix / 一等奖</button>
    <p id="firstPrize"></p>
  </div>

  <div class="prize-container">
    <button onclick="drawSecondPrize()">2ème prix / 二等奖</button>
    <p id="secondPrize"></p>
  </div>
</div>

<script>
const localNumberRanges = {
  '1-A': 100,
  '1-B': 35,
  '1-C': 96,
  '2-A': 100,
  '2-B': 100,
  '2-C': 1
};

function generateTicketNumber(exclude = []) {
  let ticketNumber;
  do {
    const levelNumber = Math.floor(Math.random() * 2) + 1; // 1 or 2
    const areaCodes = ['A', 'B', 'C'];
    const areaCode = areaCodes[Math.floor(Math.random() * areaCodes.length)];
    const maxLocalNumber = localNumberRanges[`${levelNumber}-${areaCode}`];
    const localNumber = Math.floor(Math.random() * maxLocalNumber) + 1; // 1 to maxLocalNumber
    ticketNumber = `${levelNumber}-${areaCode}-${localNumber.toString().padStart(3, '0')}`;
  } while (exclude.includes(ticketNumber)); // Ensure the ticket hasn't already been drawn
  return ticketNumber;
}

function drawPrizes(prizeCount, preventDuplicates = false) {
  let winners = [];
  let drawnTickets = [];

  for (let i = 0; i < prizeCount; i++) {
    let ticketNumber = generateTicketNumber(preventDuplicates ? drawnTickets : []);
    winners.push(ticketNumber);
    drawnTickets.push(ticketNumber); // Keep track of the drawn ticket
  }
  
  return winners;
}

function drawFirstPrize() {
  const firstPrize = drawPrizes(1);
  document.getElementById('firstPrize').textContent = `1st Prize: ${firstPrize}`;
}

function drawSecondPrize() {
  const secondPrize = drawPrizes(1);
  document.getElementById('secondPrize').textContent = `2nd Prize: ${secondPrize}`;
}

// Update the draw functions to disable buttons
function drawFirstPrize() {
  const firstPrize = drawPrizes(1);
  document.getElementById('firstPrize').textContent = `1st Prize: ${firstPrize}`;
  document.querySelector("button[onclick='drawFirstPrize()']").disabled = true;
}

function drawSecondPrize() {
  const secondPrize = drawPrizes(1);
  document.getElementById('secondPrize').textContent = `2nd Prize: ${secondPrize}`;
  document.querySelector("button[onclick='drawSecondPrize()']").disabled = true;
}

</script>

</body>
</html>
```
### Participation prizes only, with background
```html
<!DOCTYPE html>
<html lang="en">
<!--Chenoa, opensource Github liuchen37-->
<!--version 3.2b: participation prize only, updated appearances-->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Participation Prizes Draw App</title>
<style>
body {
      background-image: url('https://github.com/liuchen37/Pics/blob/main/randomdrawbkgd.jpg?raw=true');
      background-size: cover; /* Cover the entire page */
      background-position: center; /* Center the image */
      background-repeat: no-repeat; /* Do not repeat the image */
      font-family: Arial, sans-serif;
      text-align: center;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      height: 100vh;
    }

  h2 {
    font-size: 2em;
    margin: 0.5em 0;
    line-height: 1.2;
  }

  button {
    font-size: 1.5em;
    margin: 10px;
    padding: 10px 20px;
    background-color: #FFF;
    color: #FF3300;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #E62E00;
  }

  p {
    font-size: 1.2em;
    margin: 5px 0;
  }

  #participationPrizes {
    color: yellow; /* Sets the text color to yellow */
  }

.container {
    color: #FF6666; /* light red */
    font-size: 1.5em; /* increases the text size */
  }

  .prize-container {
    margin-top: 20px;
  }
    
    
    /* Updated style for disabled button */
    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

<div class="container">
  <h2>Joyeux Nouvel An chinois !</h2>
  <h2>中国新年快乐！</h2>

  <div class="prize-container">
    <button onclick="drawParticipationRewards()">Prix de participation / 参与奖</button>
    <p id="participationPrizes"></p>
  </div>
</div>

<script>
const localNumberRanges = {
  '1-A': 100,
  '1-B': 35,
  '1-C': 96,
  '2-A': 100,
  '2-B': 100,
  '2-C': 100
};

function generateTicketNumber(exclude = []) {
  let ticketNumber;
  do {
    const levelNumber = Math.floor(Math.random() * 2) + 1; // 1 or 2
    const areaCodes = ['A', 'B', 'C'];
    const areaCode = areaCodes[Math.floor(Math.random() * areaCodes.length)];
    const maxLocalNumber = localNumberRanges[`${levelNumber}-${areaCode}`];
    const localNumber = Math.floor(Math.random() * maxLocalNumber) + 1; // 1 to maxLocalNumber
    ticketNumber = `${levelNumber}-${areaCode}-${localNumber.toString().padStart(3, '0')}`;
  } while (exclude.includes(ticketNumber)); // Ensure the ticket hasn't already been drawn
  return ticketNumber;
}

function drawPrizes(prizeCount, preventDuplicates = false) {
  let winners = [];
  let drawnTickets = [];

  for (let i = 0; i < prizeCount; i++) {
    let ticketNumber = generateTicketNumber(preventDuplicates ? drawnTickets : []);
    winners.push(ticketNumber);
    drawnTickets.push(ticketNumber); // Keep track of the drawn ticket
  }
  
  return winners;
}

function drawParticipationRewards() {
  const participationWinners = drawPrizes(50, true); // Ensure unique winners
  document.getElementById('participationPrizes').textContent = `Participation Rewards: ${participationWinners.join(', ')}`;
}

// Update the draw functions to disable buttons
function drawParticipationRewards() {
  const participationWinners = drawPrizes(50, true); // Ensure unique winners
  document.getElementById('participationPrizes').textContent = `Participation Rewards: ${participationWinners.join(', ')}`;
  document.querySelector("button[onclick='drawParticipationRewards()']").disabled = true;
}
</script>

</body>
</html>
```

# *Bon nouvel an chinois!*
