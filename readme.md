# lnedit

Convert a symbolic link into an editable file or directory.

If it links to a directory, it will create it and make links in it to
all of its original contents.

If it links to a file deep in a directory hierarchy (like
`remotedir/blahblah/interestingfile`), it will re-create the whole
directory hierarchy and finally copy the target file.


## 📥 Installation

Just copy the `lnedit` file anywhere you want. I have it in my
`.local/bin` directory (which is in my `PATH`.)


## 💡 Rationale

This is useful for example in this case (which often happens to me):

I am going to work with some colleague's data. My program needs to know
about (most of) it, but I don't need to modify it all (and don't want
to -- it's huge!). So first:

```sh
$ ln -s /home/colleague/bigdir .
```

Now I have a symlink `bigdir -> /home/colleague/bigdir`. I'm actually
interested in modifying `bigdir/subdir/subsubdir/data` but leaving
untouched `bigdir/logs`, `bigdir/auxiliary_stuff` and so on. So I just:

```sh
$ lnedit bigdir/subdir/subsubdir/data
```

Ta-da! Now I have:

```
bigdir/
bigdir/logs -> /home/colleague/bigdir/logs
bigdir/auxiliary_stuff -> /home/colleague/bigdir/auxiliary_stuff
bigdir/subdir/
bigdir/subdir/baby_steps ->  /home/colleague/bigdir/subdir/baby_steps
bigdir/subdir/subsubdir/
bigdir/subdir/subsubdir/f1 -> /home/colleague/bigdir/subdir/subsubdir/f1
bigdir/subdir/subsubdir/f2 -> /home/colleague/bigdir/subdir/subsubdir/f2
bigdir/subdir/subsubdir/data
```

I can modify `data` and still usie all the other files without having
copied anything else. It means that my program will run using it
all, my colleague's files and my modified files.


## ⚖️ License

This program is licensed under the GPL v3. See the [project
license](license.md) for further details.
