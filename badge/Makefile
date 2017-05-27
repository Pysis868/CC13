# Arduino Make file.
# It is not necessary, but you may refer to `https://github.com/sudar/Arduino-Makefile`.

# All variables are customizable from the environment, and defaults will be used if absent.
# Source: https://stackoverflow.com/questions/448910/makefile-variable-assignment#

# Source: https://stackoverflow.com/a/8080530
SELF_DIR ?= $(dir $(lastword $(MAKEFILE_LIST)))

### PROJECT_DIR
### This is the path to where you have created/cloned your project
PROJECT_DIR ?= $(SELF_DIR)/..

### AVR_GCC_VERSION
### Check if the version is equal or higher than 4.9
AVR_GCC_VERSION ?= $(shell expr `avr-gcc -dumpversion | cut -f1` \>= 4.9)

### ARDMK_DIR
### Path to the Arduino-Makefile directory.
ARDMK_DIR ?= $(PROJECT_DIR)/Arduino-Makefile

### ARDUINO_DIR
### Path to the Arduino application and resources directory.
ARDUINO_DIR ?= /usr/local/arduino

# Mac users may want to use this one instead.
#ARDUINO_DIR = /Applications/Arduino.app/Contents/Java

### USER_LIB_PATH
### Path to where the project's libraries are stored.
USER_LIB_PATH ?= $(realpath $(PROJECT_DIR)/libraries)

### BOARD_TAG & BOARD_SUB
### For Arduino IDE 1.0.x
### Only BOARD_TAG is needed. It must be set to the board you are currently using. (i.e uno, mega2560, etc.)
# BOARD_TAG         = mega2560
### For Arduino IDE 1.6.x
### Both BOARD_TAG and BOARD_SUB are needed. They must be set to the board you are currently using. (i.e BOARD_TAG = uno, mega, etc. & BOARD_SUB = atmega2560, etc.)
### Note: for the Arduino Uno, only BOARD_TAG is mandatory and BOARD_SUB can be equal to anything
### Tested with 1.8.2 on Linux and Mac successfully.
#BOARD_TAG    = atmega328
BOARD_TAG    ?= diecimila
BOARD_SUB    ?= atmega328

### If avr-gcc -v is higher than 4.9, activate coloring of the output
ifeq "$(AVR_GCC_VERSION)" "1"
    CXXFLAGS     += -fdiagnostics-color
endif

### MONITOR_BAUDRATE
### It must be set to Serial baudrate value you are using.
MONITOR_BAUDRATE ?= 115200

### MONITOR_PORT
### The port your board is connected to. Using an '*' tries all the ports and finds the right one.
MONITOR_PORT ?= /dev/ttyUSB0

# Mac users may want to use this one or one like it instead.
#MONITOR_PORT = /dev/tty.usbserial-12345678




# The main Arduino include.
include $(ARDMK_DIR)/Arduino.mk
