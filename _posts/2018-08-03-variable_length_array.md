---
layout:     post
title:      Variable Length Arrays 
date:       2018-08-03
summary:    Slightly disturbing way of dealing with arrays in C
categories: C/C++
---

C can depending on how you structure things be a pain when it comes to arrays.
C++ has vectors (et al) which are super easy to use. One solution in C
(and I stress one solution). Is VLA's.

The method is to have your array as your last member, then allocate both the space
required for the struct and the array in one shot.


{% highlight c %}

/* vla.c */

#include <stdio.h>
#include <stdlib.h>


struct foo {
        int len;
        int data[0];
};


int
main() {
        struct foo *f = 0;
        
        int i;
        int arr_len = 4;
        int arr_bytes = sizeof(f->len) * arr_len);
        int total_bytes = sizeof(f) + arr_bytes;

        f = malloc(total_bytes);
        f->len = arr_len;

        for(i = 0; i < f->len; ++i) {
                f->data[i] = i + 1;
        }

        printf("Array Data: ");

        for(i = 0; i < f_len; ++i) {
                printf("%d, ", f->data[i]);
        }

        printf("\n");

        return 0;
};

{% endhighlight %}

Compile and run,

{% highlight bash %}

gcc vla.c && ./a.out

{% endhighlight %}

Outputs ...

{% highlight plaintext %}

Array Data: 1, 2, 3, 4,

{% endhighlight %}

This kinda feels hackish to me, and I think there are usually better ways, however
its cool to know you can do this.
