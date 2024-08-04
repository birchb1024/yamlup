# YAMLUP - Document markup in YAML
This is an approach to writing documents in YAML using the goyamp macro-processor. This technique will - collect and substitute variables and macros - generate the Markdown syntax - execute code snippets and insert the output in the document - read data files into a document - allow complicated processing in external programs and internally in Lua
## Yamlup File Format
Yamlup reads 100% YAML files, using YAML maps for directives.
Since a document is an ordered thing, we use a YAML list for each element of the document. A paragraph of text is a YAML string. The simplest document would therefore be
```YAML
---
- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

```

{ Forgetting the leading minus character results in the error : did not find expected '-' indicator  }
### Comments
YAML has comments which start with the hash # so ...
### Headings
Headings are denoted by a YAML map with one entry, the title of the heading.
```YAML
- h<level number>: <title line>

```

for example
```YAML
- h1: My excellent document about an interesting subject
```

### Code blocks
Yamlup has markup keys for fixed width font blocks. "code", "bash:" and "yaml:" are provided. The format is generally
```YAML
- yaml:, code: or bash: |
  <lines of code>

```

For example
```YAML
- code: |
  let Main() be [
    Ws("Hello World!*N")
  ]

```

## Generating Markdown from Yamlup format
Yamlup is converted to markdown using the Goyamp macro processor. This program scans each input file and outpust lines of text.
It first needs the macro definitions for the markup instructions, these are defined in `markdown.yaml`. The general format of the CLI command is
```shell
$ cat markdown.yaml <your document files>... | goyamp -o lines > <outputfile>.md

```

Example
```shell
cat markdown.yaml readme.yaml | goyamp -o line

```

Example, generate the Markdown and HTML of this document
```shell
cat markdown.yaml readme.yaml | goyamp -o lines | tee README.md | markdown-it /dev/stdin > README.html

```

