# Fortran Standard Search

`fss` is a small shell script searching a string in the titles of the subsections of the Fortran standard, and opening the pages in a PDF viewer. It is based on `pdfgrep`, `cut` and `okular` (`evince` can also be used).

You can use the PDF of the official ISO standard or a J3 working document (see https://j3-fortran.org/doc/year/). Put the path to the PDF in the `standard` constant at the top of the script and the page of the index in the `index_page` constant. You can also configure your PDF viewer with the `viewer` and `vieweropts` constants.

You can search for example the `ABS` intrinsic by typing:

```bash
$ ./fss abs
355:15     16.9.2        ABS (A)
547:9      C.2.4     Abstract types (7.5.7.1)
583:19     C.10.3      Abstract interfaces and procedure pointer components (15.4, 7.5)
```

The script will call the Okular PDF viewer and open each of the pages shown in the results (here pages 355, 547, 583).

To exclude the two false results, we could also use the fact that in the standard there is generally a space between the name of the functions and the parenthesis:

```bash
$ ./fss "abs "
355:15     16.9.2        ABS (A)
```

Note that your search pattern is a regex. A consequence is that you should for example escape a parenthesis:

```bash
$ ./fss "abs \("
355:15     16.9.2        ABS (A)
```

# Options

- `-h` will print `fss` usage.


# Notes

- `fss` uses the  `--ignore-case` option of `pdfgrep`.
- If no string is passed, `fss` opens the index of the standard.
- If the string is not found, `fss` opens the index of the standard.
- With GNOME Evince and its `-i` option, if there are several results only one page will be opened.
- This script could be used with any other PDF document with the same kind of section numbering and naming.
- In FreeBSD 13.1, `pdfgrep` is available but unhappily it says that PCRE support was disabled at compilation time. Evince and Okular are available, but also `xreader` which have a `-i` option like Evince.

# TODO

- An `--ignore-case` option could be added as it could be useful to take case into account (the Fortran intrinsics are generally in uppercase in the standard).

# References
* Discussion at the origin of this project: https://fortran-lang.discourse.group/t/navigating-the-fortran-standard-document/4597
* https://pdfgrep.org/
* https://www.gnu.org/software/coreutils/manual/coreutils.html#cut-invocation
* https://en.wikipedia.org/wiki/List_of_PDF_software#Linux_and_Unix
* https://okular.kde.org/
* https://wiki.gnome.org/Apps/Evince
* https://man.archlinux.org/man/xreader.1.en
