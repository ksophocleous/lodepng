LodePNG for C (ISO C90) and C++
==

LodePNG is a PNG image decoder and encoder, all in one, no dependency or linkage to zlib or libpng required. It's made for C (ISO C90), and has a C++ wrapper with a more convenient interface on top.

See lodepng.h for documentation.

official website http://lodev.org/lodepng

Note
==
This fork contains small changes to the original lodepng, in particular the include directive in your code should look like this:
```C++
#include <lodepng/lodepng.h>
```

instead of just
```C++
#include <lodepng.h>
```

Other than that everything else should be the same. 
It build using cmake.

I will eventually get around adding some of the examples from the original site + build the unit tests (ctest)
