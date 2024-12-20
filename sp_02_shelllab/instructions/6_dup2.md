```bash
DUP(2)                      BSD System Calls Manual                     DUP(2)

NAME
     dup, dup2 -- duplicate an existing file descriptor

SYNOPSIS
     #include <unistd.h>

     int
     dup(int fildes);

     int
     dup2(int fildes, int fildes2);

DESCRIPTION
     dup() duplicates an existing object descriptor and returns its value to the calling process (fildes2 = dup(fildes)).  The argument fildes is a small non-negative integer index in the per-process descriptor
     table.  The value must be less than the size of the table, which is returned by getdtablesize(2).  The new descriptor returned by the call is the lowest numbered descriptor currently not in use by the
     process.

     The object referenced by the descriptor does not distinguish between fildes and fildes2 in any way.  Thus if fildes2 and fildes are duplicate references to an open file, read(2), write(2) and lseek(2) calls
     all move a single pointer into the file, and append mode, non-blocking I/O and asynchronous I/O options are shared between the references.  If a separate pointer into the file is desired, a different object
     reference to the file must be obtained by issuing an additional open(2) call.  The close-on-exec flag on the new file descriptor is unset.

     In dup2(), the value of the new descriptor fildes2 is specified.  If fildes and fildes2 are equal, then dup2() just returns fildes2; no other changes are made to the existing descriptor.  Otherwise, if
     descriptor fildes2 is already in use, it is first deallocated as if a close(2) call had been done first.

RETURN VALUES
     Upon successful completion, the new file descriptor is returned.  Otherwise, a value of -1 is returned and the global integer variable errno is set to indicate the error.

ERRORS
     The dup() and dup2() system calls will fail if:

     [EBADF]            fildes is not an active, valid file descriptor.

     [EINTR]            Execution is interrupted by a signal.

     [EMFILE]           Too many file descriptors are active.

     The dup2() system call will fail if:

     [EBADF]            fildes2 is negative or greater than the maximum allowable number (see getdtablesize(2)).

SEE ALSO
     accept(2), close(2), fcntl(2), getdtablesize(2), open(2), pipe(2), socket(2), socketpair(2)

STANDARDS
     dup() and dup2() are expected to conform to IEEE Std 1003.1-1988 (``POSIX.1'').

4th Berkeley Distribution      December 1, 2010      4th Berkeley Distribution
(END)
```