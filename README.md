Introduction
------------

A ctypes-based adapter to libarchive. The source-code is written to be clear 
and intuitive.

Even 7-Zip is supported.

**This is a work in progress to be finished very soon.**

I could definitely use some help contributing to the completeness of this
library.


Task List
---------

| Done | Task |
|:----:| ---- |
| X | Enumerate entries |
| X | Extract entries to disk |
| X | Populate archives from disk |
|   | Populate archives from memory |
|   | Populate archives into memory |
|   | Fill-out the entry object's information/accessors |


Examples
--------

To enumerate the entries in an archive:

```python
import libarchive

with libarchive.reader('test.7z') as reader:
    for e in reader:
        # (The entry evaluates to a filename.)
        print("> %s" % (e))
```

To extract the entries from an archive to the current directory (like a normal,
Unix-based extraction):

```python
import libarchive

for state in libarchive.pour('test.7z'):
    if state.pathname == 'dont/write/me':
        state.set_selected(False)
        continue

    # (The state evaluates to a filename.)
    print("Writing: %s" % (state))
```

To build an archive from a collection of files (omit the target for STDOUT):

```python
for entry in libarchive.create(
                '7z', 
                ['/aa/bb', '/cc/dd'], 
                'create.7z'):
    print("Adding: %s" % (entry))
```