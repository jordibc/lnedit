lnedit
======

Convert a symbolic link into an editable file or directory.

If it links to a directory, it will create it and make links to all
its contents.

If it links to a file deep in a hierarchy like::

  remotedir/blabla/interestingfile

it will re-create the whole hierarchy and finally copy the target file.


Rationale
---------

One scenario where this is useful is the following (which happens
often for me!):

I am going to work on some colleague's data, the program needs to know
about (most of) it, but I don't need to modify it all (and don't want
to -- it's huge!). So first:

  $ ln -s ~colleague/bigdir .

Then I just go to the files that I want to actually edit:

  $ lnedit bigdir/projects/superduper/data

Ta-da! I can modify "data" and enjoy using all the other files without
having copied anything else, and still have the main program run using
it all, my colleague's files and my modified files.