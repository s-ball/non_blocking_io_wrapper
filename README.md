# non_blocking_io_wrapper

##Description:

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


## Disclaimer: beta quality

All functionalities are now implemented. Yet it still lacks more
documentation, and has not been extensively tested.

## License

This work is licenced under a MIT Licence. See
[LICENSE.txt](https://raw.githubusercontent.com/s-ball/non_blocking_io_wrapper/master/LICENCE.txt)