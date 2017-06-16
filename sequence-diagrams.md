# Sequence Diagrams

### What are they?

``` sequence
Title: Here is a title
A->B: Normal line
B-->C: Dashed line
C->>D: Open arrow
D-->>A: Dashed open arrow
```

### Resources

* [Visual Syntax for Sequence Diagrams](https://www.smartdraw.com/sequence-diagram/#sequenceDiagramNotations)
* Generators with a domain specific language to draw them:
    * http://sequencediagram.org/
    * https://www.websequencediagrams.com/
        * Seems like the tech from this [GitHub project](https://github.com/bramp/js-sequence-diagrams) may be in use because its [GitHub Page](https://bramp.github.io/js-sequence-diagrams/) matches the visuals on `websequencediagrams.com`, very closely.
* GitBook plugins for generating sequence diagrams:
    * https://github.com/gmassanek/gitbook-plugin-js-sequence-diagram