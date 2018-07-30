---
layout:     post
title:      Hello World in C
date:       2018-07-29
summary:    The ubiquitous hello world blog post
categories: C/C++
---

The simplist C program ...


{% highlight c %}

/* hello.c */

#include <stdio.h>

int
main() {
        printf("Hello World\n");

        return 0;
};

{% endhighlight %}


Outputs ...


{% highlight plaintext %}

Hello World

{% endhighlight %}


Compile and run with GCC

{% highlight bash %}

gcc hello.c && ./a.out

{% endhighlight %}

or Clang

{% highlight bash %}

clang hello.c && ./a.out

{% endhighlight %}
