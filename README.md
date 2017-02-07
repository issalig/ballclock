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

Plan generator
https://jsfiddle.net/issalig/w3oorhne/
http://codepen.io/issalig/pen/wgxGaw

MISC CODE FOR HSV

local NUM_LEDS = 5;
local i = 1;
local d = 1;
local hue = 0;

local function hueToRgb(hue)
    if hue >=0 and hue < 60  then return 255, hue * 255 / 60, 0 end;
    if hue >=60 and hue < 120  then return (120-hue) * 255 / 60, 255, 0 end;
    if hue >=120 and hue < 180  then return 0, 255, (hue-120) * 255 / 60 end;
    if hue >=180 and hue < 240  then return 0, (240-hue) * 255 / 60, 255 end;
    if hue >=240 and hue < 300  then return (hue-240) * 255 / 60, 0, 255 end;
    if hue >=300 and hue < 360  then return 255,0,(360-hue) * 255 / 60 end;
end

ws2812.init()
local buffer = ws2812.newBuffer(NUM_LEDS,3);
buffer:fill(0,0,0);

tmr.alarm(0, 50, 1, function()
    hue = (hue + 1) % 360;
    local r,g,b = hueToRgb(hue);

    i = i + d;
    if( i == NUM_LEDS ) then d = -1 end
    if( i == 1 ) then d = 1 end
    buffer:fade(3);
    buffer:set(i, r,g,b);
    buffer:write();
end)

