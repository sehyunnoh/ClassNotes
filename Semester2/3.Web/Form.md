```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Forms and Data</title>
    <style>
      #message {
        padding: 20px;
        background-color: yellow;
        font-family: Verdana;
        font-size: 30px;
        display: none;
        margin-top: 20px;
      }
    </style>
    <script>
      window.addEventListener("DOMContentLoaded", function() {
        var food = document.getElementById("food");
        // food.value = "type food";
        // setTimeout(function(){
        //     console.log(food.value);
        // },2000);

        // var myData = [10, 30, { biggest: 300, smallest: 100 }];
        // localStorage.myData = JSON.stringify(myData);

        var submit = document.getElementById("submit");
        var message = document.getElementById("message");
        var list = document.getElementById("list");

        // if (localStorage) {
        //   // localStorage.clear();
        //   if (localStorage && localStorage.foods) {
        //     // console.log(localStorage.foods);
        //     list.innerHTML = localStorage.foods;
        //   } else {
        //     localStorage.foods = "";
        //   }
        // }

        var foods = [];
        if(localStorage){
          if(localStorage.foods){
            foods = JSON.parse(localStorage.foods);
            console.log(foods);
            list.innerHTML = foods.join("<br>");
          }
        }


        submit.addEventListener("click", function(e) {
          // if( food.value == "" ){
          //     e.preventDefault();
          //     alert("enter food to mouth");
          // }

          // /regular expression/ pattern matching
          // if (!food.value.match(/^melon$/i)) {
          //   message.innerHTML = "enter correct food";
          //   message.style.display = "inline-block";
          //   e.preventDefault();
          // }

          // if (localStorage) {
          //   localStorage.foods += food.value + "<br>";
          // }

            foods.push(food.value);
            if(localStorage) localStorage.foods = JSON.stringify(foods);

        });
        // end of sumit
      });
    </script>
  </head>
  <body>
    <form action="./result.html" method="POST">
      <input type="text" id="food" name="food" value="" />
      <input type="submit" id="submit" value="SUBMIT" />
    </form>

    <div id="message"></div>
    <div id="list"></div>
  </body>
</html>
```