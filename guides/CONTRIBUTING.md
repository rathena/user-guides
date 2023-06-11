# Contributing To These Guides

You'd like to help us improve these guides? Great! We're always looking for new contributors to help us improve our documentation. There are many ways you can contribute, from writing new guides, improving existing guides, or even just fixing typos.

## What Can I Contribute?

There are many ways you can contribute to this project. Here are some examples:

- Writing new guides
- Improving existing guides
- Fixing typos
- Expanding explanations

## How Do I Contribute?

Contributing to this project is easy. Just follow these steps:

1. Fork this repository
2. Create a new branch for your changes
3. Make your changes
4. Commit your changes
5. Push your changes to your fork
6. Create a pull request
7. Wait for your changes to be reviewed and merged
8. Celebrate!
9. Repeat steps 2-8 as often as you like

## How Should I Write My Guide?

### Basics

We have a few guidelines for writing guides. Please follow these guidelines when writing your guide:

- Guides should be written in markdown format
- Guides should be written in a way that is easy to understand
- Guides should be written in a way that is easy to read
- Guides should be written in a way that is easy to follow
- Guides should be written in a way that is easy to translate
- Guides should be written in a way that is easy to maintain
- Guides should be written in a way that is easy to update
- Guides should be written in a way that is easy to expand
- Guides should be written in a way that is easy to improve
- That should cover it..

### File Location

The markdown files for guides need to be placed in the `/guides/` directory. The file name should be the same as the guide title, with all spaces replaced with hyphens. For example, a guide titled "How To Install rAthena" would be saved as `how-to-install-rathena.md`.

We have created some directories to help organize the guides. Please place your guide in the appropriate directory. If you are unsure where to place your guide, please ask in our [Discord server](https://discord.gg/kMeMXWEvSV).

### Markdown Guidelines

You can structure your guide any way you see fit, but we do have a few guidelines for writing markdown files to keep everything looks reasonably consistent.

#### Headings

Headings should be used to break up your guide into sections. When you use hashes `#` to create headings, you should use the following number of hashes for each heading:

- `#` - Top level heading (autogen - do not use in your guide)
- `##` - Second level heading
- `###` - Third level heading
- `####` - Fourth level heading

These headings are automatically turned into a table of contents on the guide page. This allows users to quickly jump to the section they are interested in.

#### Code Blocks

Code blocks should be used to display code. You can use code blocks to display commands, code snippets, or even entire files. To create a code block, you can use the following syntax:

    ```text
    # This is a code block
    ```

!!! tip "You can add an optional language identifier to enable syntax highlighting in your code block."

#### Inline Code

Inline code should be used to display code that is part of a sentence. To create inline code, you can use the following syntax:

    `This is inline code`

#### Links

Links should be used to link to other pages. To create a link, you can use the following syntax:

    [Link Text](https://example.com)

#### Images

Images can be used, but we recommend using them sparingly. They should be linked from a permenant hosting solution (not somewhere that deletes images after x days) and should not be pushed to this repository unless absolutely necessary. To display an image, you can use the following syntax:

    ![Image Alt Text](https://example.com/image.png)

#### Tables

Tables can be used to display data in a tabular format. To create a table, you can use the following syntax:

    | Column 1 | Column 2 | Column 3 |
    | -------- | -------- | -------- |
    | Row 1    | Row 1    | Row 1    |
    | Row 2    | Row 2    | Row 2    |
    | Row 3    | Row 3    | Row 3    |

#### Lists

Lists can be used to display data in a list format. To create a list, you can use the following syntax:

    - List Item 1
    - List Item 2
    - List Item 3

### MkDocs Goodies

Since we are using MkDocs to serve the documentation, we can get to use of the plugins and extensions it provides;

=== "Admonitions"

    Admonitions, also known as call-outs, are an excellent choice for including side content without significantly interrupting the document flow.

    **Usage**

    Admonitions follow a simple syntax: a block starts with `!!!`, followed by a
    single keyword used as a type qualifier. The content of the block follows on
    the next line, indented by four spaces:

    ``` markdown title="Admonition"
    !!! note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```

    <div class="result" markdown>

    !!! note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    </div>


    **Changing the title**

    By default, the title will equal the type qualifier in titlecase. However, it
    can be changed by adding a quoted string containing valid Markdown (including
    links, formatting, ...) after the type qualifier:

    ``` markdown title="Admonition with custom title"
    !!! note "Phasellus posuere in sem ut cursus"

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```

    <div class="result" markdown>

    !!! note "Phasellus posuere in sem ut cursus"

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    </div>


    **Removing the title**

    Similar to [changing the title], the icon and title can be omitted entirely by
    adding an empty string directly after the type qualifier. Note that this will
    not work for [collapsible blocks]:

    ``` markdown title="Admonition without title"
    !!! note ""

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```

    <div class="result" markdown>

    !!! note ""

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    </div>

    [changing the title]: #changing-the-title
    [collapsible blocks]: #collapsible-blocks

    **Collapsible blocks**

    When an admonition block is started with `???` instead
    of `!!!`, the admonition is rendered as a collapsible block with a small toggle
    on the right side:

    ``` markdown title="Admonition, collapsible"
    ??? note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```

    <div class="result" markdown>

    ??? note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    </div>

    Adding a `+` after the `???` token renders the block expanded:

    ``` markdown title="Admonition, collapsible and initially expanded"
    ???+ note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```

    <div class="result" markdown>

    ???+ note

        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    </div>

    **Inline blocks**

    Admonitions can also be rendered as inline blocks (e.g., for sidebars), placing
    them to the right using the `inline` + `end` modifiers, or to the left using
    only the `inline` modifier:

    === ":octicons-arrow-right-16: inline end"

        !!! info inline end "Lorem ipsum"

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

        ``` markdown
        !!! info inline end "Lorem ipsum"
    
            Lorem ipsum dolor sit amet, consectetur
            adipiscing elit. Nulla et euismod nulla.
            Curabitur feugiat, tortor non consequat
            finibus, justo purus auctor massa, nec
            semper lorem quam in massa.
        ```

        Use `inline end` to align to the right (left for rtl languages).

    === ":octicons-arrow-left-16: inline"

        !!! info inline "Lorem ipsum"

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

        ``` markdown
        !!! info inline "Lorem ipsum"

            Lorem ipsum dolor sit amet, consectetur
            adipiscing elit. Nulla et euismod nulla.
            Curabitur feugiat, tortor non consequat
            finibus, justo purus auctor massa, nec
            semper lorem quam in massa.
        ```

        Use `inline` to align to the left (right for rtl languages).

    __Important__: admonitions that use the `inline` modifiers _must_ be declared
    prior to the content block you want to place them beside. If there's
    insufficient space to render the admonition next to the block, the admonition
    will stretch to the full width of the viewport, e.g., on mobile viewports.

    **Supported types**

    Following is a list of type qualifiers provided by Material for MkDocs, whereas
    the default type, and thus fallback for unknown type qualifiers, is `note`[^1]:

    [^1]:
        Previously, some of the supported types defined more than one qualifier.
        For example, authors could use `summary` or `tldr` as alternative qualifiers
        to render an [`abstract`](#type:abstract) admonition. As this increased the
        size of the CSS that is shipped with Material for MkDocs, the additional
        type qualifiers are now all deprecated and will be removed in the next major
        version. This will also be mentioned in the upgrade guide.

    [`note`](#type:note){ #type:note }

    :   !!! note

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`abstract`](#type:abstract){ #type:abstract }

    :   !!! abstract

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`info`](#type:info){ #type:info }

    :   !!! info

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`tip`](#type:tip){ #type:tip }

    :   !!! tip

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`success`](#type:success){ #type:success }

    :   !!! success

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`question`](#type:question){ #type:question }

    :   !!! question

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`warning`](#type:warning){ #type:warning }

    :   !!! warning

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`failure`](#type:failure){ #type:failure }

    :   !!! failure

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`danger`](#type:danger){ #type:danger }

    :   !!! danger

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`bug`](#type:bug){ #type:bug }

    :   !!! bug

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`example`](#type:example){ #type:example }

    :   !!! example

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

    [`quote`](#type:quote){ #type:quote }

    :   !!! quote

            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et
            euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
            purus auctor massa, nec semper lorem quam in massa.

=== "FlowCharts"
    Diagrams help to communicate complex relationships and interconnections between different technical components, and are a great addition to project documentation. Material for MkDocs integrates with Mermaid.js, a very popular and flexible solution for drawing diagrams.

    ```` markdown title="Flow chart"
    ``` mermaid
    graph LR
    A[Start] --> B{Error?};
    B -->|Yes| C[Hmm...];
    C --> D[Debug];
    D --> B;
    B ---->|No| E[Yay!];
    ```
    ````

    <div class="result" markdown>

    ``` mermaid
    graph LR
    A[Start] --> B{Error?};
    B -->|Yes| C[Hmm...];
    C --> D[Debug];
    D --> B;
    B ---->|No| E[Yay!];
    ```
    </div>

    Using sequence diagrams
    Sequence diagrams describe a specific scenario as sequential interactions between multiple objects or actors, including the messages that are exchanged between those actors:

    ```` markdown title="Sequence chart"
    ``` mermaid
    sequenceDiagram
    autonumber
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
    ```
    ````

    <div class="result" markdown>

    ``` mermaid
    sequenceDiagram
    autonumber
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
    ```
    </div>

=== "Formatting"

    Material for MkDocs provides support for several HTML elements that can be used 
    to highlight sections of a document or apply specific formatting.

    ``` title="Text with suggested changes"
    Text can be {--deleted--} and replacement text {++added++}. This can also be
    combined into {~~one~>a single~~} operation. {==Highlighting==} is also
    possible {>>and comments can be added inline<<}.

    {==

    Formatting can also be applied to blocks by putting the opening and closing
    tags on separate lines and adding new lines between the tags and the content.

    ==}
    ```

    <div class="result" markdown>

    Text can be <del class="critic">deleted</del> and replacement text
    <ins class="critic">added</ins>. This can also be combined into
    <del class="critic">one</del><ins class="critic">a single</ins> operation.
    <mark class="critic">Highlighting</mark> is also possible
    <span class="critic comment">and comments can be added inline</span>.

    <div>
    <mark class="critic block">
        <p>
        Formatting can also be applied to blocks by putting the opening and
        closing tags on separate lines and adding new lines between the tags and
        the content.
        </p>
    </mark>
    </div>

    </div>

    **Highlighting text**

    Text can be highlighted with a simple syntax, which is more convenient that directly using the corresponding
    [`mark`][mark], [`ins`][ins] and [`del`][del] HTML tags:

    ``` title="Text with highlighting"
    - ==This was marked==
    - ^^This was inserted^^
    - ~~This was deleted~~
    ```

    <div class="result" markdown>

    - ==This was marked==
    - ^^This was inserted^^
    - ~~This was deleted~~

    </div>

    [mark]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark
    [ins]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ins
    [del]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/del

    **Sub- and superscripts**

    Text can be sub- and 
    superscripted with a simple syntax, which is more convenient than directly
    using the corresponding [`sub`][sub] and [`sup`][sup] HTML tags:

    ``` markdown title="Text with sub- and superscripts"
    - H~2~O
    - A^T^A
    ```

    <div class="result" markdown>

    - H~2~O
    - A^T^A

    </div>

    [sub]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sub
    [sup]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sup

    **Adding Title to Code Bocks**
    
    ````` title="Example Code"
    ``` markdown title="Markdown Title"
        Example content
    ``` 
    `````
    <div class="result" markdown>

    ``` markdown title="Markdown Title"
        Example content
    ``` 
    </div>

    **Adding keyboard keys**

    Keyboard keys can be rendered with a simple syntax.
    Consult the [Python Markdown Extensions] documentation to learn about all
    available shortcodes:

    ``` markdown title="Keyboard keys"
    ++ctrl+alt+del++
    ```

    <div class="result" markdown>

    ++ctrl+alt+del++

    </div>

    [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/#extendingmodifying-key-map-index

=== "Content Tabs"
    Sometimes, it's desirable to group alternative content under different tabs,
    e.g. when describing how to access an API from different languages or
    environments.

    Code blocks are one of the primary targets to be grouped, and can be considered
    a special case of content tabs, as tabs with a single code block are always
    rendered without horizontal spacing:

    ``` title="Content tabs with code blocks"
    === "C"

        ``` c
        #include <stdio.h>

        int main(void) {
        printf("Hello world!\n");
        return 0;
        }
        ```

    === "C++"

        ``` c++
        #include <iostream>

        int main(void) {
        std::cout << "Hello world!" << std::endl;
        return 0;
        }
        ```
    ```

    <div class="result" markdown>

    === "C"

        ``` c
        #include <stdio.h>

        int main(void) {
        printf("Hello world!\n");
        return 0;
        }
        ```

    === "C++"

        ``` c++
        #include <iostream>

        int main(void) {
        std::cout << "Hello world!" << std::endl;
        return 0;
        }
        ```

    </div>

    **Grouping other content**

    When a content tab contains more than one code block, it is rendered with
    horizontal spacing. Vertical spacing is never added, but can be achieved
    by nesting tabs in other blocks:

    ``` title="Content tabs"
    === "Unordered list"

        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci

    === "Ordered list"

        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci
    ```

    <div class="result" markdown>

    === "Unordered list"

        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci

    === "Ordered list"

        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci

    </div>

    **Embedded content**

    When [SuperFences] is enabled, content tabs can contain arbitrary nested
    content, including further content tabs, and can be nested in other blocks like
    [admonitions] or blockquotes:

    ``` title="Content tabs in admonition"
    !!! example

        === "Unordered List"

            ``` markdown
            * Sed sagittis eleifend rutrum
            * Donec vitae suscipit est
            * Nulla tempor lobortis orci
            ```

        === "Ordered List"

            ``` markdown
            1. Sed sagittis eleifend rutrum
            2. Donec vitae suscipit est
            3. Nulla tempor lobortis orci
            ```
    ```

    <div class="result" markdown>

    !!! example

        === "Unordered List"

            ``` markdown
            * Sed sagittis eleifend rutrum
            * Donec vitae suscipit est
            * Nulla tempor lobortis orci
            ```

        === "Ordered List"

            ``` markdown
            1. Sed sagittis eleifend rutrum
            2. Donec vitae suscipit est
            3. Nulla tempor lobortis orci
            ```

    </div>

=== "Data Tables"
    Data tables can be used at any position in your project documentation and can
    contain arbitrary Markdown, including inline code blocks, as well as [icons and
    emojis]:

    ``` markdown title="Data table"
    | Method      | Description                          |
    | ----------- | ------------------------------------ |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | Method      | Description                          |
    | ----------- | ------------------------------------ |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    </div>

    **Column alignment**

    If you want to align a specific column to the `left`, `center` or `right`, you
    can use the [regular Markdown syntax] placing `:` characters at the beginning
    and/or end of the divider.

    === "Left"

        ``` markdown hl_lines="2" title="Data table, columns aligned to left"
        | Method      | Description                          |
        | :---------- | :----------------------------------- |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |
        ```

        <div class="result" markdown>

        | Method      | Description                          |
        | :---------- | :----------------------------------- |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |

        </div>

    === "Center"

        ``` markdown hl_lines="2" title="Data table, columns centered"
        | Method      | Description                          |
        | :---------: | :----------------------------------: |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |
        ```

        <div class="result" markdown>

        | Method      | Description                          |
        | :---------: | :----------------------------------: |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |

        </div>

    === "Right"

        ``` markdown hl_lines="2" title="Data table, columns aligned to right"
        | Method      | Description                          |
        | ----------: | -----------------------------------: |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |
        ```

        <div class="result" markdown>

        | Method      | Description                          |
        | ----------: | -----------------------------------: |
        | `GET`       | :material-check:     Fetch resource  |
        | `PUT`       | :material-check-all: Update resource |
        | `DELETE`    | :material-close:     Delete resource |

        </div>

=== "Footnotes"
    Footnotes are a great way to add supplemental or additional information to a specific word, phrase or sentence without interrupting the flow of a document. Material for MkDocs provides the ability to define, reference and render footnotes.

    **Adding footnote references**

    A footnote reference must be enclosed in square brackets and must start with a
    caret `^`, directly followed by an arbitrary identifier, which is similar to
    the standard Markdown link syntax.

    ``` title="Text with footnote references"
    Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]
    [^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    [^2]:
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.
    ```
    
    <div class="result" markdown>

    [^1]: Footnote Example.
    [^2]:
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
        nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
        massa, nec semper lorem quam in massa.

    Footnote Example[^1] dolor sit amet, consectetur adipiscing elit.[^2]

    </div>

=== "InlineHilite"

    InlineHilite is an inline code highlighter inspired by CodeHilite.
    ```text
    Here is some code: `#!py3 import pymdownx; pymdownx.__version__`.

    The mock shebang will be treated like text here: ` #!c++ int test = 0; `.
    ```
    <div class="result" markdown>

    Here is some code: `#!py3 import pymdownx; pymdownx.__version__`.

    The mock shebang will be treated like text here: ` #!c++ int test = 0; `.
    </div>

=== "Mark"
    Mark adds the ability to insert <mark\></mark\> tags. The syntax requires the text to be surrounded by double equal signs.

    ```
    ==mark me==

    ==smart==mark==
    ```
    <div class="result" markdown>

    ==mark me==

    ==smart==mark==
    </div>

----

### Testing Your Guide

If you have MkDocs installed, you can test your guide locally by running the following command:

    mkdocs serve

This starts a local web server that you can use to view your guide. You can then visit `http://localhost:8000` in your web browser to view your guide. This is useful for testing links, images, and other formatting.

### What Happens Next?

Once you have created your pull request, it will be reviewed by a member of the documentation team or an rA Repository Maintaner. If your pull request is approved, it will be merged into the default (`master`) branch and after a few moments will be pushed automatically as a HTML file to the [Guides](https://rathena.github.io/user-guies/) website.

If your pull request is not approved, you will be given feedback on what needs to be changed before it can be merged.
