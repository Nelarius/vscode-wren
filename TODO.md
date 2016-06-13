
# TODO

## Parse the inheritance case in the class definition

Currently only `(\b(foreign)\s+)?(\bclass)\s+(\w+)` is used -- this will not match the trailing `is Action {` part.

## Method highlighting

My attempt at parsing the method definition and setting the method name attribute looked like this:

```js
"method": {
    "name": "meta.method",
    "begin": "(\\b(construct|static)\\s+)?(\\w+=|\\w+|\\+|-|\\*|/|%|<=?|>=?|==|!=?|&|\\||~)",
    "beginCaptures": {
        "2": { "name": "storage.modifier" },
        "3": { "name": "entity.name.function" }
    },
    "end": "(?=})",
    "patterns": [
        { "include": "#comment" },
        { "include": "#blockComment" },
        { "include": "#keyword" },
        { "include": "#constant" },
        { "include": "#string" },
        { "include": "#variable" }
    ]
},
"foreignMethod": {
    "name": "meta.method",
    "begin": "\\b(foreign)\\s+(\\b(construct|static)\\s+)?(\\w+=|\\w+|\\+|-|\\*|\/|%|<=?|>=?|==|!=?|&|\\||~)",
    "beginCaptures": {
        "1": { "name": "storage.modifier" },
        "3": { "name": "storage.modifier" },
        "4": { "name": "entity.name.function"}
    },
    "end": "\n"
}
```

The only problem was finding the matching closing brace. Instead, the method body would end at the very first closing brace of any if-statement or block argument, causing the very next statement to be parsed as a method definition, no matter what it was.

Maybe the syntax definition for OmniSharp might be of help: https://github.com/OmniSharp/omnisharp-vscode/blob/master/syntaxes/csharp.json.

## Better string interpolation

String interpolation also needs to figure out the true closing parenthesis. Currently it breaks on expressions involving parenthesis, like method calls.
