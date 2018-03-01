---
layout: post
comments: true
title: "Code review: artifact rejection"
date: 2018-02-26
author: Dan Peterson
---

On Monday, February 26 we met to hear from David Caldwell to review the code for a method of removing large artifacts from electrophysiology data in humans.

For a bit of background, the Ojemann/Rao labs are interested in intracranial
electrode arrays implanted in humans for both recording and stimulation.
Recording during and immediately after stimulation presents a challenge, as an
injected signal in one electrode causes large artifacts in the other electrodes
in the array. These artifacts are many orders of magnitude greater than the
desired signal - and can even come close to saturating the amplifier.

There are a couple of approaches to these kinds of artifacts:
1)  Call it a loss and simply not use data from affected time windows,
2)  Interpolate through the affected time window, or
3)  Attempt to subtract out the artifact to reveal the underlying signal.

3 is the approach attempted here. The difficulty in this approach is in
deciding exactly what signal to subtract. To this end, David used a variation
of a Dictionary Learning approach, where we use a bank of a known artifact
signals, and select from among those the template that provides the best
artifact suppression.

Since this is a relatively young field, these approaches aren’t often described
in detail in journal articles, and are not executed in a fully reproducible
way. In preparation for an upcoming publication, and to make this method more
widely available, David created a GitHub repository with code to perform the
dictionary-learning based artifact removal method:

https://github.com/davidjuliancaldwell/artifactRejection

Most of the discussion revolved around sharing general tips for a project like
this. Some issues discussed were:

- If you post your research software on GitHub, make sure that you chose a license. If you do not, technically it is under copyright. In that vein, if you include any code from other projects, make sure to check the licenses of those projects - there may be restrictions. This is a great resource for choosing a license for your scientific software: https://choosealicense.com/

- If you distribute code and example data, try to indicate what the correct or successful output looks like (console output, figures, output files, etc). Ideally, there would be a “test” script that checks the output automatically.

- When introducing a novel computational method, it’s a good idea to also implement alternate approaches, if it’s simple to do so. This lets users help compare methods on their data easily.

In addition to these issues, there was also a discussion about what to do with
large example data files. For the purposes of this meeting David had shared a
google drive link, but that is suboptimal for a variety of reasons. A better
solution would be to host it on ResearchWorks, which is service available to UW
Researchers that provides persistent hosting for research data:
(https://www.lib.washington.edu/dataservices). Another solution may be to use
DataLad (http://datalad.org/) which is made for this purpose, and has a
git-like versioned data repository.

If you are going to post example data along with your code, try to make sure
that the file format is documented and specified, in case potential users have
a different file format and need to convert.

Another discussion centered around the user interface - GUI vs command-line.
The consensus was that command-line was preferable, but including a GUI option
can increase the user base, if there is enough time and effort available to
develop a GUI.

Finally, many attendees had some general tips for cleaning up a codebase:

- Use built-in argument parsers, or argument parsing libraries, rather than long ‘switch’ statements.

- Be consistent about CamelCase versus names_with_underscores. An exception may be to have different naming conventions for different things, like variables versus functions.

- Make sure indentation is consistent. Also, it’s good style to include comments about the end of long for-loops or conditional statements.

- Use a consistent comment header for functions, and clearly indicate which parameters are optional and which are required (i.e. have no defaults).

- With functions that have many arguments, consider passing a struct of options, and/or support using config files to pass options.

- Readme.md files in GitHub can be spruced up with advanced formatting, section headings, images, links, etc. This site is particularly helpful for writing Readme.md files (http://markdownlivepreview.com/).

Some of these suggestions have already been implemented. Overall, the most
important thing to consider is your goals. Publicly available research code can
serve two different purposes: To document a particular analysis a reproducible
way, or to make the method available to potential users. These two things
support each other, but are subtly different. For researchers with limited
time, they may chose to emphasize one aspect over another.
