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
to -- it's huge!). So first::

  $ ln -s ~colleague/bigdir .

Now I have a symlink `bigdir -> ~colleague/bigdir`. I'm actually
interested in modifying `bigdir/projects/superduper/data` but letting
`bigdir/logs`, `bigdir/auxiliary_stuff` and so on stay there. So I just:
```
  $ lnedit bigdir/projects/superduper/data
```
Ta-da! Now I have:
```
  bigdir/
  bigdir/logs -> ~colleague/bigdir/logs
  bigdir/auxiliary_stuff -> ~colleague/bigdir/auxiliary_stuff
  bigdir/projects/
  bigdir/projects/baby_steps ->  ~colleague/bigdir/projects/baby_steps
  bigdir/projects/superduper/
  bigdir/projects/superduper/f1 -> ~colleague/bigdir/projects/superduper/f1
  bigdir/projects/superduper/f2 -> ~colleague/bigdir/projects/superduper/f2
  bigdir/projects/superduper/data
```
I can modify `data` and enjoy using all the other files without having
copied anything else, and still have the main program run using it
all, my colleague's files and my modified files.
