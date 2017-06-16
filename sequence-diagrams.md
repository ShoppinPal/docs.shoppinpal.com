# Sequence Diagrams

### What are they?

``` sequence
Title: Current Architecture
Browser->Webserver: Normal line
Webserver-->Notifier: Dashed line
Notifier->>Queue: Open arrow
Queue-->>Worker: Dashed open arrow
```

### Resources

* [Visual Syntax for Sequence Diagrams](https://www.smartdraw.com/sequence-diagram/#sequenceDiagramNotations)
* Generators with a domain specific language to draw them:
    * http://sequencediagram.org/
    * https://www.websequencediagrams.com/
    * https://bramp.github.io/js-sequence-diagrams/
        * [GitHub project](https://github.com/bramp/js-sequence-diagrams)
        > A simple javascript library to turn text into vector UML sequence diagrams. Heavily inspired by websequencediagrams.com, who offer a serverside solution. We use Jison to parse the text, and Snap.svg to draw the image.
* GitBook plugins for generating sequence diagrams:
    * https://github.com/gmassanek/gitbook-plugin-js-sequence-diagram