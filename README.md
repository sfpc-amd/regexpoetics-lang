Regular Expressions DSL
=======================

This document sketches out a basic domain-specific language (DSL) for converting text into values that can be used for music synthesis, etc.

This idea is connected to a project called [_Regular Expressions_](https://github.com/notioncollective/regexpoetics) by Jonathan Wohl and Andy Dayton, a simple tool for writing text live and using it to generate audio. 

![Regular Expressions](https://github.com/notioncollective/regexpoetics/raw/master/public/img/screen.png)

[Video screen capture of a _Regular Expressions_ performance.](https://vimeo.com/120005565)

The language itself would be implemented using JavaScript and either [peg.js](https://github.com/pegjs/pegjs) or [ohm](https://github.com/cdglabs/ohm).

## Semantics

The semantics of this language are based on the final goal — using words to generate sounds. There are three main steps in that process.

1. Finding patterns within a larger text
2. Filtering those patterns or extracting information from them
3. Sending the resulting information out to be interpretated


## Syntax

This is a very early draft of potential syntax, subject to quite a bit of change.


Expressions can be written in LISP-y syntax:

```
(/channel (f:notes (pattern all /(.*)/)))
```

Or in arrow notation

```
-> all f:notes /channel
```

Or a combo

```
-> (pattern /(.*)/) f:notes /channel
```

Define a pattern

```
(pattern all /(.*)/)
```

Run a filter

```
-> all f:notes
```

Send to OSC channel

```
-> all f:notes /channel
```


## Core Functionality

* **Define Patterns** - use regular expressions to define patterns that can include groupings
* **Output** - output data to various channels. most likely will be sent to WebSocket which can then be sent via OSC
* **Define Filters** - define JavaScript functions that will filter incoming data and return modified data. filters can be synchronous or asynchronous.

## Potential Addons

 * **Notes Filter** - parses data for "note" letters (A-G) and returns only the note data
 * **Word Distance Filter** - given a set of two words, uses NLP to generate a numeric value based on word distance.
 * **Sentiment Analysis Filter** - given a word or a set of words, run sentiment analysis and return a numeric value.
