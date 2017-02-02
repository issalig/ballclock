# ballclock
An hexagonal ball clock with RGB leds.
Inspired by a ping pong led ball clock (http://hackedgadgets.com/2011/02/02/ping-pong-led-clock/ https://github.com/szczys/Ping-Pong-Clock/blob/master/ping-pong-clock.c), this build makes use of ws2812b RGB leds and distrute them in an hexagonal grid.

The chosen layout is an hexagon of 3-ball radius that make a total of 19 balls. Hours are in the outer hexagon, minutes (5, 15 .. 55) in the central hexagon and the central led is reserved for seconds. For multiples of 10, the closest 5 multiples will be lit.
```
  2:35
   o o o   
  o o o *  
 o o o o o 
  o * o o  
   o o o
```

```
  6:00
   o o o   
  o * * o
 o o o o o 
  o o o o  
   o * o
```

Also, some information int the shape of numbers is expected.

```

   o o *   
  o * * *
 o o o * o
  o o * o  
   * * *
```

ws2821b are 5V powered and consume around 60mA when in full brightness (white). Thus, having a total of 19 leds will get a maximum of 1.14A that should be enough for a 5v, 1A USB charger.

