---
slug: "/johhny-five-repl-esp8266"
title: "Javascript robotics: The Johnny Five REPL"
description: "Lets interact with your Javascript robots"
pubdate: "2020-06-05"
hero: "/images/posts/j5-esp/repl.png"
tags: ["robotics", "javascript", "esp8266"]
layout: "../../layouts/BlogPostLayout.astro"
---

In the [previous article](https://jamesbest.tech/posts/wireless-javascript-robots-johhny-five-esp8266), we discussed how to get up and running with Johnny Five and the ESP8266 micro-controller. If you are not sure how to get set up I recommend you read that article first.

Previously we created a simple script that allowed us to control the onboard LED with our keyboard. This required us to install the `keypress` package and listen in `process.stdin`. This is not a bad approach but there is a better one.

Johnny Five comes packaged with a REPL. A REPL (read-eval-print-loop) is an interactive language shell giving a simple interactive interface to the Johnny Five API. We can control our robots with the REPL but there is some set up first.

## Setting up the REPL

We need to make the REPL aware of our hardware by injecting the `instance` of the hardware into our script. We are using the script from before but with the keyboard code stripped out:

```javascript
const { EtherPortClient } = require("etherport-client")
const { Board, Led, Pin } = require("johnny-five")

const board = new Board({
  port: new EtherPortClient({
    host: "192.168.1.109",
    port: 3030,
  }),
  repl: false,
})

const LED_PIN = 2

board.on("ready", () => {
  console.log("Board ready")
  var led = new Led(LED_PIN)
})
```

Now, let's add the REPL code. Update the board ready callback to look like this:

```javascript
[...]
board.on("ready", function() {
  /*
    Initialize pin 2, which
    controls the built-in LED
  */
  var led = new Led(LED_PIN);

  /*
    Injecting object into the REPL
    allow access while the program
    is running.

    Try these in the REPL:

    led.on();
    led.off();
    led.blink();

  */
  board.repl.inject({
    led: led
  });
});
```

With this simple addition, we now have access to all the functions available on the LED object.

## Limiting access

But what if we don't want to give our users unfettered access? What if we only want to give access to specific functions or write functions that do more than just control the hardware. Maybe we want to add logging or provide more appropriate function names. Well, we can write our own functions that are available in the REPL and inject those instead.

```javascript
[...]
board.on("ready", function() {
  /*
    Initialize pin 2, which
    controls the built-in LED
  */
  var led = new Led(LED_PIN);

  board.repl.inject({
    // Allow limited on/off control access to the
    // Led instance from the REPL.
    on: function() {
      led.on();
    },
    off: function() {
      led.off();
    },
    flash: function () {
      led.blink();
    },

  });
});
```

This script will make `on()`, `off()` and `flash()` functions available in the REPL.

And that is it. A nice, short intro to the Johnny Five REPL. Until you start hooking your scripts up to WebSockets or a REST API, I think this is one of the better ways to control your robots.

# Thanks for reading 🙏

If there is anything I have missed, or if there is a better way to do something then please let me know.

## Check out our software-focused podcast - [Salted Bytes](https://open.spotify.com/show/7IdlgpiDfYcOdCn57mPLvH?si=X1ArfHvqQXSOAfc1h7Y_Eg)
