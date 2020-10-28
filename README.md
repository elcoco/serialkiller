## Serial Killer

A less annoying serial terminal written in Python3

### Features
- send and receive data over serial port or serial over TCP
- read data from pipe and send over serial, wait for confirmation string
- **temporary free up port** to upload code by using an external command
- **log data** to file
- **autodetect** serial port
- readline **history** with ↑↓

### Introduction
Nobody likes to use the arduino IDE, but it functions well for uploading code to your MCU.  
One problem I experienced while using my favorite editor, was that you have to exit the serial  
monitor to free the serial port so code can be uploaded.
SerialKiller is a serial monitor that can be externally signaled to free up the serial port.
```
# This example will free up serial, upload code and connect to serial again.
$ sk -l && arduino --upload my_super_awesome_project.ino && sk -u
```

### Examples
```
# Try to guess serial port, using default baudrate, 115200
$ sk

# Specify port and baudrate
$ sk -p /dev/ttyUSB0 -b 9600

# Specify url to connect over eg telnet
$ sk -U socket://localhost:23

# Read from STDIN line by line and send over serial.
# Wait for string 'ok' before sending next line.
# This is handy for when you want to send gcode to GRBL CNC firmware.
$ cat test.gcode | sk -c ok -T 5

# Read from STDIN line by line and send over serial.
# wait n seconds before sending next line
$ cat test.gcode | sk -c ok -w 5

# Free up (lock) serial port of running sk instance
$ sk -l

# Reconnect (unlock) serial port of running sk instance
$ sk -u

# Log to file, file will be created inside dir ~
$ sk -L -P ~
```

### Vim keybinding
```
# Add this line to your .vimrc file to compile and upload current file using arduino IDE
nnoremap <C-a> :w<CR>:!sk -l ; arduino --upload % ; sk -u<CR>
```

### Help
```
laptop ~/dev/serialkiller master > sk --help
usage: sk [-h] [-p PORT] [-b RATE] [-t TIMEOUT] [-L] [-P LOG_DIR] [-l] [-u] [-d]

SerialKiller does serial things.

optional arguments:
  -h, --help            show this help message and exit
  -p PORT, --port PORT  default: /dev/ttyUSB0
  -b RATE, --baudrate RATE
                        default: 115200
  -t TIMEOUT, --timeout TIMEOUT
                        default: 0
  -L, --log             log data to file
  -P LOG_DIR, --log_dir LOG_DIR
                        specify log dir
  -l, --lock            free serial port
  -u, --unlock          reconnect to serial
  -d, --debug           enable debugging
```
