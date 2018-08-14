---
layout:     post
title:      SDL2 Tutorial 
date:       2018-08-19
summary:    SDL2 in 60 seconds 
categories: C/C++
---

SDL is a fantastic crossplatform window/input library. Here's how to get it up
and running in 60 seconds on Mac.

First we need it installed.

{% highlight bash %}
brew install sdl2
{% endhighlight %}

Once we have that installed we can create a window with the following code.

{% highlight c %}
/* sdl2.c */
#include <SDL2/SDL.h>
#include <stdio.h>

#include <OpenGL/gl3.h>

/* SDL details */
struct sdl_app {
        SDL_Window *window;
        SDL_GLContext *gl_context;
} app = {0};

  int
app_start() {
        SDL_Init(SDL_INIT_EVERYTHING);

        Uint32 flags = SDL_WINDOW_RESIZABLE |
                       SDL_WINDOW_OPENGL;

        app.window = SDL_CreateWindow(
                "Window Title", 
                SDL_WINDOWPOS_UNDEFINED,
                SDL_WINDOWPOS_UNDEFINED,
                640,
                480,
                flags 
        );

        SDL_GL_SetAttribute(
                SDL_GL_CONTEXT_MAJOR_VERSION, 4);
        SDL_GL_SetAttribute(
                SDL_GL_CONTEXT_MINOR_VERSION, 2);
        SDL_GL_SetAttribute(
                SDL_GL_CONTEXT_PROFILE_MASK,
                SDL_GL_CONTEXT_PROFILE_ES);
        SDL_GL_SetAttribute(SDL_GL_RED_SIZE, 5);
        SDL_GL_SetAttribute(SDL_GL_GREEN_SIZE, 5);
        SDL_GL_SetAttribute(SDL_GL_BLUE_SIZE, 5);
        SDL_GL_SetAttribute(SDL_GL_DEPTH_SIZE, 24);
        SDL_GL_SetAttribute(SDL_GL_STENCIL_SIZE, 8);
        SDL_GL_SetAttribute(SDL_GL_DOUBLEBUFFER, 1);
        SDL_GL_SetAttribute(SDL_GL_MULTISAMPLEBUFFERS, 2);
        SDL_GL_SetAttribute(SDL_GL_MULTISAMPLESAMPLES, 4);

        app.gl_context = SDL_GL_CreateContext(app.window);
        SDL_GL_MakeCurrent(app.window, app.gl_context);
        SDL_GL_SetSwapInterval(1);

        return app.window ? 1 : 0;
}


int
app_tick() {
        /* update SDL */
        SDL_Event evt;

        while(SDL_PollEvent(&evt)) {
                if(evt.type == SDL_QUIT) {
                        return 0;
                }
        }

        /* present */
        SDL_GL_SwapWindow(app.window);

        return 1;
}


void
app_end() {
        SDL_DestroyWindow(app.window);
        SDL_Quit();
}

int
main() {
        if(!app_start()) {
                printf("Failed to startup app\n");
                return 0;
        }
        
        while(app_tick());

        app_end();

        return 0;
}

{% endhighlight %}

Build and Run

{% highlight bash %}
clang sdl.c -I /usr/local/include/ -L /usr/local/lib/ -lsdl2 -framework OpenGL
{% endhighlight %}

You should have a Window now. MacOS makes some of this easy in particular OGL,
although the OGL is quite lacking on MacOS.

_Some things to note_
- You need to poll the events once a frame.
- Poll the events and swap the window on the same thread it was created on.


[SDL](https://www.libsdl.org/)

