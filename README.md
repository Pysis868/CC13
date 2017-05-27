# Overview
CarolinaCon13 (CC13) Badge Jank

## Project Files
- `CC13 Badge.pdf` - Detailed badge assembly guide (soldering required).
- `libraries/` - TODO: PC Badge setup program dependencies for applying programming to the integrated chip.
- `badge/` - Actual code files for setting up and running on the badge device.
  - `Badge.ino` - This project's Arduino Sketch File and main device code.
  - `README.md` - PC Badge Setup program command help list.
  - `*.h`/`*.cpp` - PC Badge Setup program source files.
  - `Makefile` - C-style project build automation definition file.

## Arduino Build Environment Set-up

### General Linux setup

Download the latest Arduino archive from `https://www.arduino.cc/en/Main/Software`.

    xz --decompress arduino-1.8.2-linux64.tar.xz
    sudo su -;
    cd /usr/local;
    tar xvf ~/Downloads/arduino-1.8.2-linux64.tar;
    ln -s arduino-1.8.2/ arduino;
    git clone --recursive 'https://github.com/lockfale/CC13.git';

### Mac Install

    brew cask install arduino

Add this to your `PATH` environment variable: `"/Applications/Arduino.app/Contents/Java/hardware/tools/avr/bin/"`

    python -m pip install pyserial

Source: [reddit - r/python - When I "import serial" I get the error message:"no module named serial"](https://www.reddit.com/r/Python/comments/3hhe8a/when_i_import_serial_i_get_the_error_messageno/)

Put these lines in your profile script:

    ARDUINO_DIR="/Applications/Arduino.app/Contents/Java"
    MONITOR_PORT="/dev/tty.usbserial-12345678"

## Use

Be sure the jumper is on the center and other pin towards the dot on the FTDI chip!

Command to build PC Setup badge program:

    make

Command to upload code to badge:

    make upload

Command to connect serial port (requires screen):

    make monitor

Keystrokes to disconnect from the serial port in screen session: `^-a k Y`

## Development

### Adding LED Patterns

To add an LED pattern:
1. In `badge/led.h`:
    1. Add a function for it at the bottom.
1. In `badge/setup.cpp`:
    1. Add a submenu command for it.
1. In `badge/led.cpp`:
    1. Add a `const byte` array to with its own name and each sequential animation state of your desired LED pattern in binary format matching the number of LEDs in each entry.
    2. Add a time interval element to the `patternTimes` array.
    3. Add a pattern iteration count element to the `patternLengths` array.
    4. Edit the `changePattern` function:
        1. Increment the integer for the first `tmpPattern` check.
        2. Add a branch to `memcpy_P` the new pattern function.
    5. Add a function for it at the bottom.
