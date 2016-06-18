
# TODO

## Better string interpolation

String interpolation also needs to figure out the true closing parenthesis. Currently it breaks on expressions involving parenthesis, like method calls.

## Overloading the subscript operator

The subscript operator argument is interpreted as a method name, when it should be the parameter. This could probably be solved by a separate regex, since the subscript operator doesn't look like any of the other operator overloads.
