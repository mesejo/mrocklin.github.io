---
title: Avoid Indirection
tagline: for human readability
date: 2019-06-23
blogpost: true
author: Matthew Rocklin
category: programming
---

This post argues for avoiding indirection in community code.

We are taught to hide away details
----------------------------------

I often see code where authors abstract away details by placing them in some
external function.  Here is a toy example:

### Before indirection

```python
# main.py

if x.startswith("foo"):
    do_something_with(x)
```

### After indirection

```python
# main.py

if is_foolike(x):
    do_something_with(x)
```

```python
# utils.py

def is_foolike(x):
    return x.startswith("foo")
```

There are good reasons for this behavior:

1.  If this code is repeated several times
    it can make things more compact
2.  If this code is repeated several times
    it creates a central place for that logic
    so that it can be changed centrally in the future
3.  It hides away details that may not be relevant to the main point of the function.
    It's like a footnote in prose.
4.  It gives a name to a set of operations,
    using the function name as inline documentation
4.  If often feels cleaner and more abstract

We're taught to do this in school.
Find some chunk of functionality,
abstract it away,
move on.


The case to avoid indirection
-----------------------------

However, there is also a cost to this behavior.
When a new reader encounters this code,
they need to jump between many function definitions in many files.
This non-linear reading process requires more mental focus
than reading linear code.

This indirection isn't as much of a problem during the writing process,
the original author is focused on building up an abstraction model in their head,
and so writing this abstraction into code makes sense and feels good.
However, it's much more of a problem when a reader is asked
to inspect and understand a piece of code quickly.
This happens in two important situations:

1.  **During review**, when a reviewer is asked to verify that code is
    sensible before it can be merged into the main project.
    That reviewer probably has about a tenth as much time to spend
    as the original author does on that code.
2.  **While debugging** future issues.
    This code will eventually be involved in a bug and some completely
    different developer will have to glance at this code to figure out what's going on.
    They'll have to understand some small section this code within a few minutes
    to determine what is relevant.
    They won't be able to invest the time to understand the full thought process behind it,
    and a web of function definitions can slow down this process considerably.

Both review and debugging are far more often bottlenecks in modern community
code than is original development.  Because of this, I often encourage
developers to avoid abstraction, and "please inline this function definition".

But functions are still a good idea
-----------------------------------

Just to be clear,
there are plenty of reasons to separate complex logic into multiple functions,
particularly when there is repetition,
or when some important policy is likely to change in the future.
There is some balance to find here.

Mostly, I want authors to be aware that there is a human cost to indirection
that is felt more acutely by everyone reading the code except the original author.

Further reading
---------------

This post extends the broad theme in the post [Write Dumb Code](https://matthewrocklin.com/blog/work/2018/01/27/write-dumb-code)
