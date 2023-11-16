# Download and install BCM2835.h library V 1.73 on a RPi 4 with RPi OS

## 1. Install the library
To install the library i followed the tutorial @ https://raspberry-projects.com/pi/programming-in-c/io-pins/bcm2835-by-mike-mccauley, i put it here for a backup in case it get lost and for ease use in case u need it.

**U can skip the Downloads steps of the guide by downloading the bcm2835.h library (v 1.73) from my repo and place it into ur Desktop, then jump to the "./configure" bash command**


### Download steps
In the commands below change the .XX to match the current library version number, e.g. “.37”.

If you are using the GUI then open the command prompt using Menu > Other > LXTerminal

Using your RPi download the .tar.gz file from the library page to your “/home/pi/” root directory.  You can do this using wget on the command line:

```bash
cd /home/pi/
```

```bash
wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.XX.tar.gz
```

### Install steps
Install the library files using the following commands

Unzip the downloaded file (Change the file version number to match your downloaded version)


```bash
tar zxvf bcm2835-1.XX.tar.gz
```

The files will be unzipped into a folder called “/home/pi/bcm2835-#.#” where # is the version number. (The following instructions are based on the instructions in the bcm2835.h file so if something doesn’t work check there to see if the instructions have changed)

Change to the directory the files we’re unzipped into (Change the directory version number to match your downloaded version)

```bash
cd bcm2835-1.XX
```

Run the configure exe

```bash
./configure
```

Execute the makefile

```bash
make
```

Then

```bash
sudo make check
```

Then

```bash
sudo make install
```

(The sudo is needed to elevate permissions to the root user)

The library is now ready to use.

## 2. Using the Library In A Geany Project

Including the library header file

```C
#include <bcm2835.h>
```

When you compile you also need to include -lbcm2835 so the libraries object file is added to the final compilation.
For example at the command line:

gcc clk.c -o clk -lbcm2835

If u are using Geany u can modify the build command into the IDE.
To do that, click on the arrow near the build button, select *set build commands* and type into the build command window:

```bash
gcc -Wall -o "%e" "%f" -lbcm2835
```
to add BCM2835 library to all compilation (for those source file who includes that library in the code).

# Not always safe, do that only if u know what u are doing!
U can also modify the launch command and add whatever u need/want, for example u can add

```bash
sudo
```
before the build/launch command to do that operations as root user. 

# Skip the next part
~In a simple makefile for a project with a single file called main.c:

all: output_file_name

output_file_name: main.o
	gcc main.o -lbcm2835 -o output_file_name

main.o: main.c
	gcc -c main.c

clean:
	rm -rf *o output_file_name~
