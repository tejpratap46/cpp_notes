---
description: >-
  Pragma is a Include Guards, it tells compiler whether  to include header file
  again or not
---

# #pragma

`#pragma` was introduced to remove dependency on [ifdef.md](ifdef.md "mention") for solely including header file.

```cpp
// In myheader.h
#ifndef MYHEADER_H
#define MYHEADER_H

// Header contents go here

#endif // MYHEADER_H
```

Above, as we can see here we are using `#ifndef` for including header files only once, but here we need to declare a Macro = `MYHEADER_H` to chieve this.

To overcome this unnecessary creation of a Macro, we can use `#pragma once` which does the same thing without declaring any Macro.
