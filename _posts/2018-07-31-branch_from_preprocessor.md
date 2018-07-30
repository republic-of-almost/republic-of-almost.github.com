---
layout:     post
title:      Branch from Preprocessor
date:       2018-07-31
summary:    When possible avoid preprocessor guards
categories: C/C++
---

I see alot of code thats written like this


{% highlight c %}

/* branch.c */

#include <stdio.h>

/* #define SOMETHING */

int
main() {

        #ifdef SOMETHING
        printf("Something\n");
        #else
        printf("No Something\n");
        #endif
        
        return 0;
};

{% endhighlight %}


Usually this is done to hide some extra feature, debug code or platform code.
It can be nicer to just branch off the preprocessor instead.

That way the compiler will always evaluate both
paths so if a particular branch goes stale you'll know about it sooner.

{% highlight c %}

/* branch.c */

#include <stdio.h>

/* toggle between 1 or zero */
#ifndef SOMETHING
#define SOMETHING 0
#endif

int
main() {

        if(SOMETHING) {
                printf("Something\n");
        } else {
                printf("No Something\n");
        }
        
        return 0;
};

{% endhighlight %}

Compile with something, 

{% highlight bash %}

gcc branch.c -DSOMETHING=1 && ./a.out

{% endhighlight %}

outputs ...

{% highlight plaintext %}

Something

{% endhighlight %}

Compile without something, 

{% highlight bash %}

gcc branch.c && ./a.out

{% endhighlight %}

outputs ...

{% highlight plaintext %}

No Something

{% endhighlight %}

There is no performance impact, the compiler is smart enough to notice the branch
is constant and throw away the other branch.

Two things to consider however

 - Its not allways possible as sometimes are trying to hide platform differences.
 - MSVS will generate a warning by default.

