```bash
SIGPROCMASK(2)              BSD System Calls Manual             SIGPROCMASK(2)

NAME
     sigprocmask -- manipulate current signal mask

SYNOPSIS
     #include <signal.h>

     int
     sigprocmask(int how, const sigset_t *restrict set, sigset_t *restrict oset);

DESCRIPTION
     The sigprocmask() function examines and/or changes the current signal mask (those signals that are blocked from delivery).  Signals are blocked if they are members of the current signal mask set.

     If set is not null, the action of sigprocmask() depends on the value of the parameter how.  The signal mask is changed as a function of the specified set and the current mask.  The function is specified by
     how using one of the following values from <signal.h>:

     SIG_BLOCK    The new mask is the union of the current mask and the specified set.

     SIG_UNBLOCK  The new mask is the intersection of the current mask and the complement of the specified set.

     SIG_SETMASK  The current mask is replaced by the specified set.

     If oset is not null, it is set to the previous value of the signal mask.  When set is null, the value of how is insignificant and the mask remains unset providing a way to examine the signal mask without
     modification.

     The system quietly disallows SIGKILL or SIGSTOP to be blocked.

RETURN VALUES
     A 0 value indicated that the call succeeded.  A -1 return value indicates an error occurred and errno is set to indicated the reason.

ERRORS
     The sigprocmask() call will fail and the signal mask will be unchanged if one of the following occurs:

     [EINVAL]           how has a value other than those listed here.

SEE ALSO
     kill(2), sigaction(2), sigsuspend(2), sigsetops(3)

STANDARDS
     The sigprocmask() function call is expected to conform to IEEE Std 1003.1-1988 (``POSIX.1'').

BSD                              June 4, 1993                              BSD
(END)
```