## Trace

Gives us the big picture of what happens when a request is made to an application

## Span
A span is a unit of work, or operation. It is usually a function call or a part of a function, whatever is relevant.

A span is part of a trace. 

Spans can be `root spans` (no parent id) or child spans. You can wrap one in another as you see fit.