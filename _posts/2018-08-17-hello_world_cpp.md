---
layout:     post
title:      Hello World in C++
date:       2018-08-17
summary:    C++ version of the Hello World
categories: C/C++
---

The simplist C++ program ...


{% highlight c %}

/* hello.cpp */

#include <iostream>

int
main() {
        std::cout << "Hello World" << std::endl;

        return 0;
};

{% endhighlight %}

Outputs ...


{% highlight plaintext %}

Hello World

{% endhighlight %}


Compile and run with GCC

{% highlight bash %}

g++ hello.cpp && ./a.out

{% endhighlight %}

or Clang

{% highlight bash %}

clang++ hello.cpp && ./a.out

{% endhighlight %}
