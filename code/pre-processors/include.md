# #include

\#include This directive is used to include header files in your program. There are two ways to use it:

```cpp
#include <iostream>  // For standard library headers
#include "myheader.h"  // For your own headers
```

### difference between <> and "" while including a header

## For including header files using \`<>\`

All header files, either available in standard/system or inside include folder of CPP project can be included using <>

Even `<iostream>` file is same as C's `<studio.h>` i.e. it appends `.h`, designers of CPP decided to not mark them with `<iostream.h>` extension, maybe to differentiate CPP header files from C header file.

## For including header files using \`""\`

This type of import we can used for module local header files, if a header file is only applicable to your project at a single place or just that folder, you can create a header file locally and import it as `#include<myheader.h>`&#x20;

You can learn more about why we need header files in the first place here.
