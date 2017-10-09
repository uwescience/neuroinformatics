---
layout: post
comments: true
title:  "Scientific Code Review"
date:   2017-10-08 07:30:00 -0700
author: Ariel Rokem
---

# How to practice scientific code review

Code review is an important aspect of modern software development practice, but
there are very few resources available for scientists to learn how to do code
review, and those who try to incorporate this practice into their work struggle
to get started.

The premise of code review in the scientific context is that it is very easy to
make errors in writing code for scientific data analysis (a point made very
eloquently in the quotes mentioned
[here](http://blog.nipy.org/ubiquity-of-error.html)). Sometimes these errors are
small, and don't seriously affect the results that you report. But in the
worse-case scenario, you end up having to [retract three *Science* papers](http://science.sciencemag.org/content/314/5807/1856.long)).

Another important role that code review plays in the scientific context is that
it provides scientists with an opportunity to learn. Many scientists
(myself included) do not have the opportunity to receive formal training in
software engineering, but nevertheless end up having to write a significant
amount of software in their research. I benefitted tremendously from having my
own code reviewed as a beginning programmer (and was fortunate to have
mentors and colleagues who were inclined to review my code), and I continue to
benefit from this practice as my software development practice evolves.

This document aims to serve as guidelines for the code reviews that we will do
as part of the Neuroinformatics WG, but some of the advice below pertains to
code review in a scientific context more broadly. The hope is that this
document and discussions following it will serve as a useful point of reference
for scientists and their friends.

## What we'll talk about here

Code review refers to the practice of looking at someone else's software and
offering suggestions for improvement. While this practice is quite common in
the writing of scientific manuscripts (as evidenced by the typical
acknowledgement "We thank x, y and z for reading a previous version of this
manuscript..."), and in the preparation of talks and other presentations, it is
still not very common for scientists to look at each other's code and
offer their opinion.

The notable exception is open source software projects that use code review as
part of their development workflow. Though this is an important use of code
reviews, it is not the main topic of the current document, and I will not
discuss it in any length. Some of the things that I will mention may still
apply to this case.

The case that I mostly have in mind here is the review of code by colleagues
and collaborators on research projects, similar to the review of manuscripts,
results and presentations that are common in research groups that I have been
part of. While I don't think that this is a common practice yet, I see no
reason that it would become more common. Maybe the guidelines below will help.

## Methodology

### Asynchronous vs. synchronous reviews

There are two primary ways to conduct a code review:

#### Synchronous code review

The author of the code and the reviewer are co-located at the time of the
review. This mode of review allows for a detailed setting of the context in
which the code was written by the author, and for a line-by-line (or
chunk-by-chunk) walk-through of the elements of the code. It has the advantage
that it enables more focus on the precise feedback that the author is seeking
(see below). In addition, the rapid back and forth. Moreover, some of the
misunderstandings that are inherent to asynchronous communication can be avoided
through a rapid face-to-face conversation. Code review can get surprisingly
personal, and surprisingly acrimonious fast. The kinds of misunderstandings that
can lead code review in this direction are easier to avoid in face-to-face
communication.

### Asynchronous code review

Code is submitted for review, by email or via some other automated system, and
reviewers read it at their leisure, providing feedback in their own time-line.
One automated system that has been designed for code review are [Github pull
requests](https://help.github.com/articles/about-pull-requests/). These provide
a particularly good interface for asynchronous code review, and many open source
software projects use this mechanism to review new code contributions, before
they are merged into the main development branch of the software. Disadvantages
of asynchronous code review complement the advantages of the synchronous code
review, and revolve around the kinds of miscommunications inherent to all
asynchronous communication. But there are also clear advantages to asynchronous
code review: they require less coordination, and can be used by distributed
teams, that wouldn't realistically be able to review all code contributions in
person. Since this is the mode of review used by a large portion of the
open-source software community, it is worth learning how to receive and give
asynchronous code review through Github.

### How you can help as a code author:

Have a goal in mind (see also [Marian Petre and Greg Wilson's study on the topic](https://arxiv.org/abs/1407.5648)): If you have a specific focus
that is the purpose of the code review, make an effort to point out where you
would like to focus. For example, if there is a performance bottle-neck you
would like to discuss point to it first in the initial read-through, and then go
back to it in the detailed discussion. In this case, you might want to postpone
discussion of other aspects of the code, such as the implementation of a
mathematical formulation, or the modular design of the code. This is
particularly important in synchronous code review, which is usually more
time-bounded

Give reviewers the necessary context. In some cases, this might require you to
provide a quick explanation of your data, and how it was generated, or the
theory behind the algorithm that you are implementing. Often, presenting a few
of your use-cases for the code is going to be helpful.

Submit bite-sized chunks of code: It is reasonable to assume that you will be
able to go through no more than **200 lines of code** (see below) in a single
review session, whether synchronous or asynchronous. Even if you are submitting
your code for asynchronous review, more than 1,000 lines of code would be really
hard to review.

Fernando Perez wrote some [useful guidelines](http://fperez.org/py4science/code_reviews.html) for synchronous
code review ("the lab meeting for code "). For the purposes of our Working
Group meetings that include code reviews, we will use a protocol that is
similar to that outlined there. In particular:

- Send your code out well in advance: at least a week before we review it
together

- Again, you can point us to large amounts of code, but we can probably only
review about 50-200 lines of code in detail, so if you point us to a large
code-base, be sure to point out the part of the code where you would like us to
focus.

- Include examples of how you use the code: tests, or some simple use-cases
often help reviewers understand the context and the API better than a long
explanation ever would.

### What you should do as a code reviewer:

#### How to review

*Read the code through - first all of it, with focus on the API*

Read through the code. If you are reviewing a large amount of code, get a sense
of the intended purpose of the code first, before you dive. Just like in a
paper review, it is often useful to restate at the beginning of the review what
you think the author intended to do in this work in a few sentences. This sets
the stage for the review of the details.

Reading the tests or documentation can give you a good sense of the intended
use-cases, and the API (application programming interface). This is often a
good place to start, because comments about the API are often the ones that
will require the most dramatic changes in the code, and you can save a lot of
time for everyone by starting with those, rather than starting with requests
to fix typos, that eventually get scuttled when the API changes dramatically.

*Ask questions*

Asking questions is almost always a [good idea](http://engineering.khanacademy.org/posts/tips-for-code-reviews.htm). You
want to make sure that you understand the intentions of the code author.
Also, people like to be listened to, and asking questions is an active form of
listening.

*Read the details: focus on modularity and design*

One of the main contributions you can make as a reviewer is to pull the code
author **away** from the details, to point out the big picture of the code.
It is quite usual particularly for scientific code . A different perspective.
This might entail changes in the modularization of the code, or in its broader
design, to accommodate and enable use-cases that were not on the code author's
mind when they initially wrote the software.

*Read the details - focus on the math*

Scientific software often implements mathematical ideas. If it is called for,
make sure that you understand the mathematical ideas that are implemented and
the ways in which the math got transferred to code.

*Read the details - focus on performance*

When going through the code on this pass, take a look at parts of the code that
look like they might be performance bottle-necks. This is particularly
easy if the code author has pointed out performance issues and potential
bottle-necks. Consider what could be done to relieve these bottle-necks: has
the code author taken advantage of all the tools at their disposal? For
example, many software languages used in scientific computing provide
substantial advantages for vectorization of mathematical operations that are
repeated over large arrays. Languages may have specialized tools for speeding
up slow performance-critical code (for examples from Python, see [this blog post](http://jakevdp.github.io/blog/2013/06/15/numba-vs-cython-take-2/)). But
adopting new tools can sometimes be cumbersome. Consider the costs and benefits
of adopting a new tool when offering advice about how to improve performance.

*Read the details - focus on formatting, typos, comments, documentation and
overall code clarity*

Finally, after all the other concerns have been alleviated, you can dive into
the nitty gritty: comment about choice of variable names, typos in s
documentation, and comments, and the format and clarity of the documentation
(some of these issues will surface in the first stage, as they pertain to the
overall clarity of the author's intentions). Though you want to make sure that
the code is properly formatted, that conventions of the language and the project
are followed, and there aren't any language errors, be sure to mark comments
that are minor as such (this idea also comes from this great
[post](http://engineering.khanacademy.org/posts/tips-for-code-reviews.htm)). It
allows the author to address them, without stressing about them.

#### Other things to think about as a reviewer:

- Review small-ish chunks of code. There is
[research](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/) that shows that you can't
effectively review more than about 200-400 lines of code in one sitting.
The same research suggests that you should expect to spend about 60 minutes
reviewing 500 lines of code, and that you should take your time doing it. This
means that you should take a break after about an hour of reviewing code.  

- Be kind: remember that the code was written by a person, who expended
creative effort into writing the code. Don't be dismissive, even if this person
did things that you consider to be grave mistakes. This can be particularly
hard to remember when conducting asynchronous code review, and particularly
when reviewing a new code contribution to a project that you care a lot about.
Needless to say that this will pay off in good karma. It might also pay off in
returning contributors. Part of the charm of open-source software development
is that today's anonymous contributors is tomorrow's trusted collaborator. And
there is no cost associated with being kind. So do it.
