---
layout: default
---

# Lot Size Calculator

This is to help you calculate the Lot Size

<table id="mainTable">
</table>

### Lot Size:
<p id="output"></p>

<script>
  let cookies = initCookies();
  
  // Initialize input boxes
  let accBalInput = document.createElement("input");
  accBalInput.id = "accBal";
  accBalInput.placeholder = "Enter Account Balance";

  let riskPercentageInput = document.createElement("input");
  riskPercentageInput.id = "riskPercentage";
  riskPercentageInput.placeholder = "Enter Risk Percentage";

  let stopLossInput = document.createElement("input");
  stopLossInput.id = "stopLoss";
  stopLossInput.placeholder = "Enter Stop Loss";

  let inputs = [accBalInput, riskPercentageInput, stopLossInput];

  inputs.forEach(function(input) {
    input.type= "number";
    input.min = "0";
    input.value = cookies.get(input.id);
  })

  let output = document.getElementById("output");

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

  Array.of(accBalInput, riskPercentageInput).forEach(function(input) {
      // Save to cookie
      input.addEventListener('input', function() {writeCookie(input.id, document.getElementById(input.id).value);});
  });

  // Update anytime the textboxes are updated
  inputs.forEach(function(input) {
    input.addEventListener('input', function() {


      // Do the math
      let accBal = parseFloat(document.getElementById("accBal").value);
      let riskPercentage = parseFloat(document.getElementById("riskPercentage").value);
      let stopLoss = parseFloat(document.getElementById("stopLoss").value);

      if(accBal>0 && riskPercentage>0 && stopLoss>0)
      {
        output.textContent = riskPercentage * accBal / (stopLoss * 1000);
      } else
      {
        output.textContent = '';
      }
    })
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
        <td id="accBalD">
        </td>
      </tr>
      <tr>
        <th>Risk Percentage</th>
      </tr>
      <tr>
        <td id="riskPercentageD">
        </td>
      </tr>
      <tr>
        <th>Stop Loss</th>
      </tr>
      <tr>
        <td id="stopLossD">
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
    <td id="accBalD">
    </td>
    <td id="riskPercentageD">
    </td>
    <td id="stopLossD">
    </td>
  </tr>`
    }

    document.getElementById("accBalD").appendChild(accBalInput);
    document.getElementById("riskPercentageD").appendChild(riskPercentageInput);
    document.getElementById("stopLossD").appendChild(stopLossInput);

    focusInput();
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

  // Inititialize a map of cookies
  function initCookies(){

    let decookie = decodeURIComponent(document.cookie);
    let pairs = decookie.split('\; ');

    let value = new Map();
    pairs.forEach(function(cookie){
      value.set(cookie.substring(0, cookie.indexOf('=')), cookie.substring(cookie.indexOf('=') + 1));
    })

    return value;
  }

</script>
