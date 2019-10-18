## Topic: Mobile Ecosystem / See Mobile Ecosystem presentation in Module 01

1. Definitions
    - Page Weight: The sum of bytes for a specific HTML page PLUS the byte count of EVERY resource the page uses
    - smart client: client can maintain their functionality even when disconnected
    - bandwidth: the rate of data transfer, bit rate, or throughput measured in bits per second(bps)
    - latency: network latency is measured either one-way(the time from the source sending a packet to the destination receiving it) or round-trip latency which is most often quoted because is it measured from a single point.
2. Best practices
   - Keep It Simple(but not too simple or ugly!)
   - Most frequent should be displayed first(such as a banking app)
   - No more than 3 levels of navigation
   - Reduce user input when possible(ex. using defaults when possible or option buttons)
   - avoid horizontal scrolling
   - provide adequate navigation
   - maintain consistency across pages...fonts, colours, etc.
   - use responsive design for orientation changes
   - provide visual separation of sections using colours, for example, instead of whitespace
   - change colours based on light conditions such as sun, shade, indoor, low lighting so easy to read
   - always include accessibility support
3. Mobile applications versus Desktop applications
   - higher latency(slower)
   - screen size is smaller
   - shorter battery life
   - testing and debugging is a challenge
   - browsers can behave differently
   - mobile users are in a distracted environment and usually have immediate needs

## Topic: ECMA / ES6 / See ECMA presentation in Module 02 plus In-class examples, exercises, and assignments

1. Using let and const keywords
   - var: function-scoped variables
   - let: scoped at block{} level 
   - const : scoped at block{} level, cannot be reassigned in the code (array, object changes can be made)
2. Using the for...of loop
   - allows iteration over arrays or strings (any iterable object)
   - does not work with actual objects
    ```js
    let college = "sheridan";
    for(let letter of college){console.log(letter)};
    ```
3. Creating output using template literals that includes static text and variable data
   - back-tick or grave accent
```js
let cp = 4;
let sa = 2;
let terms = `The cp program ${cp+sa} terms`;
```
4. Using Classes with constructors
   - class are not hoisted
```js
class CircleArea{
    constructor (radius){
        this.radius = radius;
    }
    getArea(){
        return Math.pow(this.radius,2);
    }
}
let circle = new CircleArea(5);
```

## Topic: Local Storage / See Local Storage presentation in Module 02 plus In-class examples, exercises, and assignments

```js
localStorage.setItem(key, value);
localStorage.getItem(key, value);
localStorage.removeItem(key);
localStorage.clear();
```

1. Local storage setup (key/Value pairs)
2. Saving to local storage
3. Retrieving from local storage
4. Updating web page with local storage data / .innerHTML or .value based on whether the output area is an HTML tag or an <input> field
5. Removing one item from local storage

## Topic: jQuery / AJAX / JSON / See jQuery presentations in Module 03 and Module 04 plus In-class examples, exercises, and assignments

1. What is jQuery?
   - javascript library with customized scripts that handle many tasks needed for creating fully interactive web sites
   - lightweight and contains all the common dom, event, and ajax functions.
   - single script file
```js
<head>
    <script src="js/jquery.js"></script>
</head>
```
2. jQuery symbol used to tell site to use the jQuery library
   - $(selector).action();
```js
$("#id").html(""); //innerHTML
$("#id").append("");
$("#id").css("property","value");
```
3. Selecting and updating elements using jQuery
```js
$("#id").action();
$("tag").action();
$(".class").action();
$("img[alt]").html("inclusion of an attribute");
$("img:not([alt])").html("absence of an attribute");
$("p:has(img)").html("contains another specific tag");
$("p:contains('hello')").html("contains specific text");
$("a[href='index.html']").html("match");
$("a[href!='syst2444']").html("no match");
$("a[href^='syst']").html("starts with");
$("a[href$='.jpg']").html("ends with");
$("a[href~='syst']")html("word match");

$(this).hide("slow");
$(this).fadeout(5000);
$(this).show();
$(this).toggle();
$(this).addClass("ex");
$(this).removeClass("ex");
$(this).toggleClass("ex");
$(this).mouseover(function(){});
$(this).mouseout(function(){});
$(this).hover(function(){}, function(){});

$("h1:nth(0)").css("font-size", "1.5em");
$("h1:first").html("title line");
$("h1:last").html("copyright");

```
4. Explain the purpose of the $(document).ready(function() {});
   - used to prevent any jquery code from running before the document is finished loading
5. Coding using jQuery with AJAX to pull data from a JSON file
6. How to traverse to a specific level in a JSON file
7. How to loop through data elements in a JSON file
8. How to retrieve a single data element from a JSON file