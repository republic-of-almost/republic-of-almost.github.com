---
layout:     post
title:      Virtual Memory
date:       2018-08-19
summary:    Allocating virtual memory in windows
categories: C/C++
---

Virtual memory has some pretty cool tricks, however what are the basics of just
using it.

{% highlight c %}
/* valloc.c */

#include <Windows.h>

struct thing {
        int i;
};

int
main() {

        /* allocates the addresses but not the memory */
        LPVOID addr = VirtualAlloc(
                NULL,
                sizeof(struct thing) * 1000000000,
                MEM_RESERVE,
                PAGE_NOACCESS);

        /* we need the page size */
        SYSTEM_INFO sys_info;
        GetSystemInfo(&sys_info);


        /* reserve the memory, but it doesn't allocate until write,
           this allocates 2 pages of memory */
        addr = VirtualAlloc(
                addr,
                sys_info.dwPageSize * 2,
                MEM_COMMIT,
                PAGE_EXECUTE_READWRITE);

        /* cast the pointer then write */
        struct thing *th_array = (struct thing*)addr;

        th_array[0].i = 123;

        return 0;
}

{% endhighlight %}

Care must be taken that you only write within the pages you have allocated in the second call.

[MSDN:VirtualAlloc](https://msdn.microsoft.com/en-us/library/windows/desktop/aa366887(v=vs.85).aspx)