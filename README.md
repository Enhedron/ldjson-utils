# ldjson-utils

Line Delimited JSON Utilities

## Installation

You'll need `/usr/bin/pypy`. It should run with most versions of python or pypy, but has been tested with pypy 2.7.3, python 2.7.6 and python 3.4.0.

Just clone the repository, and use the scripts in `bin`. There's no need to compile anything.

## ldjson-filter

Usage:

    ldjson-filter EXPRESSION [FILE]...

Filter line delimited json like grep. EXPRESSION is a python expression that evaluates to a bool. If EXPRESSION evaluates to True on a given line, the line is output on stdout. The expression is provided with a variable called `doc` for each line, which is the result of `json.loads(line)`.

### Examples

Given the following line delimited json:

    { "forename": "Charles", "surname": "Babbage", "dob": 17911226 }
    { "forename": "Ada", "surname": "Lovelace", "dob": 18151210 }

**Read from stdin**

    ldjson-filter 'doc["dob"] == 17911226 and doc["forename"] == "Charles"'

will output:

    { "forename": "Charles", "surname": "Babbage", "dob": 17911226 }

**Read from files**

    ldjson-filter 'doc["dob"] == 18151210' log1.ldjson log2.ldjson

will output:

    { "forename": "Ada", "surname": "Lovelace", "dob": 18151210 }
