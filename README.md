BETA 0 MARKET RISK DOCUMENTATION GENERATOR

OBJECTIVE

Build a minimal Python tool that generates a static HTML documentation
website from a collection of Markdown files.

The purpose of this version is only to demonstrate the core concept.

The tool must:

-   Read Markdown nodes.
-   Build a documentation graph.
-   Generate one HTML page per node.
-   Generate a profile graph page.
-   Allow navigation between pages using hyperlinks.
-   Support notation reuse inside model documentation.
-   Support local MathJax.
-   Not depend on Mermaid.
-   Not depend on MkDocs.
-   Not depend on a web server.
-   Produce a completely static website.

TERMINOLOGY

Node: a Markdown file. Page: the generated HTML file corresponding to a
node.

One node always generates exactly one page.

NODE TYPES

1.  Data node
2.  Model node

GRAPH RULES

Allowed: Data -> Model Model -> Data

Forbidden: Data -> Data Model -> Model

A model node must define inputs and outputs, and these must always be
data nodes.

NOTATION SYSTEM

Notation belongs only to data nodes.

Model nodes can reference notation using aliases.

Example:

{{ returns.tenor }} -> T

Object notation:

{{ returns }}

resolves to the object symbol defined in the data node.

PROFILE

A profile defines: - documentation root node - producer choices

Traversal starts from the root node and proceeds upstream.

PAGE UNIQUENESS

One node always generates one page.

Never generate multiple pages for the same node.

DATA PAGE CONTENT

-   title
-   markdown content
-   notation table
-   possible producer models
-   possible consumer models
-   selected producer in current profile

MODEL PAGE CONTENT

-   title
-   markdown content
-   inputs
-   outputs
-   notation tables for inputs
-   notation tables for outputs

TEXT GRAPH PAGE

The main navigation page is profile_graph.html.

Represent the graph as text relationships with clickable links.

LOCAL MATHJAX

Use local MathJax assets copied into the generated site.

OUTPUT STRUCTURE

site/ index.html profile_graph.html style.css assets/ mathjax/
DataNode.html ModelNode.html

DEPENDENCIES

Python standard library PyYAML Markdown

BUILD PROCESS

1.  Read profile.
2.  Read all markdown nodes.
3.  Build producer/consumer relationships.
4.  Resolve selected profile graph.
5.  Generate HTML page for each selected node.
6.  Generate profile_graph.html.
7.  Generate index.html.
8.  Copy local MathJax assets.
9.  Write site output directory.

END OF BETA 0 SPECIFICATION
