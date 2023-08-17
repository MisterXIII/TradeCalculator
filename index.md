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
    <td>
      <input class="query" type="number" id="accBal" name="accBal" placeholder="Enter Account Balance" min="0">
    </td>
    <td>
      <input class="query" type="number" id="stopLoss" name="stopLoss" placeholder="Enter Stop Loss" min="0">
    </td>
    <td>
      <input class="query" type="number" id="riskPercentage" name="riskPercentage" placeholder="Enter Risk Percentage" min="0">
    </td>
  </tr>
</table>

### Stop Loss Size:
<p id="output"></p>

<script>

  let inputs = document.querySelectorAll(".query")

  let output = document.getElementById("output")

  inputs.forEach(function(input) {
    input.addEventListener('input', function() {
      let accBal = parseInt(document.getElementById("accBal").value);
      let stopLoss = parseInt(document.getElementById("stopLoss").value);
      let riskPercentage = parseInt(document.getElementById("riskPercentage").value);

      if(accBal && stopLoss>0 && riskPercentage>0)
      {
        output.textContent = riskPercentage * accBal / (stopLoss * 1000);
      } else
      {
        output.textContent = ''
      }
    })
  });

  function writeCookie(){

  }

  function readCookie(){
    
  }

</script>
