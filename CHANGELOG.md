# Changelog
All notable changes to the project will be documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Fortran Standard Search 0.6] 2022-10-26

### Added
- `pdfgrep` options `--color always --cache`. Using the cache speeds dramatically the search when the command is used several times.
- `${viewer}` and `${vieweropts}` constants to choose easily a PDF viewer.
- Options can now be added to `fss`: the `-h` option will call the `usage()` function.

### Changed
- The `pdfgrep` options are now set up using their full name for clarity.


## [Fortran Standard Search 0.5] 2022-10-25

### Added
- Initial commit.
