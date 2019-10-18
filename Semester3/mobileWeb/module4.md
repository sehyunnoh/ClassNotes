## jsonp

- only perform get requests
- server must explicitly support it

```js
$.ajax({
    url:http://run,
    dataType: "jsonp",
    success: jsonCallback
});

function jsonCallback(data){console.log(data)};

$.getJSON(
    "http://api.github.com/users/jeresig?callback?",
    function(data){console.log(data)}
);
```

```js
var sArray = new Array();
var newRec;

class Student {
  constructor(name, number, program, coop, list) {
    this.name = name;
    this.number = number;
    this.program = program;
    this.coop = coop;
    this.list = list;
  }

  outputCoop(coop) {
    let out;
    if (coop) {
      out = "YES";
    } else {
      out = "NO";
    }
    return out;
  }
}

$(document).ready(function() {
  $.getJSON("dataFiles/schoolData.json", function(data) {
    start = data.students.studentRec;
    for (let x = 0; x < start.length; x++) {
      newRec = new Student(
        start[x].name,
        start[x]["student-number"],
        start[x].program,
        start[x].coop,
        start[x].email
      );
      sArray.push(newRec);
    }
    loadStudentData();
  });
});

function loadStudentData() {
  $("h4").html("Student Data");
  $(".labels").html(
    "<th>NAME</th><th>ID</th><th>PROGRAM</th><th>COOP?</th><th>EMAIL</th>"
  );
  $("#sdata").html("");

  for (let x of sArray) {
    $("#sdata").append(
      `	<tr>
            <td>${x.name}</td>
            <td>${x.number}</td>
            <td>${x.program}</td>
            <td>${x.outputCoop(x.coop)}</td>
            <td>${x.list}</td>
        </tr>
       `
    );
  }
}

/* AJAX call that can be used instead of .getJSON()
    $.ajax({
        type: "POST",
        url: "ex02-JSON.json",
        dataType: "json",
        success: loadJSON,
				error: function (request,error) {
            alert('Network error has occurred: ' + error);}
    });

*/
```

## myscript.js

```js
var cityArray = new Array();
var latArray = new Array();
var lngArray = new Array();
var rowID;

$(document).ready(function() {
  $.getJSON("dataFiles/cities.json", function(data) {
    $("#cityList").html("");
    for (let x = 0; x < data.cities.length; x++) {
      cityArray[x] = data.cities[x].cityName;
      latArray[x] = data.cities[x].cityLat;
      lngArray[x] = data.cities[x].cityLng;

      $("#cityList").append(
        `
          <li li-id='${x}'>
            <a href="weather.html">${data.cities[x].cityName}</a>
          </li>
          `
      );
    }

    localStorage.setItem("cityArray", JSON.stringify(cityArray));
    localStorage.setItem("latArray", JSON.stringify(latArray));
    localStorage.setItem("lngArray", JSON.stringify(lngArray));
  });
});

$(document).on("click", "#cityList > li", function() {
  localStorage.setItem("rowID",$(this).closest("li").attr("li-id"));
});
```

## myscript 2

```js
$(document).ready(function() {
  var d = new Date();
  $("#cdate").html(d);
  latArray = JSON.parse(localStorage.getItem("latArray"));
  lngArray = JSON.parse(localStorage.getItem("lngArray"));
  rowID = localStorage.getItem("rowID");

  var lat = latArray[rowID];
  var lon = lngArray[rowID];
  var apiURI = `http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=484e47e5a69dfcd6d1d089e84051d0d5`;

  $.ajax({
    type: "GET",
    url: apiURI,
    dataType: "jsonp",
    success: function(response) {
      console.log(response);
      $(".dataCity").html(response.name);
      $(".dataTemp").html((response.main.temp - 273.15).toFixed(0) + " C");
      $(".dataWind").html(response.wind.speed + " knots");
      $(".dataHum").html(response.main.humidity + " %");
      $(".dataPress").html(response.main.pressure + " mbars");
    }
  });
});
```

## myscript.js

```js
var countryName;
var background;
var pList = new Array();
var rowID;

class Prov {
  constructor(name, type, capital, flag, ...cities) {
    this.name = name;
    this.type = type;
    this.capital = capital;
    this.flag = flag;
    this.cities = cities;
  }
}

$(document).ready(function() {
  $.ajax({
    type: "GET",
    url: "dataFiles/canada.json",
    dataType: "json",
    success: loadJSON,
    error: function(e) {
      alert(`${e.status} - ${e.statusText}`);
    }
  });
});

function loadJSON(data) {
  countryName = data.country.name;
  background = data.country.background;

  for (let prov of data.country.division) {
    if (prov.type == "province") {
      var cities = new Array();

      for (let city of prov.city) {
        cities.push(city);
      }

      pList.push(
        new Prov(prov.name, prov.type, prov.capital, prov.pic, cities)
      );
    }
  }
  mainScreen(data);
}

function mainScreen() {
  $("#country").html(countryName);
  $("#background").html(background);
  $("#background").hide();
  $("#provList").html("");
  for (let x = 0; x < pList.length; x++) {
    $("#provList").append(
      `
			<li li-id='${x}'>
				<a href="otherPages/provPage.html">${pList[x].name}</a>
			</li>
			`
    );
  }
}

$(document).on("click", "#provList >li", function() {
  localStorage.setItem("cname", countryName);
  localStorage.setItem("rowID", $(this).closest("li").attr("li-id"));
  localStorage.setItem("pList", JSON.stringify(pList));
});
```

## myscriptProv.js

```js
var pList = new Array();
var rowID;
var cList = new Array();

$(document).ready(function() {
  cname = localStorage.getItem("cname");
  rowID = localStorage.getItem("rowID");
  pList = JSON.parse(localStorage.getItem("pList"));

  $("#country").html(cname);
  $("#pname").html(pList[rowID].name);
  $("#capital").html(pList[rowID].capital);
  $("#flag").html(`<img src='../images/${pList[rowID].flag}'>`);

  for (x = 0; x < pList[rowID].cities[0].length; x++) {
    $("#cities").append(`${pList[rowID].cities[0][x]}<br>`);
  }
});
```
