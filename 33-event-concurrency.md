# Event based concurrency

Event loop

API: select(), poll()


How to receive events?

Check if there is any incoming I/O that should be attended to.

Example: web server checks if any network packets have arrived, in order to service them.

Async interfaces return immediately. 

This set of descriptors may represent network sockets to which the server is paying attention.

No locks needed -> simplicity

## Problem: blocking sys calls

What if an event requires that you issue a system call that might block?

Solution: async I/O

Applications may issue an I/O request and return control immediately to the caller before the I/O is completed.

Additional interfaces enable an app to determine if I/Os have completed.

## Another issue: state management

Manual stack management

Solution: continuation
record socket descriptor in some data structure

## More difficulties

Moving from single CPU to multiple.

Event handlers in parallel.

Critical sections arise.

Event handling without locks is not possible anymore.

Does not integrate well with paging: event-handler faults will block.

Event based code may be hard to manage over time.

