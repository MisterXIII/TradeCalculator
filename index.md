---
layout: default
---

# Stop Loss Calculator

This is to help you calculate the _____

| Account Balance | Stop Loss Size    | Risk Percentage |
|:----------------|:------------------|:----------------|
| <input class="query" type="text" id="accBal" name="accBal" placeholder="Enter Account Balance">           | <input class="query" type="text" id="stopLoss" name="stopLoss" placeholder="Enter Stop Loss"> | <input class="query" type="text" id="riskPercentage" name="riskPercentage" placeholder="Enter Risk Percentage">  |
<br>
<p id="output"></p>
<br>

<script>

  let inputs = document.querySelector(".query")

  inputs.forEach(function(input) {
    input.addEventListener('input', function() {
      let accBal = document.getElementById("accBal");
      let stopLoss = document.getElementById("stopLoss");
      let riskPercentage = document.getElementById("riskPercentage");

      output.textContent = riskPercentage * accBal / (stopLoss * 1000);
    })
  });

</script>
