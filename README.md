rop-tool v2.2
====

A tool to help you writing binary exploits


### OPTIONS

```
rop-tool v2.2
Help you to make binary exploits.

Usage: rop-tool <cmd> [OPTIONS]

Commands :
   gadget      Search gadgets
   patch       Patch the binary
   info        Print info about binary
   heap        Display heap structure
   search      Search on binary
   help        Print help
   version     Print version

Try "rop-tool help <cmd>" for more informations about a command.
```

#### GADGET COMMAND

```
Usage : rop-tool gadget [OPTIONS] [FILENAME]

OPTIONS:
  --arch, -A               Select an architecture (in raw mode only)
  --all, -a                Print all gadgets (even gadgets which are not uniq)
  --depth, -d         [d]  Specify the depth for gadget searching (default is 5)
  --flavor, -f        [f]  Select a flavor (att or intel)
  --no-filter, -F          Do not apply some filters on gadgets
  --help, -h               Print this help message
  --no-color, -n           Do not colorize output
  --raw, -r                Open file in raw mode (don't considere any file format)
  
```

#### SEARCH COMMAND

```
Usage : rop-tool search [OPTIONS] [FILENAME]

OPTIONS:
  --all-string, -a    [n]  Search all printable strings of at least [n] caracteres. (default is 6)
  --byte, -b          [b]  Search the byte [b] in binary
  --dword, -d         [d]  Search the dword [d] in binary
  --help, -h               Print this help message
  --no-color, -n           Don't colorize output
  --qword, -q         [q]  Search the qword [q] in binary
  --raw, -r                Open file in raw mode (don't considere any file format)
  --split-string, -s  [s]  Search a string "splited" in memory (which is not contiguous in memory)
  --string, -S        [s]  Search a string (a byte sequence) in binary
  --word, -w          [w]  Search the word [w] in binary

```

#### PATCH COMMAND

```
Usage : rop-tool patch [OPTIONS] [FILENAME]

OPTIONS:
  --address, -a       [a]  Select an address to patch
  --bytes, -b         [b]  A byte sequence (e.g. : "\xaa\xbb\xcc") to write
  --filename, -f      [f]  Specify the filename
  --help, -h               Print this help message
  --offset, -o        [o]  Select an offset to patch (from start of the file)
  --output, -O        [o]  Write to an another filename
  --raw, -r                Open file in raw mode

```

#### INFO COMMAND

```
Usage : rop-tool info [OPTIONS] [FILENAME]

OPTIONS:
  --filename, -f      [f]  Specify the filename
  --help, -h               Print this help message
  --no-color, -n           Disable colors

```

#### HEAP COMMAND

```
Usage : rop-tool heap [OPTIONS] [COMMAND]

OPTIONS:
  --help, -h               Print this help message
  --library, -l     <l>    Specify the library path for libheap.so (default : ./libheap-x86-64.so)
  --no-color, -N           Do not colorize output
```

**Small explication about output of heap command**

Each line correspond to a malloc chunk, and the heap is dumped
after each execution of heap functions (free, malloc, realloc, calloc)

* addr: is the real address of the malloc chunk

* usr_addr: is the address returned by malloc functions to user

* size: is the size of the malloc chunk

* flags: P is PREV_INUSE, M is IS_MAPED and A is NON_MAIN_ARENA

### FEATURES
* String searching, Gadget searching, patching, info, heap visualization
* Colored output
* Intel and AT&T flavor
* Support of ELF, PE and MACH-O binary format
* Support of big and little endian
* Support of x86 and x86_64 architecture


### EXAMPLES

Basic gadget searching

* rop-tool gadget ./program 

Display all gadgets with AT&T syntax

* rop-tool gadget ./program -f att -a

Search in RAW file (not supported format)

* rop-tool gadget ./program -r

Search a "splitted" string in the binary

* rop-tool search ./program -s "/bin/sh"

Search all strings in binary

* rop-tool search ./program -a

Patch binary at offset 0x1000, with "\xaa\xbb\xcc\xdd" and save as "patched" :

* rop-tool patch ./program -o 0x1000 -b "\xaa\xbb\xcc\xdd" -O patched

Visualize heap allocation of /bin/ls command :

* rop-tool heap /bin/ls

### SCREENSHOTS

```
rop-tool gadget /bin/ls
```

![ScreenShot](https://t0x0sh.org/repo/rop-tool/screens/screen1.png)

```
rop-tool search /bin/ls -a
```

![ScreenShot](https://t0x0sh.org/repo/rop-tool/screens/screen2.png)

```
rop-tool search /bin/ls -s "/bin/sh\x00"
```

![ScreenShot](https://t0x0sh.org/repo/rop-tool/screens/screen3.png)

```
rop-tool search /bin/ls -w 0x90
```

![ScreenShot](https://t0x0sh.org/repo/rop-tool/screens/screen4.png)

```
rop-tool heap ./a.out
```

![ScreenShot](https://t0x0sh.org/repo/rop-tool/screens/screen5.png)

### DEPENDENCIES
- [capstone](http://capstone-engine.org/)

### RELEASES
- https://t0x0sh.org/rop-tool/releases/

### LICENSE
- GPLv3 license : http://www.gnu.org/licenses/gpl-3.0.txt

### AUTHOR
Tosh 

tosh -at- t0x0sh ~dot~ org

