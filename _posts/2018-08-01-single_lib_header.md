---
layout:     post
title:      Single Header Libs 
date:       2018-08-01
summary:    Not the template / lazy header kind
categories: C/C++ 
---

Single file header and impl libs have become popular, from a users point of view
they tend to look like this.

{% highlight c %}

/* some src.c file */

#define SOME_LIB_INCLUDE_IMPL
#include "some_lib.h"

#include <stdio.h>

int main() {
        printf("%d\n", some_lib_function());

        return 0;
}

{% endhighlight %}

From the point of view of the library maintainer the code is structured 
something like this (more or less).


{% highlight c %}

/* some_lib.h */

/* interface */

#ifndef USUAL_INC_GUARD
#define USUAL_INC_GUARD

int
some_lib_function();

#endif

/* impl */

#ifdef SOME_LIB_INCLUDE_IMPL
#ifndef SOME_LIB_IMPL_GUARD
#define SOME_LIB_IMPL_GUARD

int
some_lib_function() {
        return 42;
}

#endif
#endif

{% endhighlight %}


So now in one of your source files you define `SOME_LIB_INCLUDE_IMPL` before
including the library header. 


Compile and run,

{% highlight bash %}

gcc src.c && ./a.out

{% endhighlight %}

outputs ...

{% highlight plaintext %}

42

{% endhighlight %}

This can make distributing small libs nice. Its a single file, and can have its
source compiled into a source file. Which is preferable than inline functions or
(shudder) C++ templates.

Some cool examples ...

- [STB](https://github.com/nothings/stb)
- [STB Maintained List](https://github.com/nothings/single_file_libs)
