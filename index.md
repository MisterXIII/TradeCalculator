---
layout: default
---

# Lot Size Calculator

This is to help you calculate the _____

<table id="mainTable">
</table>

### Lot Size:
<p id="output"></p>

<script>
  
  let inputs = document.querySelectorAll(".query")

  let output = document.getElementById("output")

  // Mobile or Desktop screen?
  let desktopScreen = window.innerWidth > 768;
  drawTable();

// Expiry for cookies: 30 days
  let d = new Date();
  d.setTime(d.getTime() + 1000*60*60*24*30);
  console.log("Expiry time in UTC: " + d.toUTCString());
  let suffix = "\; expires=" + d.toUTCString() + "\; path=/";


  // LOG: Starting cookie
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

  // Adjust table if resized
  window.addEventListener('resize', function() {

    if((desktopScreen && window.innerWidth <= 768) || (!desktopScreen && window.innerWidth > 768)) {
      desktopScreen = window.innerWidth > 768;
      drawTable();
    }
  });


    
  // Window resize
  function drawTable(){
    if (window.innerWidth <= 768){
      mainTable.innerHTML = `
      <tr>
        <th>Account Balance</th>
      </tr>
      <tr>
        <td>
          <input type="number" class="query" id="accBal" name="accBal" placeHolder="Add Acount Balance">
        </td>
      </tr>
      <tr>
        <th>Risk Percentage</th>
      </tr>
      <tr>
        <td>
          <input type="number" class="query" id="riskPercentage" name="riskPercentage" placeHolder="Add Risk Percentage">
        </td>
      </tr>
      <tr>
        <th>Stop Loss</th>
      </tr>
      <tr>
        <td>
          <input type="number" class="query" id="stopLoss" name="stopLoss" placeHolder="Add Stop Loss">
        </td>
      </tr>`



    } else {
      mainTable.innerHTML = `
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
  </tr>`
    }
  }

// Load cookies and fill up text boxes
function fillText() {
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
}

// Set focus to the first unfilled text box
function focusInput()
{
  Array.from(inputs).some(function(input) {
    if(!input.value)
    {
      input.focus();
      return true;
    }
  });
}

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
