---
layout:     post
title:      GL Hello World 
date:       2018-08-25
summary:    Random clear colors 
categories: C/C++
---

In the last post we created an SDL2 window, now we are going to create some
pretty colors on the window using GL.

{% highlight c %}
static struct change_color {
        /* colors and rate of change */
        float r, dr;
        float g, dg;
        float b, db;
} demo = {0};


static int 
demo_start()
{
        demo.r = 1.f; demo.dr = 0.004f;
        demo.g = 0.5f; demo.dg = 0.008f;
        demo.b = 1.f; demo.db = 0.016f;

        return 1;
}


static int 
demo_tick()
{ 
        demo.r += demo.dr;
        demo.g += demo.dg;
        demo.b += demo.db;

        /* use trig functions to flip from 0 to 1 */
        float r = (float)cos(demo.r);
        float g = (float)sin(demo.g);
        float b = (float)cos(demo.b);

        r = (r / 0.5f) + 1.f;
        g = (g / 0.5f) + 1.f;
        b = (b / 0.5f) + 1.f;

        glClearColor(r, g, b, 1);
        glClear(GL_COLOR_BUFFER_BIT);
        return 1;
}


static int
demo_resize(int width, int height) {
        glViewport(0, 0, width, height);
        return 1;
}
{% endhighlight %}

This is about as simple a GL app as you can get. All we are doing is clearing
the backbuffer with different colors. We cycle through the RGB channels at
different rates.

The code can be found on my [github](https://github.com/PhilCK/ck_demos),
It only supports macOS and Emscripten right now. You'll have to edit the `main.c`
file to include `color_change.c`

{% highlight bash %}
./build_mac.sh
./bin/demo
{% endhighlight %}

You should see something like [this](http://cooperking.net/00_clear_color).

