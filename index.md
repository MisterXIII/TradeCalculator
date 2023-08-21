---
layout: default
---

# Stop Loss Calculator

This is to help you calculate the _____

<table>
  <tr>
    <th>Account Balance</th>
    <th>Risk Percentage</th>
    <th>Stop Loss</th>
  </tr>
  <tr>
    <td>
      <input class="query" type="number" id="accBal" name="accBal" placeholder="Enter Account Balance" min="0">
    </td>
    <td>
      <input class="query" type="number" id="riskPercentage" name="riskPercentage" placeholder="Enter Risk Percentage" min="0">
    </td>
    <td>
      <input class="query" type="number" id="stopLoss" name="stopLoss" placeholder="Enter Stop Loss" min="0">
    </td>
  </tr>
</table>

### Stop Loss Size:
<p id="output"></p>

<script>

  let inputs = document.querySelectorAll(".query")

  let output = document.getElementById("output")

  let suffix = "\; ";


  // Update anytime the textboxes are updated
  inputs.forEach(function(input) {
    input.addEventListener('input', function() {

      // Do the math
      let accBal = parseInt(document.getElementById("accBal").value);
      let riskPercentage = parseInt(document.getElementById("riskPercentage").value);
      let stopLoss = parseInt(document.getElementById("stopLoss").value);

      if(accBal>0 && riskPercentage>0 && stopLoss>0)
      {
        output.textContent = riskPercentage * accBal / (stopLoss * 1000);
      } else
      {
        output.textContent = '';
      }
    })
  });

  // Read cookies when loading
  window.addEventListener('load', function() {
    let cooks = readCookie();
    cooks.forEach(function(cook)
    {
      let key = cook.substring(0, cook.indexOf('='));
      let val = cook.substring(cook.indexOf('=') + 1);

      document.getElementById(key).value = val;
    })
    console.log("Starting cookie: " + document.cookie);
  });


  // Save to cookies before unloading
  window.addEventListener('unload', function(){
    clearCookie();
    writeCookie("accBal", document.getElementById("accBal").value);
    writeCookie("riskPercentage", document.getElementById("riskPercentage").value);

    console.log("Final cookie: " + document.cookie);
  });

  // Add a value to the cookie
  function writeCookie(key, value){
    document.cookie = key + "=" + value;
  }

  // Clear the cookie
  function clearCookie(){
    document.cookie = "";
  }

  // Read a value from the cookie
  function readCookie(){

    let decookie = decodeURIComponent(document.cookie);
    value = decookie.split('\; ');

    return value;
  }

</script>
