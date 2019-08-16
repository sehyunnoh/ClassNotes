# final exam review
```js
var x;
x = 10;
var y = 5;
if (x > y) {
//   console.log("yay");
}
// console.log(x > y);
function trip(destination) {
//   console.log(destination);
}

// hoisting ( declare scope )
trip("Hawaii!");

var myths = ["Dracula", "SpongeBob", "Unicorn"];

for (var i = 0; i < myths.length; i++) {
//   console.log(myths[i]);
}

// myths.map(m => console.log(m));

// splice, slice, split, reverse, push, pop, shift, unshift, sort, indexOf -> 값 없으면 return -1
// push(?) + end
// pop - end
// shift - start
// unshift(?) + start

var transport = {
  type: "bus",
  cost: 20
};

transport.color="red";
transport['color']="blue";

// console.log(transport);

// combination question

// make object literal called players loop through myths and add a rendom score out of 10 to each myth inside players

var players={};

for(var i=0; i < myths.length; i++){
    players[myths[i]] = Math.floor(Math.random()*10)+1;
}

console.log(players);
```

# added
```js
Window.addEventListenr("DOMContentLoaded", function(){*});

Window -> object
addeventLIstener -> Method
"DOMContentLoaded" -> Argument 
; => termination

	- make object literal called players loop through myths and add a rendom score out of 10 to each myth inside players

	- Write the code to make tech tag disappear when clicked on.
      . display:none;
	- Log to the console the value of vr tag when we submit the form prevent the default action as well.
    document.getElementById("myAnchor").addEventListener("click", function(event){
  event.preventDefault()
});
	- Test if vr matches a number
	- Use localStorage to set a score to remembered score or to zero
	- What is json stand for Javascript object notation
	. JSON.stringify()
	. JSON.parse()
	 -> json에 저장되는 형태
		String
		Number
		Array
		Object List 

Function literal, anonymous function 

createElement

setInterval
setTimeout

Cookie  -> session storage (do not ask how to use cookie )
localStorage -> session storage
```