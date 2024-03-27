#game_development 

[The original documentation](https://mermaid.js.org/syntax/flowchart.html)


# Flowcharts

Flowcharts are composed of 
- **nodes** (geometric shapes) and 
- **edges** (arrows or lines). 

The Mermaid code defines how **nodes** and **edges** are made and accommodates different arrow types, multi-directional arrows, and any linking to and from subgraphs.

> If you are using the word "end" in a Flowchart node, capitalize the entire word or any of the letters (e.g., "End" or "END"), or apply this [workaround](https://github.com/mermaid-js/mermaid/issues/1444#issuecomment-639528897). Typing "end" in all lowercase letters will break the Flowchart.

## Node
This is the default:

```mermaid
flowchart LR
    id
```
---
## Node w/ text


```mermaid
flowchart LR
    id1[This is the text in the box]
```

---
## Node w/ unicode

Use `"` to enclose unicode text
```mermaid
flowchart LR
    id["This ❤ Unicode"]
```
---
## Node w/ .md formating
Use double quotes and back-ticks to enclose the markdown text.
```mermaid
%%{init: {"flowchart": {"htmlLabels": false}} }%%
flowchart LR
    markdown["`This **is** _Markdown_`"]
    newLines["`Line1
    Line 2
    Line 3`"]
    markdown --- newLines
```

---
# Direction

## TD (Top Down)
or **TB** (Top Bottom)
```mermaid
flowchart TD
    Start --> Stop
```
---
## LR (Left --> Right)

```mermaid
flowchart LR
    Start --> Stop
```
---
## RL (Right --> Left)
```mermaid
flowchart RL
    Start --> Stop
```
---
## BT (Bottom --> Top)
```mermaid
flowchart BT
    Start --> Stop
```

---

# Shape

## Round Edges

> $(\text{Wrap your text in parentheses})$

```mermaid
flowchart LR
    id1(This is the text in the box)
```

---

## Oval Shape

> $([\text{Wrap your text in brackets, and then parentheses}])$


```mermaid
flowchart LR
    id1([This is the text in the box])
```

---

## Subroutine Shape

This barely shows up on my machine so just don't use this one

> $\text{[[Wrap your text in double-brackets]]}$

```mermaid
flowchart LR
    id1[[This is the text in the box]]
```

---

## Cylinder Shape 

> $[(\text{Wrap your text in parentheses, and then brackets})]$
```mermaid
flowchart LR
    id1[(Database)]
```

---
## Circle Shape

> $((\text{Wrap your text in double-parentheses}))$

```mermaid
flowchart LR
    id1((This is the text in the circle))
```

---

## Asymmetric Shape

> $>\text{This is the text in the box}]$

```mermaid
flowchart LR
    id1>This is the text in the box]
```

`NOTE: only the shape above is possible and not its mirror.`

---

## Diamond Shape

> $\{ \text{Wrap with Brackets} \}$

```mermaid
flowchart LR
    id1{This is the text in the box}
```

---

## Hexagon Shape

```mermaid
flowchart LR
    id1{{This is the text in the box}}
```

---

## Parallelogram

```mermaid
flowchart TD
    id1[/This is the text in the box/]
```

---
### Parallelogram alt

```mermaid
flowchart TD
    id1[\This is the text in the box\]
```

This is the text in the box

---

## Trapezoid

```mermaid
flowchart TD
    A[/Christmas\]
```

---

### Trapezoid alt

```mermaid
flowchart TD
    B[\Go shopping/]
```
---
### Double circle
```mermaid
flowchart TD
    id1(((This is the text in the circle)))
```

---

