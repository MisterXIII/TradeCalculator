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
      <input class="query" type="number" id="accBal" name="accBal" onload="this.textContent=readCookie(this.id);" onunload="writeCookie(this.id, this.value)" placeholder="Enter Account Balance" min="0">
    </td>
    <td>
      <input class="query" type="number" id="riskPercentage" name="riskPercentage" onload="this.textContent=readCookie(this.id);" onunload="writeCookie(this.id, this.value)" placeholder="Enter Risk Percentage" min="0">
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

  // Update anytime the textboxes are updated
  inputs.forEach(function(input) {
    input.addEventListener('input', function() {

      // Do the math
      let accBal = parseInt(document.getElementById("accBal").value);
      let stopLoss = parseInt(document.getElementById("stopLoss").value);
      let riskPercentage = parseInt(document.getElementById("riskPercentage").value);

      if(accBal>0 && stopLoss>0 && riskPercentage>0)
      {
        output.textContent = riskPercentage * accBal / (stopLoss * 1000);
      } else
      {
        output.textContent = ''
      }
    })
  });

  // Add a value to the cookie
  function writeCookie(key, value){
    if(readCookie(key))
    {
      deleteCookie(key);
    }
    document.cookie += key + "=" + value + ";";
  }

  // Remove a value from the cookie
  function deleteCookie(key) {
    if(document.cookie.search(key) == -1)
    {
      return;
    }

    let st = document.cookie.indexOf(key);
    let ed = document.cookie.indexOf(";", st);

    document.cookie = document.cookie.substr(0, st) + document.cookie.substr(ed + 1);



  }

  // Clear the cookie
  function clearCookie(){
    document.cookie = "";
  }

  // Read a value from the cookie
  function readCookie(key){
    let ind = document.cookie.indexOf(key);
    if(ind == -1)
    {
      return "";
    }

    return document.cookie.substr(document.cookie.indexOf("=", ind) + 1, document.cookie.indexOf(";", ind));
  }

</script>
