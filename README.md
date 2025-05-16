## Serial Killer

A less annoying serial terminal written in Python3

### Features
- send and receive data over serial port  
- **temporary free up port** to upload code by using an external command  
- **log data** to file  
- **autodetect** serial port  
- readline **history** with ↑↓  
- can print control characters, very handy for debugging UART messages  

### Introduction
Nobody likes to use the arduino IDE, but it functions well for uploading code to your MCU.  
I noticed, while using my favorite editor instead, that having to exit the serial monitor to free the serial port everytime I want to upload code is super annoying.  
SerialKiller is a serial monitor that can be externally signaled to free up the serial port.  

    # This example will free up serial, upload code and connect to serial again.
    $ sk --lock && arduino --upload my_super_awesome_project.ino && sk --unlock

### Examples

    # Try to guess serial port, using default baudrate, 115200
    $ sk

    # Specify port and baudrate
    $ sk --port /dev/ttyUSB0 -b 9600

    # Free up (lock) serial port of running sk instance
    $ sk --lock

    # Reconnect (unlock) serial port of running sk instance
    $ sk --unlock

    # Log to file, file will be created inside dir ~
    $ sk --log-dir ~

### Vim keybinding

    # Add this line to your .vimrc file to compile and upload current file using arduino IDE
    nnoremap <C-a> :w<CR>:!sk -l ; arduino --upload % ; sk -u<CR>

### Help

    $ sk -h

    usage: sk [-h] [-p PORT] [-b RATE] [-U URL] [-t SEC] [-P] [-N]
              [-L DIR] [-l] [-u] [-D]

    SerialKiller does serial things.

    options:
      -h, --help           show this help message and exit
      -p, --port PORT      default: autodetect
      -b, --baudrate RATE  default: 115200
      -U, --url URL        url eg: socket://host:port
      -t, --timeout SEC    default: 0.1
      -P, --print_cchars   convert incoming control chars to
                           printable
      -N, --send_newline   send newline on enter
      -L, --log_dir DIR    specify log dir
      -l, --lock           free serial port
      -u, --unlock         reconnect to serial
      -D, --debug          enable debugging
