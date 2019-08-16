```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>DOM Basics - Document Object Model</title>

    <script>
      // alert("help");
      console.log("ya!");

      // dom 불러 온다음에 작동 (이렇게 안하면 null)
      window.addEventListener("DOMContentLoaded", function() {
        var fastcars = document.getElementById("fastcars");
        var fastcars2 = document.querySelector("#fastcars2");
        var fastcars3 = document.querySelector("#fastcars3");
        var fastcars4 = document.querySelector("#fastcars4");

        var carSpeed = [0, 0, 0, 0];
        var speed = 1;

        setTimeout(function() {
          fastcars.innerHTML = "<strong>Tesla</strong>";
          fastcars.style.background = "orange";
          speed = 10;

          setInterval(function() {
            carSpeed[3] += 6;
            fastcars4.style.left = carSpeed[3] + "px";
          }, 50);
        }, 3000);

        // fastcars.style.fontWeight = "bold";

        setInterval(function() {
          carSpeed[0] += speed;
          fastcars.style.left = carSpeed[0] + "px";
          if (carSpeed[0] > 1200) {
            speed *= -1;
          }

          carSpeed[1] += 5;
          fastcars2.style.left = carSpeed[1] + "px";
          carSpeed[2] += 2;
          fastcars3.style.left = carSpeed[2] + "px";
        }, 50);

        fastcars.addEventListener("mousedown", function(e) {
          // speed = 0;
          e.target.style.display = "none";
          // fastcars.style.display = "none";
        });

        var stopsign = document.createElement("div");
        stopsign.setAttribute("width", 100);
        stopsign.setAttribute("id", stopsign);
        stopsign.innerHTML = "STOP";
        stopsign.style.background = "red";
        stopsign.style.color = "white";
        // stopsign.style.width = "300px";
        // stopsign.style.display = "inline-block";

        document.body.appendChild(stopsign);
      });
    </script>

    <style>
      .cars {
        padding: 20px;
        margin: 30px;
        display: inline-block;
        font-family: verdana;
        position: relative;
        font-weight: bold;
        cursor: pointer;
      }
      #fastcars {
        background: yellow;
      }
      #fastcars2 {
        background: red;
      }
      #fastcars3 {
        background: blue;
      }
      #fastcars4 {
        background: gray;
      }
    </style>
  </head>
  <body>
    <div id="fastcars" class="cars">
      Lada
    </div>
    <br />
    <div id="fastcars2" class="cars">
      SuperCar
    </div>
    <br />
    <div id="fastcars3" class="cars">
      Ironman
    </div>
    <br />
    <div id="fastcars4" class="cars">
      Porche
    </div>
  </body>
</html>
```