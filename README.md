# SerialKiller

A better serial terminal written in Python3

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
