## myscript.js

```js
$(document).ready(function() {
  $("h2:first").html("Selectors and ");
  $("h2:first").append("Actions and DOM");
  $("h2:nth(0)").css("font-style", "italic");
  $("h2:nth(0)").addClass("h2Style");

  $("#gifImages").click(function() {
    $("#s1 img[src $='.gif']").addClass("gifBorder");
    $("#s1 img[src $='.gif']").removeClass("gifBorder");
    $("#s1 img[src $='.png']").toggle();
    $("section[title ^= 'Text']").css("color", "red");
    $("section:contains('color')").css("font-style", "italic");
    $("section:has(p:contains('para3'))").css("text-decoration", "underline");
    // $("section:has(p):contains('para3"))
  });

  $("#hoverClick").mouseover(function() {});
  $("#hoverClick").mouseout(function() {});
  $("#slide").click(function() {
    $(this).slideToggle("slow");
  });

  $("#fade").click(function() {
    $(this).fadeOut(3000, function() {
      $("#callBack").html("<img src='images/back.gif'>");
    });
  });

  $("#callBack").click(function() {
    $("#fade").fadeIn(3000, function() {
      $("#callBack").html("");
    });
  });

  $("#d2button").hide();
  $("#rbutton").click(function() {
    $("img#pear").remove();
    $(this).remove();
  });

  var a;
  $("#dbutton").click(function() {
    a = $("img#strawberry").detach(); // 딸기 이미지 갖고와서 a에 넣음 (remove and keep data)
    $("#abutton").show();
  });

  $("#d2button").click(function() {
    $("img#apple").after(a);
  });

  $("#abutton").click(function() {
    $(".pieApple").replaceWith(a);
  });
});
```
