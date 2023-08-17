---
layout: default
---

# Stop Loss Calculator

This is to help you calculate the _____

<table>
  <tr>
    <th>Account Balance</th>
    <th>Stop Loss</th>
    <th>Risk Percentage</th>
  </tr>
  <tr>
    <th>
      <input class="query" type="text" id="accBal" name="accBal" placeholder="Enter Account Balance">
    </th>
    <th>
      <input class="query" type="text" id="stopLoss" name="stopLoss" placeholder="Enter Stop Loss">
    </th>
    <th>
      <input class="query" type="text" id="riskPercentage" name="riskPercentage" placeholder="Enter Risk Percentage">
    </th>
  <tr>
</table>


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
