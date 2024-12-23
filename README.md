# html-calculadora
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculator with Decimal Point</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    .calculator {
      margin-top: 20px;
    }
    .display {
      width: 100%;
      height: 40px;
      margin-bottom: 10px;
      text-align: right;
      padding-right: 10px;
      font-size: 18px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 50px);
      gap: 5px;
      justify-content: center;
    }
    .button {
      width: 50px;
      height: 50px;
      font-size: 18px;
      border: 1px solid #ccc;
      border-radius: 5px;
      cursor: pointer;
    }
    .button:active {
      background-color: #f0f0f0;
    }
  </style>
</head>
<body>
  <h1>Calculadora básica</h1>

  <div class="calculator">
    <input type="text" id="display" class="display" disabled>
    <div class="buttons">
      <button class="button" onclick="addNumber('7')">7</button>
      <button class="button" onclick="addNumber('8')">8</button>
      <button class="button" onclick="addNumber('9')">9</button>
      <button class="button" onclick="setOperator('/')">/</button>
      <button class="button" onclick="addNumber('4')">4</button>
      <button class="button" onclick="addNumber('5')">5</button>
      <button class="button" onclick="addNumber('6')">6</button>
      <button class="button" onclick="setOperator('*')">*</button>
      <button class="button" onclick="addNumber('1')">1</button>
      <button class="button" onclick="addNumber('2')">2</button>
      <button class="button" onclick="addNumber('3')">3</button>
      <button class="button" onclick="setOperator('-')">-</button>
      <button class="button" onclick="addNumber('0')">0</button>
      <button class="button" onclick="addDecimal()">.</button>
      <button class="button" onclick="calculate()">=</button>
      <button class="button" onclick="setOperator('+')">+</button>
      <button class="button" onclick="clearDisplay()">C</button>
    </div>
  </div>

  <script>
    let currentNumber = '';
    let previousNumber = '';
    let operator = null;

    function addNumber(num) {
      currentNumber += num;
      updateDisplay();
    }

    function addDecimal() {
      if (!currentNumber.includes('.')) {
        currentNumber += '.';
        updateDisplay();
      }
    }

    function setOperator(op) {
      if (currentNumber === '') return;
      if (previousNumber !== '') calculate();
      operator = op;
      previousNumber = currentNumber;
      currentNumber = '';
    }

    function calculate() {
      if (!operator || currentNumber === '' || previousNumber === '') return;
      const num1 = parseFloat(previousNumber);
      const num2 = parseFloat(currentNumber);

      let result;
      if (operator === '+') result = num1 + num2;
      if (operator === '-') result = num1 - num2;
      if (operator === '*') result = num1 * num2;
      if (operator === '/') result = num1 / num2;

      currentNumber = result.toString();
      operator = null;
      previousNumber = '';
      updateDisplay();
    }

    function clearDisplay() {
      currentNumber = '';
      previousNumber = '';
      operator = null;
      updateDisplay();
    }

    function updateDisplay() {
      document.getElementById("display").value = currentNumber;
    }
  </script>
</body>
</html>
