# Fortran Standard Search

`fss` is a small shell script searching a string in the titles of the subsection of the Fortran standard, and opening the pages in a PDF viewer. It is based on `pdfgrep`, `cut` and `okular`.

You can use the PDF of the official ISO standard or a J3 working document (see https://j3-fortran.org/doc/year/). Put the path to the PDF in the `standard` constant at the top of the script and the page of the index in the `index_page` constant.

Then search for example the `ABS` intrinsic by typing:

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


# Notes

- `fss` uses the  `--ignore-case` option of `pdfgrep`.
- If no string is passed, `fss` opens the index of the standard.
- If the string is not found, `fss` opens the index of the standard.


# TODO

- An `--ignore-case` option could be added as it could be useful to take case into account (the Fortran intrinsics are generally in uppercase in the standard).
- A `--help` option could be added.


# Other PDF viewers
With GNOME evince, you can use the `-i` option:

```bash
evince -i ${that_page} "${standard}" &
```

But only one page will be opened.


# References
* Discussion at the origin of this project: https://fortran-lang.discourse.group/t/navigating-the-fortran-standard-document/4597
