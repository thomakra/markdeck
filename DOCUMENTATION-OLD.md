# Documentation

## author your deck

To start with *markdeck*, see [the tl;dr](/markdeck/README.md#tldr) section.

Every change you make to the ```slides.md``` file, the various config files, or the
```assets/``` subdir, triggers a rebuild of your deck.
The integrated web server then pushes these changes to your browser, so no need to
reload your slides manually.


## slides config

~The ```config``` file defines some global settings, ...~

Since v0.17, the config resides in the ```slides.md``` as well, an own section bracketed by ```---```:

    ---
    title: the nice title
    ---

    # first slide...

* title: the title of your deck *surprise*

* controls: should the navigation be rendered in lower right corner? [default: false]

* pdf: name of the pdf to be rendered (or missing when no pdf needed)

TODO: document theme, transition, pdf_size, pdf_delay, highlight_style


## slides in general

### web presentation with reveal.js

documentation of [reveal.js](https://github.com/hakimel/reveal.js/)
(see also the [promo slidedeck](http://lab.hakim.se/reveal-js/#/))

### pdf rendering with decktape

```assets/css/render-pdf.css``` gets applied when rendering the pdf.


### background shortcuts

specify the background of your slide:

* with a solid color
```
# your title {bg=COLOR}
```

* with an image

```
# your title {bg=COLOR;PATH_TO_IMAGE}
```

the text color gets set depending on the COLOR argument
(using a dark color results in white text, for example)

* with css3

```
# your title {bgcss=CSSCLASSHERE}
```

put your css definition in ```slides.css``` and give it a selector like this:
```.CSSCLASSHERE .reveal { background: ...}``` (Note: the ".reveal" part
is important here.)
If you like to have a white text color, put something like this in
```slides.css```, too:

```
.CSSCLASSHERE .reveal section > * {
    color: #fff;
    text-shadow: 1px 1px #000;
    }
```


## asciiart

codeblocks of the class "plantuml", "ditaa", "dot", or "qr" get replaced during
conversion by rendered images (in the following examples: plantuml):

    ```plantuml
    ...
    ```

The images are cached locally, changes to the codeblock or its parameters result
in a re-rendering.

the default commandline parameters for the asciiart renderer are defined
in the [render-asciiart-filter.config](example/render-asciiart-filter.config) file.

if you want to change these parameters, you can specify them as follows (note:
you have to use the slightly longer notation with curly braces):

    ```{.plantuml args="..."}
    ...
    ```

### asciiart: plantuml

* [plantuml website](http://plantuml.com)
* [language reference](http://plantuml.com/PlantUML_Language_Reference_Guide.pdf)
* [common commands](http://plantuml.com/commons)
* [common settings](http://plantuml.com/skinparam)
* [sequence diagram](http://plantuml.com/sequence-diagram)
* [example plantuml slide](https://arnehilmann.github.io/markdeck/#/plantuml)

<!-- -->
    ```plantuml
    @startuml
    Bob->Alice : hello
    Alice->Bob : oh, you again...
    @enduml
    ```

### asciiart: ditaa

* [original project](https://github.com/stathissideris/ditaa)
* [documentation](https://github.com/stathissideris/ditaa#usage-and-syntax)
* fork of ditaa, with minimal dependencies: [ditaamini @ github](https://github.com/pepijnve/ditaa.git)
* [example ditaa slide](https://arnehilmann.github.io/markdeck/#/ditaa)

<!-- -->
    ```ditaa
    +--------+   +-------+    +-------+
    |        +---+ ditaa +--->|       |
    |  Text  |   +-------+    |diagram|
    |Document|   |!magic!|    |       |
    |     {d}|   |       |    |       |
    +---+----+   +-------+    +-------+
        :                          ^
        |       Lots of work       |
        +--------------------------+
    ```

### asciiart: graphviz

* [graphviz website](http://www.graphviz.org)
* [dot language](http://www.graphviz.org/pdf/dotguide.pdf)
* [attributes](http://www.graphviz.org/content/attrs)
* [node shapes](http://www.graphviz.org/content/node-shapes)
* [arrow shapes](http://www.graphviz.org/content/arrow-shapes)
* [gallery of examples](http://www.graphviz.org/Gallery.php)
* [example graphviz slide](https://arnehilmann.github.io/markdeck/#/graphviz)

<!-- -->
    ```dot
    digraph G {
        bgcolor=transparent;
        node [style=filled,color=white];

        a -> b -> c;
        a -> c;
        b -> d;
    }
    ```

### asciiart: qr

* [libqrencode website](https://fukuchi.org/works/qrencode/)
* [example qr slide](https://arnehilmann.github.io/markdeck/#/markdeck-github)

<!-- -->
    ```qr
    https://github.com/arnehilmann/markdeck
    ```


## asciinema

* [asciinema website](https://asciinema.org)
* [html player attributes](https://github.com/asciinema/asciinema-player#asciinema-player-element-attributes)

asciinema allows you to record a terminal session in a local file, and to
replay that session within your slides.
For recording, you have to [install asciinema](https://asciinema.org/docs/installation)
locally on your machine, then start recording with ```asciinema rec assets/YOUR_SESSION_FILE_HERE.json```.

embed the player with the following code (and pay attention to the ```rows``` attribute):
```
<asciinema-player
    src="./assets/YOUR_SESSION_FILE_HERE.json"
    poster="npt:0:11"
    idle-time-limit=1
    speed=2
    rows=18
    font-size="medium"
></asciinema-player>
```


# helper

Under ```http://localhost:8081``` you find some helpfull resources, like extended asciiart characters
(• ♥ ♣ € ™ ©), an extensive list of emojis (🙄 🤔), and some background generators.

TODO: more documentation here


# for adventurous developers

```
git clone https://arnehilmann.github.io/markdeck
cd markdeck
docker run -it -v $PWD:/source:ro -v $PWD/docs:/target --rm -p 8080:8080 arne/markdeck
open http://localhost:8080
# edit slides.md, change css, add images, ...
```
*Note: the ```/source``` folder could and should be mounted read-only.*


# similar projects

* https://github.com/divshot/markdeck
