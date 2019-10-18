## always include a viewport meta for responsive design

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

## Finding Nodes

```js
getElementById("id");
getElementByTagName("tag");
getElementsByClassName("className");
```

## Updating Nodes

```js
document.getElementById("id").style.color = "blue";
document.getElementById("id").innerHTML = "Hello";
document.formName.inputName.value = "Hello";
elem = document.getElementByTagName("p");
for (xx = 0; xx < elem.length; xx++) {
  elem[xx].innerHTML = "Para Data";
}
```

## main.css

```css
.exGrid {
  display: grid;
  grid-template-columns: 2fr 2fr 3fr 3fr;
  grid-template-rows: auto;
  grid-gap: 2px;
  grid-template-areas:
    "exHead exHead exHead exHead"
    "exCampus exValues exGPA exGPAOut"
    ". . exFoot exFoot";
  place-items: center; /* without this, background does not fill entire area */
}
.exHead {
  text-transform: uppercase;
  grid-area: exHead;
  font-size: 1.5em;
  color: navy;
}
td:nth-child(1) {
  text-align: left;
}
td:nth-child(2) {
  text-align: right;
}
img:hover {
  transform: scale(1.5);
}
```

## index.html

```html
    <link href="css/main.css" rel="stylesheet" />
    <script>
      function gpaCalc() {
        let cGPA = parseFloat(document.getElementById("cumulative").value);
        document.getElementById("new").innerHTML = `${calcGrade.toFixed(1)}`;
        document.getElementById("new").style.weight = "bold";
      }
    </script>
    <section class="exGrid">
      <header class="exHead"><h1>Sheridan College</h1></header>
      <section class="exGPA boxAll">
        <div class="boxHead">GPA Calculation Data</div>
        <div class="boxBody">
          <fieldset>
            <button onclick="gpaCalc()">Click to see NEW cumulative GPA</button>
          </fieldset>
        </div>
      </section>
      <footer class="exFoot">
        <p>All images &copy;Sheridan College</p>
      </footer>
    </section>
  </body>
</html>
```
