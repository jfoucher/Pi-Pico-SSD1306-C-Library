# Pi Pico SSD1306 C++ Library
## 1. Description
This is a C++ library for raspberry pi pico.

It's based on offical pi pico examples. If you are intersted in it, you can find it here [Pico Examples OLED I2C](https://github.com/raspberrypi/pico-examples/tree/master/i2c/oled_i2c).
![Pi Pico and OLED](images/Pi%20Pico%20and%20OLED.jpg)

## 2.Function Lists
|           Function           |          Introduction           |
| :--------------------------: | :-----------------------------: |
|         void show()          |  Send all data buffer to oled   |
|         void clear()         |    Make all data buffer to 0    |
| void isDisplay(bool inverse) |  1 display on , 0 display off   |
| void isInverse(bool inverse) |     1 inverse, 0 no inverse     |
|       void drawLine()        |  Draw any angle line you want   |
|    void drawRectangle(）     |        Draw a rectangle         |
|  void drawFilledRectanle()   |     Draw a filled rectangle     |
|      void drawCircle()       |          Draw a cicrle          |
|   void drawFilledCircle()    |      Draw a filled circle       |
|       void isScroll()        |       Turn on/off scroll        |
|     void setScrollDir()      |  1 scroll right,0 scroll left   |
|        void setFont()        | Set font, adafruit font support |
|       void printChar()       |        print a character        |
|         void print()         |         print a string          |
|      void drawBitmap()       |          draw an image          |

## 3.Usage
### 3.1 Declear a oled object

```cpp
#include "OLED.h"

int main(){
    OLED oled;
    return 0;
}
```

Note that, in this library I use default I2C0 and default I2C pins which is `GPIO4-SDA` and `GPIO5-SCL`, you can edit in source file or connect oled use default pins.

### 3.2 Draw some shapes

```cpp
#include "OLED.h"

int main(){
    OLED oled;
    // Rectangle
    oled.drawRectangle(0, 0, 50, 30);
    oled.drawFilledRectangle(5, 5, 40, 20);
    // Circle
    oled.drawCircle(100, 16, 14);
    oled.drawFilledCircle(100, 16, 10);
    // Send data buffer to oled
    oled.show();
    return 0;
}
```

Note that you must call `show()` function after you finish draw shapes.

So as print text or draw image, you need call `show` function too.

### 3.3 Print text

```cpp
#include "OLED.h"
#include "Cherry_Cream_Soda_Regular_16.h"

int main(){
    OLED oled;
    //String 1 "Hello", use defaule font
    uint8_t string1[] = "Hello";
    oled.print(0, 38, string1);
    // String 2 "world!", use custom font
    oled.setFont(&Cherry_Cream_Soda_Regular_16);
    uint8_t string2[] = "world!";
    oled.print(60, 32, string2);
    // Draw a text baseline and send data buffer
    oled.drawLine(0, 60, 128, 60);
    oled.show();
    return 0;
}
```

This library is adafruit font supported, because it's really popular among makers.

You can custom your own font through this website [SSD1306 Tools](http://oleddisplay.squix.ch/#/home) and modify some characters using this website [Adafruit GFX Font Customiser](https://tchapi.github.io/Adafruit-GFX-Font-Customiser/).

### 3.4 Draw some images

```cpp
#include "OLED.h"
#include "bitmap.h"

int main(){
    OLED oled;
    // Draw two images
    oled.drawBitmap(0, 0, 40, 32, pressure_40x32);
    oled.drawBitmap(45, 3, 32, 32, temperature_32x32);
    // Send data buffer to oled
    oled.show();
    return 0;
}
```

You should know that both font and image, the origin point is set at top left.

That's all. Happy hacking.