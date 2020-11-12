# non_blocking_io_wrapper

## Description:

`non_blocking_io_wrapper.NonBlockingReader` is a wrapper class to
build a non blocking stream from any read stream. It can be used for
example to wrap the `stdout` pipe of a subprocess in a non blocking way.

It is a true `io.RawIOBase` subclass. Because of that, any method valid
on an input byte stream should work seamlessly. Yet, a line access
(readline, or iterator) will raise an OSError if no data is available at
call time (you can use the `select` method to test/wait for
that condition). If some data is available a line will be returned, or a
partial one if no newline is available in the buffer.

If no data is present, a read will return None instead of blocking.

### Additional methods

    drain(timeout=None)
    
Waits for the underlying stream to reach its end of file.

If timeout is given and is not None it is the maximum time in
seconds to wait.

Returns True if it succeeded or False on timeout.

It is intended to force a blocking wait after signaling an end of
communication to a peer.

    select(timeout=None)
    
Waits for data to become available.

If timeout is given and is not None it is the maximum time in
seconds to wait.

Returns True if it succeeded or False on timeout

It is intended to allow to wait for availability of some data.

## Installation

### From PyPI

Released version are normally available from PyPI. Just user `pip` to
install the last one:

    pip install non_blocking_io_wrapper
    
### From GitHUB

You can also clone the main repository from GitHUB:

    git clone https://github.com/s-ball/non_blocking_io_wrapper.git

## Contribution - development

A test package (97% coverage as of 0.5) is included in the GitHUB
repository and in the source packages on PyPI.

### Special processing for `version.py`

Versioning file is not included in the GitHUB repository because it is
generated with `setuptools_scm`. It is of course included in PyPI packages
so you should make sure to have a true git repository, or to get the sources
from PyPI. The symptom is that you get a version number of 0.0.0 ...

## Disclaimer: beta quality

It is fully functional and pass tests for Python 3.6 to 3.9 on Travis-CI.
Yet it could have a better documentation, and has not been extensively
tested.

## License

This work is licenced under a MIT Licence. See
[LICENSE.txt](https://raw.githubusercontent.com/s-ball/non_blocking_io_wrapper/master/LICENCE.txt)