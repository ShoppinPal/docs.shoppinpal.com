# Sequence Diagrams

### What are they?

{% mermaid %}
graph TD;
  A-->B;
  A-->C;
  B-->D;
  C-->D;
{% endmermaid %}

### Resources

* [Visual Syntax for Sequence Diagrams](https://www.smartdraw.com/sequence-diagram/#sequenceDiagramNotations)
* Generators with a domain specific language to draw them:
    * http://sequencediagram.org/
    * https://www.websequencediagrams.com/
    * https://knsv.github.io/mermaid/#activations
    * https://bramp.github.io/js-sequence-diagrams/
        * [GitHub project](https://github.com/bramp/js-sequence-diagrams)
        > A simple javascript library to turn text into vector UML sequence diagrams. Heavily inspired by websequencediagrams.com, who offer a serverside solution. We use Jison to parse the text, and Snap.svg to draw the image.
* GitBook plugins for generating sequence diagrams:
    * https://github.com/gmassanek/gitbook-plugin-js-sequence-diagram
        * https://github.com/gmassanek/gitbook-plugin-js-sequence-diagram/issues/4
* Animate Sequence diagrams
    * This [video](https://youtu.be/UJxIPCylCos?t=4) suggests that someone accomplished this task, just not sure how, need to look deeper.
    * This [gist](https://gist.github.com/jzaeske/e2de8b14142818f8d8f5e74e8b6ae2b0) again suggests that someone was able to animate the sequence diagram in `reveal.js`
    * This [issue](https://github.com/hakimel/reveal.js/issues/1906) doesn't have to do with animations but it suggests that people often embed and use sequence diagrams with `reveal.js`