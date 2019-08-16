```js
// 1
var damLa = 3;
var orgStick = 5;
var deMellon = 2;
var uniTick = 7;
var coCamel = 3;

// 2
var values = "I have " + damLa + " damLa and "
           + "I have " + orgStick + " orgStick and "
           + "I have " + deMellon + " deMellon and "
           + "I have " + uniTick + " uniTick and "
           + "I have " + coCamel + " coCamel.";
console.log(values)

// 3
var most = 0;
var mostType = null;

if (most < damLa) {
  most = damLa;
  mostType = "damLa";
}
if (most < orgStick) {
  most = orgStick;
  mostType = "orgStick";
}
if(most < deMellon){
   most = deMellon;
   mostType = "deMellon";
}
if(most < uniTick){
   most = uniTick;
   mostType = "uniTick";
}
if(most < coCamel){
   most = coCamel;
   mostType = "coCamel";
}
console.log(mostType + " " + most);

// 4
var gums = [];
gums.push("damLa", "orgStick", "deMellon", "uniTick", "coCamel");

// 5
var flavours = "My flavours are: ";
for (var i = 0; i < gums.length; i++) {
  flavours += gums[i];
  if (i != gums.length - 1) {
    flavours += ", ";
  }
}
console.log(flavours);

// 6
var lastTaste = gums.pop();
gums.push("rainBow");
gums.unshift(lastTaste);

// 7
function remove(flavour1, flavour2) {
  var array = [flavour1, flavour2];
  var tmp = Math.floor(Math.random() * 2);

  var index = gums.indexOf(array[tmp]);
  if( index != -1) {
      gums.splice(index,1);
  }
}

// 8
var sodaPop = { name: "poPop", cost: 2.5, rating: 1 };
sodaPop.color = "red";
sodaPop["cost"] = 3.5;

// 9
var drinks = [];
drinks.push(sodaPop);
console.log(drinks[0]["cost"]);
```