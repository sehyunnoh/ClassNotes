## localStorage.js
```js
function saveData() {
  for (let x = 1; x <= 2; x++) {
    localStorage.setItem(`sname${x}`,document.getElementById(`sname${x}`).value);
    document.getElementById("select").innerHTML += `<option>${
      document.getElementById(`sid${x}`).value
    }</option>`;
  } 
} 

function makeReport() {
  let current = document.getElementById("select").value;
  for (let key in localStorage) {
    if (localStorage.getItem(key) == current) {
      let lastChar = key.substr(key.length - 1);
      document.getElementById("outid").value = localStorage.getItem(`sid${lastChar}`);
      let scholarship = parseFloat(localStorage.getItem(`scholarship${lastChar}`));
    }
  }
} 

function printData() { window.print();}
```