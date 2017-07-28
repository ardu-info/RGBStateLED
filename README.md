
# RGBStateLED
Provides an Arduino library for using a RGB led to asynchronously signal program states using predefined or custom blink pattern. 


## Table of Contents

* [RGBStateLED](#rgbstatusled)
* [Table of Contents](#table_of_contents)
* [Summary](#summary)
* [Installation](#installation)
* [Usage](#usage)
* [Methods](#methods)
 * [RGBStateLED(int pinRed, int pinGreen, int pinBlue, LogLevel logLevel = NONE)](#methods)
 * [void begin()](#methods)
 * [void update()](#methods)
 * [void update(unsigned long)](#methods)
 * [void setRGB(int r, int g, int b)](#methods)
 * [void SetSequence(RGBStateLEDEffect* sequence)](#methods)
 * [bool HasSequenece()](#methods)
 * [void DropSequenece()](#methods)
* [Effects](#effects)
 * [SolidLEDEffect(RGBStateLED* parent, int r, int g, int b, int duration, int start = 0, LogLevel logLevel = NONE)](#effects)
 * [RGBParserEffect(RGBStateLED* parent, char* data, int duration = 450, int start = 0, LogLevel logLevel = NONE)](#effects)
 * [FlashEffect(RGBStateLED* parent, int r,int g, int b, int riseTime, int duration, int fallTime, int start = 0, LogLevel logLevel = NONE)](#effects)
 * [WifiStateEffect(RGBStateLED* parent, int start = 0, LogLevel logLevel = NONE)(#effects)
 * [RGBStateLEDEffect(RGBStateLED* parent, unsigned long start = 0, LogLevel logLevel = NONE)](#effects)
* [Custom Effect](#customeffect)
* [Contributing](#contributing)
* [History](#history)
* [Credits](#credits)
* [License](#license)
<snippet>
<content>

## Summary

Provides an Arduino library for using a RGB led to asynchronously signal program states. 
The library provides various blink patterns (called Effects) which can be used with almost no programming efforts.
Custom effects can be created with ease.

Build-in patterns
* SolidLEDEffect - the LED emits light in a user defined color for the specified period of time (or infinit)
* RGBswitcherEffect - simple test effect which switches the led to red, followed by green, followed by blue
* RGBParserEffect - the LED emits light in a user defined color sequence. (e.g. `char* seq = "r r b";` blink red, pause, blink red, pause, blink blue)
* FlashEffect - fades from dark to the specified color and back to dark
* WifiStateEffect - indicates the current Wifi connection state


## Installation

To use this library download the zip file, uncompress it to a folder named RGBStatusLed. Move the folder to {Arduino Path}/libraries.

## Usage

Include the library at the top of your Arduino script. `#include <RGBStatusLed.h>` and add any Effekt definition you need:
* `#include <SolidLEDEffect.h>` 
* `#include <RGBswitcherEffect.h>`
* `#include <RGBParserEffect.h>`  
* `#include <FlashEffect.h>`  
* `#include <WifiStateEffect.h>`  
* or create a custom pattern by deriving  `#include <RGBStateLEDEffect.h>`  

Create a global variable and pass the pin no of the red, green and blue channel: e.g. `RGBStatusLed statusLed(D8, D7, D6);`
Add `stateLED.begin();` to the init section of your code.
Add `stateLED.update();` add the top of the loop method.

By now, you may signal a program state using one of the two options:

* call `stateLED.setRGB(r,g,b);` (0<=r,g,b<=255) and directly set a color. There is no buildin timeout.
* instantiate an effect and assign it to the stateLED. 
  * e.g. make the LED emit purple light for 1500ms 

```C++
// instantiate SolidLedEffekt, r=255,g=0,b=255  duration = 1500ms 
RGBStatusLedEffekt* seq = new SolidLedEffekt(&statusLed, 255, 0, 255,   1500);
// assign Effekt to statusLed
statusLed.SetSequence(seq);
```

* Have a close look at the examples for details on how to use each effect.
  * Example A does not make use of any effect and uses setRGB directly
  * Examples B-F illustrate the use of the build-in effects
  * Example Z-CustomEffect demonstrates how to define a custom effect. The example brings its own copy of the RGBswitcherEffect soley for demonstration purpose.


## Methods

#### RGBStateLED(int pinRed, int pinGreen, int pinBlue, LogLevel logLevel = NONE)

  Constructor used to create the state LED 
  Return: None

    * port connected to red pin of the LED (pinRed), int
      values: hardware dependent

    * port connected to green pin of the LED (pinGreen), int
      values: hardware dependent

    * port connected to blue pin of the LED (pinBlue), int
      values: hardware dependent

    * controls debug logging (logLevel), int
      values: NONE, DEBUG

#### void begin()
  todo 
  Return: None

#### void update()
  todo 
  Return: None

#### void update(unsigned long)
  todo 
  Return: None

#### void setRGB(int r, int g, int b)
  todo 
  Return: None

#### void SetSequence(RGBStateLEDEffect* sequence)
  todo 
  Return: None

#### bool HasSequenece()
  todo 
  Return: true/false

#### void DropSequenece()
  todo 
  Return: None


## Effects

#### SolidLEDEffect(RGBStateLED* parent, int r, int g, int b, int duration, int start = 0, LogLevel logLevel = NONE)

  Constructor used to create a SolidLEEffect class instance. 
  Return: None

    * brightness red (r), int
      values: 0 = dark, ... 255 = bright red

    * brightness green (g), int
      values: 0 = dark, ... 255 = bright green

    * brightness blue (b), int
      values: 0 = dark, ... 255 = bright blue

    * duration of effect (duration), int
      values: 0 = infinite, >0 value in ms 

    * start time of effect = current time (start), int, default = 0 
      values: 0 = automatic, current time in ms, value of millis()

    * controls debug logging (logLevel), int
      values: NONE, DEBUG


#### RGBParserEffect(RGBStateLED* parent, char* data, int duration = 450, int start = 0, LogLevel logLevel = NONE)

  Constructor used to create a RGBParserEffect class instance.
  Return: None

    * data string, \0 terminated (data), char*
      e.g. char* data = "r g  bb wrgb";
      values: r(ed), g(reen), b(lue), " " no color, w(hite)

    * duration of effect (duration), int
      values: 0 = infinite, >0 value in ms

    * start time of effect = current time (start), int, default = 0
      values: 0 = automatic, current time in ms, value of millis()

    * controls debug logging (logLevel), int
      values: NONE, DEBUG


#### FlashEffect(RGBStateLED* parent, int r,int g, int b, int riseTime, int duration, int fallTime,  int start = 0, LogLevel logLevel = NONE) 

  Constructor used to create a FlashEffect class instance.
  Return: None

    * brightness red (r), int
      values: 0 = dark, ... 255 = bright red

    * brightness green (g), int
      values: 0 = dark, ... 255 = bright green

    * brightness blue (b), int
      values: 0 = dark, ... 255 = bright blue

    * rise time of effect (riseTime), int
      values: >0 value in ms

    * duration of effect (duration), int
      values: >0 value in ms

    * fall time of effect (fallTime), int
      values: >0 value in ms

    * start time of effect = current time (start), int, default = 0
      values: 0 = automatic, current time in ms, value of millis()

    * controls debug logging (logLevel), int
      values: NONE, DEBUG


#### WifiStateEffect(RGBStateLED* parent, int start = 0, LogLevel logLevel = NONE) : RGBStateLEDEffect(parent, start, logLevel)

  Constructor used to create a WifiStateEffect class instance.
  Return: None

    * start time of effect = current time (start), int, default = 0
      values: 0 = automatic, current time in ms, value of millis()

    * controls debug logging (logLevel), int
      values: NONE, DEBUG

#### RGBStateLEDEffect(RGBStateLED* parent, unsigned long start = 0, LogLevel logLevel = NONE);

  Constructor used to create a RGBStateLEDEffect class instance.
  Return: None

    * start time of effect = current time (start), int, default = 0
      values: 0 = automatic, current time in ms, value of millis()

    * controls debug logging (logLevel), int
      values: NONE, DEBUG


## Custom Effect




```C++
class RGBStateLEDEffect {
  public:
    RGBStateLEDEffect(RGBStateLED* parent, unsigned long start = 0, LogLevel logLevel = NONE);
    void update(unsigned long curUpdate);
    bool isFinished();
    void setParentRGB(int r, int g, int b);
    virtual void updateLED() = 0;

  protected:
    RGBStateLED* parent;
    bool active;
    unsigned long start;
    unsigned long lastUpdate;
    unsigned long curUpdate;
    LogLevel logLevel;

    void StopSequence();
};
```


## Contributing

1. Fork the project.
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Added cool new feature xy'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request.

## History

- Jul 27, 2017 - Version 1.0.0 released.

## Credits

Written by Björn Mönikes, 2017.


## License

GNU GPL, see License.txt
</content>
</snippet>



