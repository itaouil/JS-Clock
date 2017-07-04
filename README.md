# **JS-Clock**

This is day 2 of the 30 days of vanillaJS, created by WesBos (wesbos.io).

Today the main task is to interact with a CSS clock and display the correct time on the clock using JavaScript. There are a few stalls we might hit, but I will tackle them in the development section. The final result is the following (clone and run if you want to see the animation):

![alt](https://github.com/itaouil95/JS-Clock/blob/master/clock.png)

**Development**

Right. The key things in this small projects are:

1. Transform hands such that the transformation is at the right of the hand.
2. Offset the hands.
3. Use JavaScript to select the hand and apply a style transformation.

For key number 1, we have to change the origin of where the transform property is going to be applied to:

```CSS3
transform-origin: right;
```

We then offset the hands so that they can start at time 12am/pm:

```CSS3
transform: rotate(90deg);
```

Apply a transition property as well as a cubic-bezier timing function:

```CSS3
transition: all 0.05s;

transition-timing-function: cubic-bezier(0, 2.18, 0.58, 1);
```

Now the fun part, ladies and gentlemen, JavaScript:

```JavaScript
// Select hands (using querySelector)
const hourHand = document.querySelector(".hour-hand");
const minuteHand = document.querySelector(".minute-hand");
const secondHand = document.querySelector(".second-hand");

// Set date function (basically how we apply the time to the hands)
// Set date baby
function setDate() {

  // Get current date
  const now = new Date();

  // Get time instaces
  const hours = now.getHours();
  const minutes = now.getMinutes();
  const seconds = now.getSeconds();

  // Get hands to degree proportion (offset it by 90 deg, given our original transform)
  const hoursDegrees = ((hours * 360) / 12) + 90;
  const minutesDegrees = ((minutes * 360) / 60) + 90;
  const secondsDegrees = ((seconds * 360) / 60) + 90;

  // Apply time to hands
  hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
  minuteHand.style.transform = `rotate(${minutesDegrees}deg)`;
  secondHand.style.transform = `rotate(${secondsDegrees}deg)`;

  // Debugging
  console.log(secondsDegrees);

}

// Run function every second (if eventloop let's you to)
setInterval(setDate, 1000);
```

**N.B:** Check out wesbos.io for more info about the challenge ! Happy coding !
