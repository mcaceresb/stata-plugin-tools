Description
-----------

Simple but useful utility functions for writing Stata plugins in C. At
the moment, the only tools included are functions for working with the
GNU Scientific Library.

Requirements
------------

- The GNU Scientific Library (GSL).
- Stata 13 or older.
- The stata plugin interface; I include a copy of SPI-2.0
  and SPI-3.0 in this repository so the sample scripts will
  compile, but you can download the official versions from
  [stata.com/plugins](www.stata.com/plugins).

Installation
------------

Copy the appropriate version of the SPI (3.0 for Stata 14 or later and
2.0 for Stata 13 or earlier) to the directory where you will compile your
Stata plugin. On your main file, add
```c
#include "st_gsltools.c"
#include "stplugin.h"
```

The second line is requried to compile the file into a Stata plugin.

Examples
---------

To compile `examples/gsltools.c` into a plugin, you have to run
```bash
CFLAGS="-Wall -shared -fPIC -DSYSTEM=OPUNIX"
gcc $CFLAGS -c -o stplugin.o stplugin.c
gcc $CFLAGS -c -o gsltools.o gsltools.c
gcc $CFLAGS  stplugin.o gsltools.o -lgsl -lgslcblas -lm -o gsltools.plugin
```

Now you can call the plugin from Stata:
```stata
sysuse auto
program examples_gsltools, plugin using("gsltools.plugin")
plugin call examples_gsltools price mpg
```

TODO
----

- [ ] Finish writing example uses of the plugin tools.

License
-------

MIT
