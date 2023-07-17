# Tree Sitter Playground

[https://sambacha.github.io/tree-sitter-playground/](https://sambacha.github.io/tree-sitter-playground/)

## Overview

Application Logic for syntax highlighting and tree query.

    Iterates over the abstract syntax tree, rendering it incrementally.  

Parameters:

- i: Integer counter, starts at 0 and increments each iteration
- currentRenderCount: The current parse count, used to detect if the parse has changed

Functionality:

- Loop that breaks when the parsing changes
- Every 10,000 iterations, yields execution to avoid blocking the UI
- Checks if parseCount has changed compared to currentRenderCount
  - If so, deletes the cursor and stops rendering
  - This allows the render to restart cleanly when the parse changes

## Playground.js 

1. `runTreeQuery` is a function that takes two arguments, `startRow` and `endRow`. These arguments represent the range of rows that are visible in the editor.
2. If `endRow` is not given as an argument, then it is set to `null` using the default parameter value `endRow = null`.
3. If `endRow` is `null`, then the viewport's `from` and `to` values are used to set `startRow` and `endRow` respectively.
4. The viewport is the range of rows that are actually visible in the editor, given the current scroll position. The `codeEditor` object has a method called `getViewport` that returns an object with `from` and `to` properties.
5. The `operation` method is called on the editor to make sure all the marks are cleared and re-added at the same time. This prevents the marks from being cleared and re-added one at a time, which can cause the editor to flicker.
6. The `getAllMarks` method is called on the editor to get all the marks that are currently set on the editor. The `clear` method is called on each mark to remove it from the editor.
7. If there is a tree and a query, then the `captures` method is called on the query object. This method takes the root node of the tree, the start position (row and column) and the end position (row and column) as arguments. It returns an array of captures that are found in the given range, each of which has a name and a node.
8. The `markText` method is called on the editor to mark the text between the start and end positions. The `css` option is used to set the mark's style.


## License

The MIT License (MIT)

Copyright (c) 2018-2023 Max Brunsfeld
Copyright (c) 2023 Sam Bacha
