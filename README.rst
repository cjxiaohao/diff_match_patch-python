=============================================================================
diff_match_patch
Python module based on google-diff-match-patch's C++ port
=============================================================================

google-diff-match-patch is a Google library for computing differences between text files:

 http://code.google.com/p/google-diff-match-patch
 
This project builds an extension module for Python using google-diff-match-patch's C++ implementation.
Although google-diff-match-patch has a pure Python implementation, I have a need for speed.

Dependencies
------------

Build Prerequisites:

* Python development headers (Debian package python-dev)

* Qt 4 development libraries (Debian package: libqt4-dev)

Runtime Prerequisitves:

* Qt 4 Core (Debian package: libqtcore4)
 		
Build
-----

Build the binary module using::

 python setup.py install
 
Or you may find pre-built binaries stored in the git repository in the build directory.
Your mileage may vary with these depending on whether your system is compatible.

Example
-------

Example usage::

 import diff_match_patch
 
 left_text = "this is a test"
 right_text = "this is not a test"
 
 diff = diff_match_patch.diff(left_text, right_text)
 
 for op, length in diff:
	if op == "-":
		print "next", length, "characters are deleted"
	if op == "=":
		print "next", length, "characters are in common"
	if op == "+":
		print "next", length, "characters are inserted"

Options
-------

op_list = diff_match_patch.diff(left_text, right_text[, timelimit=0][, checklines=False][, counts_only=True])

left_text and right_text are strings (if Unicode, the string is converted
to a str using the default encoding).

The optional timelimit specifies an upper bound on the amount of time
to compute the diff, in seconds, or zero (the default) to work on the
diff indefinitely. According to the Google docs, the diff will stop
working after the time is exceeded and will return a valid diff, but
it might not be the best one.

If checklines is True, the diff will do line-by-line comparisons first.

If counts_only is False, then instead of returning tuples of (op, length),
return tuples of (op, text) that gives the text needed to re-create
right_text from left_text.

