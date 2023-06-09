
# setresuid

## Intro
setresuid - set real, effective, and saved user IDs of the calling process

## Description
The setresuid system call is used to set the real, effective, and saved user IDs of the calling process. The parameters ruid, euid, and suid define the user IDs that the calling process should assume. The parameters can either be passed directly as integers or can be set to the constant value -1, which indicates that the calling process should retain its current user ID.

The use of setresuid is primarily to enable privilege elevation - that is, to allow a process to assume an effective user ID greater than its real user ID. In particular, this can be done to temporarily assume the root user ID while executing a particular task.

At user-level, the setresuid system call is equivalent to the setreuid function call.

## Arguments
* `ruid`:`uid_t` - Real user ID associated with the calling process. 
* `euid`:`uid_t` - Effective user ID associated with the calling process. Will take on a value less than or equal to the real user ID.
* `suid`:`uid_t` - Saved user ID associated with the calling process. Can take on any value, regardless of the real or effective user IDs.

### Available Tags
* K - Originated from kernel-space.
* U - Originated from user space (for example, pointer to user space memory used to get it)
* TOCTOU - Vulnerable to TOCTOU (time of check, time of use)
* OPT - Optional argument - might not always be available (passed with null value)

## Hooks
### do_setresuid
#### Type
Kprobes.
#### Purpose
To track any changes in user ID made with the setresuid system call.

## Example Use Case
One example use case for the setresuid system call would be to temporarily assume the root user ID for a particular task. For example, in a banking program, the process might need to temporarily assume the root user ID in order to read a file containing the bank's account information.

## Issues
Using setresuid can be a security risk, as it can be used to gain elevated privileges. It is important to ensure that any user IDs that are set with setresuid are set back to the original value when no longer needed. 

## Related Events
The setreuid system call is very closely related, and is functionally equivalent at user-level.

> This document was automatically generated by OpenAI and needs review. It might
> not be accurate and might contain errors. The authors of Tracee recommend that
> the user reads the "events.go" source file to understand the events and their
> arguments better.
