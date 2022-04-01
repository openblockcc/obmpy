## obmpy

This tool is modified from [ampy](https://github.com/scientifichackers/ampy), which fixes the bug that the serial port can not time out, and supports calling with python -m

MicroPython Tool (obmpy) - Utility to interact with a CircuitPython or MicroPython board over a serial connection.

Obmpy is meant to be a simple command line tool to manipulate files and run code on a CircuitPython or
MicroPython board over its serial connection.
With obmpy you can send files from your computer to the
board's file system, download files from a board to your computer, and even send a Python script
to a board to be executed.

## Installation

You can use obmpy with either Python 2.7.x or 3.x and can install it easily from
Python's package index.  On MacOS or Linux, in a terminal run the following command (assuming
Python 3):

    pip3 install --user openblock-obmpy

On Windows, do:

    pip install openblock-obmpy

Note on some Linux and Mac OSX systems you might need to run as root with sudo:

    sudo pip3 install openblock-obmpy

If you don't have Python 3 then try using Python 2 with:

    pip install openblock-obmpy

Once installed verify you can run the obmpy program and get help output:

    obmpy --help

You should see usage information displayed like below:

    Usage: obmpy [OPTIONS] COMMAND [ARGS]...

      obmpy - Adafruit MicroPython Tool

      Obmpy is a tool to control MicroPython boards over a serial connection.
      Using obmpy you can manipulate files on the board's internal filesystem and
      even run scripts.

    Options:
      -p, --port PORT  Name of serial port for connected board.  [required]
      -b, --baud BAUD  Baud rate for the serial connection. (default 115200)
      -d, --delay DELAY Delay in seconds before entering RAW MODE (default 0)
      --help           Show this message and exit.

    Commands:
      get  Retrieve a file from the board.
      ls   List contents of a directory on the board.
      put  Put a file on the board.
      rm   Remove a file from the board.
      run  Run a script and print its output.

If you'd like to install from the Github source then use the standard Python
setup.py install (or develop mode):

    python3 setup.py install

Note to run the unit tests on Python 2 you must install the mock library:

    pip install mock

## Usage

Obmpy is made to talk to a CircuitPython MicroPython board over its serial connection.  You will
need your board connected and any drivers to access it serial port installed.
Then for example to list the files on the board run a command like:

    obmpy --port /dev/tty.SLAB_USBtoUART ls

You should see a list of files on the board's root directory printed to the
terminal.  Note that you'll need to change the port parameter to the name or path
to the serial port that the MicroPython board is connected to.

Other commands are available, run obmpy with --help to see more information:

    obmpy --help

Each subcommand has its own help, for example to see help for the ls command  run (note you
unfortunately must have a board connected and serial port specified):

    obmpy --port /dev/tty.SLAB_USBtoUART ls --help

## Configuration

For convenience you can set an `AMPY_PORT` environment variable which will be used
if the port parameter is not specified.  For example on Linux or OSX:

    export AMPY_PORT=/dev/tty.SLAB_USBtoUART
    obmpy ls

Or on Windows (untested) try the SET command:

    set AMPY_PORT=COM4
    obmpy ls

Similarly, you can set `AMPY_BAUD` and `AMPY_DELAY` to control your baud rate and
the delay before entering RAW MODE.

To set these variables automatically each time you run `obmpy`, copy them into a
file named `.obmpy`:

```sh
# Example .obmpy file
# Please fill in your own port, baud rate, and delay
AMPY_PORT=/dev/cu.wchusbserial1410
AMPY_BAUD=115200
# Fix for macOS users' "Could not enter raw repl"; try 2.0 and lower from there:
AMPY_DELAY=0.5
```

You can put the `.obmpy` file in your working directory, one of its parents, or in
your home directory.
