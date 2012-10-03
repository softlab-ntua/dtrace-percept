# What is DTrace Percept?

A back-end for Percept that is based on DTrace rather than on the built-in
tracing machanisms of Erlang for the collection of trace information.

# How can I use DTrace Percept?

1. Run the DTrace/SystemTap script and redirect its output into a file.

    stap path/to/percept/lib/priv/dtrace/dtrace-percept.stap > trace.dat

or

    dtrace path/to/percept/lib/priv/dtrace/dtrace-percept.d > trace.dat

2. Perform the action you want to trace.

E.g.
    
    erl -noshell - eval "bang:bang(2,30)." -s init stop

3. Stop the execution of the DTrace/SystemTap script (by pressing Ctrl+C).

3. Analyze the produced trace file.

    1> percept:d_analyze("trace.dat").

4. Start the web server (as usual) and inspect the collected information using 
your favorite browser (as usual).

    1> percept:start_webserver().


# What is the current status of DTrace Percept?

Currently, the DTrace back-end of Percept traces specific events (spawn, link, 
getting unlinked, exit, active/inactive).

The back-end does not expose any flags that can be set, so that the user can
specify the pieces of trace information that should be collected.

DTrace back-end can collect information only from Erlang VM's that are started
after the execution of the DTrace/SystemTap script, and not from already 
running Erlang VM's.

