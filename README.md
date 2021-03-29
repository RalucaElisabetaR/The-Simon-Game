# [The-Simon-Game using jQuery](https://ralucaelisabetar.github.io/The-Simon-Game/)

```javascript
let buttonColours = ['red', 'blue', 'green', 'yellow']

let gamePattern = []
let userClickedPattern = []

let started = false
let level = 0

$(document).keypress(function () {
    if (!started) {
        $('#level-title').text('Level ' + level)
        nextSequence()
        started = true
    }
})
```

## Using jQuery to detect when any of the buttons are clicked and trigger a handler function.

```javascript
$(".btn").click(function () {
```

## Storing the id of the button that got clicked in the userChosenColour variable:

```javascript

  let userChosenColour = $(this).attr("id");
  userClickedPattern.push(userChosenColour);

  playSound(userChosenColour);
  animatePress(userChosenColour);

  checkAnswer(userClickedPattern.length - 1);
});

function checkAnswer(currentLevel) {

  if (gamePattern[currentLevel] === userClickedPattern[currentLevel])
  {
    if (userClickedPattern.length === gamePattern.length)
    {
      setTimeout(function () {
        nextSequence();
      }, 1000);
    }
  } else
  {
    playSound("wrong");
    $("body").addClass("game-over");
    $("#level-title").text("Game Over, Press Any Key to Restart");

    setTimeout(function () {
      $("body").removeClass("game-over");
    }, 200);

    startOver();
  }
}


function nextSequence() {
```

## Reset the userClickedPattern to an empty array ready for the next level once nextSequence() is triggered:

```javascript
userClickedPattern = []
```

## Increasing the level by 1 every time nextSequence() is called:

```javascript
level++
```

## Update the h1 with the value of the level.

```javascript
$("#level-title").text("Level " + level);
let randomNumber = Math.floor(Math.random() * 4);
let randomChosenColour = buttonColours[randomNumber];
gamePattern.push(randomChosenColour);

$("#" + randomChosenColour).fadeIn(100).fadeOut(100).fadeIn(100);
playSound(randomChosenColour);
}

function animatePress(currentColor) {
```

## Adding the 'pressed' class to the button that gets clicked ->> using jQuery:

```javascript
$("#" + currentColor).addClass("pressed");
setTimeout(function () {
```

## Removing the 'pressed' class after a 100 milliseconds:

```javascript
  $("#" + currentColor).removeClass("pressed");
}, 100);
}

function playSound(name) {
let audio = new Audio("sounds/" + name + ".mp3");
audio.play();
}

function startOver() {
level = 0;
gamePattern = [];
started = false;
}
```
