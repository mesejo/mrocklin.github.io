---
title: Write Tests
date: 2016-02-08
blogpost: true
author: Matthew Rocklin
category: programming
---

Tests are important for community driven open source software.
This post contains brief reasons why you should test your code, particularly if
you submit changes to existing open source projects.

## Why we don't test.

A test is an extra piece of code to verify the correctness of the code we
actually care about.

If we know that our function works then the test code is extraneous.  Because
many developers today verify code correctness through interactive sessions,
adding tests after-the-fact seems like a chore that can be skipped if time
pressure is on.  Testing feels like flossing your teeth; only theoretically
important.

This is a valid point of view. There are several ways to verify code
correctness and interactive sessions may be sufficient in some cases,
especially if your job is to write one-off scripts or notebooks for quick
analysis.

However, if you want to contribute to long term software that involves many
people collaborating over long periods of time then your tests become more
important.  Your tests will likely outlive your source-code several times over.

## Why we test

Usually we motivate testing by emphasizing the importance of verifying
present-day correctness, similar to [double entry
bookkeeping](https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system).
Verifying correctness *is* valuable, but there are several other reasons that
are just as valuable.

### Establish interfaces

Write basic interface tests before you write code.  This formally establishes
and enforces the goals of your work and forces you to think at a high-level
before you dive into low-level details.

It's hard to abstain from diving into the guts of a new problem right away.
This requires mental discipline.

### Communicate with colleagues

You can share these high-level tests with colleagues to make sure everyone is
on the same page before writing a solution.  It's far easier to understand a
function from its tests than from its source code.  Providing clean tests is a
great courtesy to your reviewers and co-workers.  This sharing process can
happen before you invest time in writing source code.

### Reduce maintenance burden

If you spend ten hours developing a contribution to a project, the project
maintainers will likely spend forty hours maintaining that contribution in the
future, especially if it is a new feature that expands the project scope rather
than a bug fix.  Tests dramatically help to reduce maintenance burden.  We
emphasize this in the following two points.

### Guard against future developers

Future developers will change your code.  They will not perfectly understand
your original intention and so will introduce bugs.  Your tests guard against
these well-meaning but imperfectly informed future developers.

### Guard against complex interactions

In a complex project your function likely depends on hundreds of other
functions and interfaces throughout the project.  These change all the time.
Tests raise a red flag whenever a proposed change would alter your
contribution.

### Enable refactoring

Software projects occasionally undergo significant internal changes.  This
often requires a small number of developers to drastically change all parts of
the code at once.  This is really only feasible if all relevant parts of the
code have decent code coverage.

Here is a [twitter quote](https://twitter.com/minrk/status/505111560394530816)
from a primary Jupyter developer:

*I never appreciate tests or dread their absence more than during a refactor.*

*--@minrk*

### Ensure current correctness

Tests ensure that the code you've just written is correct today for the use
cases you've thought about.  When you write nice tests you always find flaws in
your existing solution that you wouldn't have found otherwise.

This is the common argument usually presented in defense of testing.

### Think adversarially

Writing tests is a good time to think adversarially about your problem.  What
happens if I give a very large input here?  How about a negative number?  Oh,
what happens if the user enters a value of the wrong type; do they get a
sensible error message?  We rarely think about these issues when solving our
initial problem but they are important, especially if our code reaches
end-users.

### Force good design

Easy-to-test code separates application logic from hard-to-test components like
databases or network connections.  The burden of testing encourages us to
separate complex code from complex infrastructure so that we can test each
component in isolation.  This separation promotes future code health as well as
improved testing.

### Testing is easy

A single test that exercises the common case just once probably catches 70% of
the failures.  This probably isn't sufficient for most open-source projects but
it's comforting to know that your first few steps into testing are always the
most productive.

### Testing is hard

Good test suites take time and thought but they're very important.  Defining
the correct behavior for a complex system is just as worthwhile as designing
its implementation.

### Interactive feedback

Verifying correctness by interactive sessions can take a long time for complex
functions.  We restart our interpreter and reenter the same setup code
repeatedly.  A quick test automates this process, often providing feedback in
less than a second.  Subsecond tests, combined with tools like
[conttest](https://pypi.python.org/pypi/conttest) provide continuous feedback
as we write and save code.  Continuous feedback during coding is incredibly
productive.

### Social pressure

Finally, there is social pressure.  Few mature open source software projects
will accept untested contributions and it is generally considered a faux pas to
submit a contribution without tests.  If you have to write tests then you might
as well write them first so that they can help you during development.

Professional tip: if you interview for a job and have to do a programming
exercise, start with a few simple tests.  This helps you and the interviewer
agree on the statement of the problem, gives you rapid interactive feedback in
a stressful situation, and gives you an air of professionalism.


### Acknowledgments

This post is thanks in part to discussions with
[Martin Durant](https://github.com/martindurant).
