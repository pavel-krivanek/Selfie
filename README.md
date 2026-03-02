
# Selfie

An educational, browser-based, prototype-oriented “Self-like” environment with live object outliners, a tiny VM, and a single-file workflow inspired by TiddlyWiki.

Selfie is **not** an implementation of the Self programming language. It borrows ideas (prototype objects, slots, blocks, outliners) to explore object model concepts interactively.

## Demo mindset

Selfie is designed for:
- experimenting with a **prototype object model**
- learning how **message send + delegation** works
- stepping through the idea of **activations**, **blocks**, and **slot lookup**
- editing the system live, then **saving it as one HTML file** you can reopen later

---

## Single-file “wiki-style” saving

Selfie uses a **single-HTML self-contained saving technique** in the spirit of **TiddlyWiki’s “single file wiki”** approach:
- the application code (scripts + styles) and
- the current VM “image” (objects, open outliners, UI state)

…are all stored together in one HTML file that you can download and later reopen to continue where you left off.

If you’ve used TiddlyWiki, the concept is similar: *the document is the application and the data*.

### What is saved
When you press **Save system**, Selfie serializes:
- VM objects (prototype objects, slots, method templates, blocks, etc.)
- method code in **two forms**:
  - **Source**
  - **Bytecode**
- open outliners (which objects are open)
- outliner geometry (x/y/width/height)
- which reference connector lines are visible
- evaluator source/bytecode contents

When you reopen the HTML (or drop a `.selfieImage` file), Selfie reconstructs the VM and restores the UI.

---

## Two modes: Image view and VM view

Selfie has two primary views:

### Image view
The familiar Self-style experience:
- floating, resizable outliner windows
- editable slot names/values
- block literals and activations
- reference connectors
- evaluators inside outliners

### VM view (embedded files)
A simple in-browser “file system” for Selfie’s embedded modules:
- each script/style corresponds to a `<script>` or `<style>` section embedded in the HTML
- you can edit these “files” inside the browser
- add/rename/delete/export files
- drop `.js`/`.css` files to overwrite matching embedded names
- view the generated HTML (the exact content that will be saved)

This makes Selfie behave like a tiny “live system” that can be edited and then saved back into a single page.

---

## Bytecode: text, not real bytes

Selfie uses a very small “bytecode” instruction set, but **the bytecodes are not actual binary bytes**.

They are:
- **textual instructions** (one per line),
- compiled into an internal instruction list,
- and **interpreted** by the VM.

This makes them readable, editable, and suitable for learning and debugging.

Example:

```text
pushSelf
send arg
pushSelf
send a
send * 1
returnTop
````

---

## Implementation basis

The object model and execution ideas are based on the article:

[https://github.com/pavel-krivanek/articles/tree/master/SelfObjectModel](https://github.com/pavel-krivanek/articles/tree/master/SelfObjectModel)

Selfie adapts these concepts into a compact JavaScript implementation and visual outliner UI.

---

## Important: Selfie is not Self

Selfie is intentionally small and educational. It differs from Self in many serious ways. A few examples:

* **No JIT, no optimizing compiler** — execution is interpreted and simple.
* **Bytecode format is textual** — designed for readability, not performance.
* **Different parser / language surface** — it’s a Self/Smalltalk-flavored toy language, not Self syntax.
* **Block semantics simplified** — closure/lexical behavior is modeled, but not fully equivalent to Self.
* **Primitives are explicit** — invoked via `primitiveSend` bytecode and implemented in JS; not the same primitive system as Self.
* **Object model is a teaching model** — many behaviors are simplified for clarity.

The goal is to provide a *workbench* to understand key ideas, not a faithful reproduction.

---

## Quick feature list

* Floating, focusable, resizable **object outliners**
* Slot types:

  * read-only data slots
  * read/write slots (`foo` and setter `foo:`)
  * method slots (method templates with source + bytecode)
  * parent slots (delegation)
  * indexed slots (array-like storage ignored by lookup)
* Block literals with inspectable instantiation and lexical parent
* Evaluators embedded in outliners (source ↔ bytecode)
* Reference connectors with endpoint circles and masking over focused outliner
* `.selfieImage` export/import of VM image state
* Single-file HTML saving (TiddlyWiki-style)

---

## Status / disclaimer

Selfie is an educational prototype. Expect rough edges and breaking changes.
If you need a production system, this is not it — but if you want a playground for object model ideas, it’s a good place to explore.

