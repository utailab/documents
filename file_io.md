# File I/O

## Introduction

If programming was only about calculating some values and storing them in the
memory, life would be much easier but boring at the same time! Almost every non
trivial task in programming requires some kind of *I/O*. But what exactly is
I/O? I/O stands for *Input/Output*. In programming jargon, input means reading
some values from a device and output means writing some values to a device.
Device is a general word that not only refers to monitors, hard disk drives,
CD-ROMs, etc but also USB ports, network cards and almost everything that is a
part of a computer.

To be able to do I/O on any device such as hard disks or monitors, we must ask
the operating system to the I/O on behalf of us. Therefore programming
languages library functions and classes use the operating system services to do
the I/O. Based on this, we should know how the operating system handles the
devices and what services it offers to work with the them.

## I/O the Unix Way

On Unix-like operating systems such as Linux, almost all devices are
represented as files (there are exceptions to this however). A file is a
conceptual entity that can be opened, read, written and closed just like
regular files on a hard disk. So there is no difference between a regular file
on the disk and a USB device because the operations that the operating system
offers are the same for both. Consequently, to do I/O on any regular file or
device (sometimes called special file), we must first **open** it, then do the
**reading** or **writing** and finally **close** it.

## I/O in Programming Languages

Building on what was said, programming languages offer these operations (open,
read, write, close) on their own way through library functions and classes.

An example in Python:

```python
>>> file = open('README.md', 'r')
>>> file
<_io.TextIOWrapper name='README.md' mode='r' encoding='UTF-8'>
>>> content = file.read()
>>> content
'# documents\nThoughts on programming\n'
>>> file.close()
>>> file
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.
```
And C:

```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main()
{
    int file, count;
    char buffer[1024];

    file = open("README.md", O_RDONLY);
    count = read(file, buffer, 1024);
    buffer[count] = '\0';
    printf("%s", buffer);
    close(file);

    return 0;
}
```

You can see that the operations are the same: open, read, close. Only the
details vary.
