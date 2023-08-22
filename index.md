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

// Expiry for cookies: 30 days
  let d = new Date();
  d.setTime(d.getTime() + 1000*60*60*24*30);
  console.log("UTC Time: " + d.toUTCString());
  let suffix = "\; expires=" + d.toUTCString() + "\; path=/";

// Load cookies and fill up text boxes
  let cooks = readCookie();
  if (cooks != null) 
  {
  cooks.forEach(function(cook)
  {
    let key = cook.substring(0, cook.indexOf('='));
    let val = cook.substring(cook.indexOf('=') + 1);

    console.log("Key: " + key);

    document.getElementById(key).value = val;
  });
  }

  Array.from(inputs).some(function(input) {
    if(!input.value)
    {
      input.focus();
      return true;
    }
  });
  console.log("Starting cookie: " + document.cookie);

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



  // Save to cookies before unloading
  window.addEventListener('beforeunload', function(){
    writeCookie("accBal", document.getElementById("accBal").value);
    writeCookie("riskPercentage", document.getElementById("riskPercentage").value);

    console.log("Final cookie: " + document.cookie);
  });

  // Add a value to the cookie
  function writeCookie(key, value){

    document.cookie = key + "=" + value + suffix;
  }

  // Read a value from the cookie
  function readCookie(){

    let decookie = decodeURIComponent(document.cookie);
    value = decookie.split('\; ');

    return value[0] == "" ? null : value;
  }

</script>
