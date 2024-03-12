Which Markdown features are supported on this site. Most of these features should also work in [[Obsidian]].

Use the view source link to see how it looks as raw Markdown text.

## Notes and admonitions

> [!note] A Note
> Note text.

Code:

```
> [!note] A Note
> Note text.
```

Instead of `!note` you can also use `!abstract`, `!info`, `!tip`, `!success`, `!question`, `!warning`, `!failure`, `!danger`, `!bug`, `!example`, `!quote` to get a specific color and icon text box (admonition). Other words can be used to (like `!obsidian` below) but they will get a standard rendering color/icon. It's better to use a standard keyword and add the title after the keyword (like above with "A Note").

> [!bug] Bug alert
> This didn't go as expected.

You can also still use the plain quoted text block.

> this is a plain
> quoted block

Code:

```
> this is a plain
> quoted block
```

Note that these blocks can be nested (but admonitions like the ones above cannot be used nested inside a quoted block).

> Hello
> > Bla
> > Bla
> Goodby

> [!tip]
> Nesting
> > this works

## Lists

### Regular lists

Markdown always supports standard, nested, bulleted and numbered lists.

Unordered (bullets).

- Item
- Item
- Item

Ordered (numbered).

1. Item
2. Item

Mixed and nested.

- Item
	- Subitem
- Item
	1. Item
		1. Subitem
		2. Subitem
	2. Item

But we also support a couple of more advanced list types.

### Definition lists

**Term 1**

:   Term 1 definition.

**Term 2**

:   Term 2 definition.

    Another indented paragraph.

> [!note] Obsidian
> Will not show definition lists correctly and to get multiple paragraphs only the first paragraph will show in regular font.

### Task lists

-   [X] Item 1
    *   [X] Item A
    *   [ ] Item B
        More text
        +   [x] Item a
        +   [ ] Item b
        +   [x] Item c
    *   [X] Item C
-   [ ] Item 2
-   [ ] Item 3

> [!note] Obsidian
> The items can be toggled, which is then reflected in the Markdown.


## Code

Inline and block code highlighting.

```clojure
(cond (= 4) (+ 2 2))
```

```yaml
foo: 10
bar:
  - ABC
  - DEF
```

Adding a title

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

Line numbers

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

Highlight specific lines.

``` py hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

The `#!python range()` function is used to generate a sequence of numbers.

Code block with annotations.

``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.

> [!note] Obsidian
> Some attributes for the highlight blocks are not shown in Obsidian. You have to put the cursor in the code block to see the attributes.

## Footnotes

This text has a footnote[^foobar]!

[^foobar]: And this is the text for the footnote.

When publishing the notes will be collected and put at the end of the document (end notes).

## Math

For inline math start a span of math text with `$` and end with `$`. To get a block of math text start a block section with `$$` and end it with `$$` each marker starting in column 1 and on a line by itself.

This is $p(x|y) = \frac{p(y|x)p(x)}{p(y)}, (p(x|y) = \frac{p(y|x)p(x)}{p(y)})$ inline math.


This is a block of math.

$$
\begin{align}
    p(v_i=1|\mathbf{h}) & = \sigma\left(\sum_j w_{ij}h_j + b_i\right) \\
    p(h_j=1|\mathbf{v}) & = \sigma\left(\sum_i w_{ij}v_i + c_j\right)
\end{align}
$$

## Diagrams

To insert diagrams we use [Mermaid](https://mermaid.js.org) support. Here are some examples but consult the [Mermaid documentation](https://mermaid.js.org/intro) for more information. To see the raw Markdown text click the source view button (top right).

### Flowchart

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

### Sequence diagram

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

### Class Diagram

``` mermaid
---
title: Animal example
---
classDiagram
    note "From Duck till Zebra"
    Animal <|-- Duck
    note for Duck "can fly\ncan swim\ncan dive\ncan help in debugging"
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal: +isMammal()
    Animal: +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
```

### State Diagram

``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```

### Entity Relationship Diagram

``` mermaid
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```
### User Journey

``` mermaid
journey
    title My working day
    section Go to work
      Make tea: 5: Me
      Go upstairs: 3: Me
      Do work: 1: Me, Cat
    section Go home
      Go downstairs: 5: Me
      Sit down: 5: Me
```

### Gantt Chart

``` mermaid
gantt
    title A Gantt Diagram
    dateFormat YYYY-MM-DD
    section Section
        A task          :a1, 2014-01-01, 30d
        Another task    :after a1, 20d
    section Another
        Task in Another :2014-01-12, 12d
        another task    :24d
```

### Pie Chart

``` mermaid
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```
### Quadrant Chart

``` mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
    Campaign C: [0.57, 0.69]
    Campaign D: [0.78, 0.34]
    Campaign E: [0.40, 0.34]
    Campaign F: [0.35, 0.78]
```

### Gitgraph Diagram

``` mermaid
---
title: Example Git diagram
---
gitGraph
   commit
   commit
   branch develop
   checkout develop
   commit
   commit
   checkout main
   merge develop
   commit
   commit
```

### C4 Diagram

``` mermaid
    C4Context
      title System Context diagram for Internet Banking System
      Enterprise_Boundary(b0, "BankBoundary0") {
        Person(customerA, "Banking Customer A", "A customer of the bank, with personal bank accounts.")
        Person(customerB, "Banking Customer B")
        Person_Ext(customerC, "Banking Customer C", "desc")

        Person(customerD, "Banking Customer D", "A customer of the bank, <br/> with personal bank accounts.")

        System(SystemAA, "Internet Banking System", "Allows customers to view information about their bank accounts, and make payments.")

        Enterprise_Boundary(b1, "BankBoundary") {

          SystemDb_Ext(SystemE, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc.")

          System_Boundary(b2, "BankBoundary2") {
            System(SystemA, "Banking System A")
            System(SystemB, "Banking System B", "A system of the bank, with personal bank accounts. next line.")
          }

          System_Ext(SystemC, "E-mail system", "The internal Microsoft Exchange e-mail system.")
          SystemDb(SystemD, "Banking System D Database", "A system of the bank, with personal bank accounts.")

          Boundary(b3, "BankBoundary3", "boundary") {
            SystemQueue(SystemF, "Banking System F Queue", "A system of the bank.")
            SystemQueue_Ext(SystemG, "Banking System G Queue", "A system of the bank, with personal bank accounts.")
          }
        }
      }

      BiRel(customerA, SystemAA, "Uses")
      BiRel(SystemAA, SystemE, "Uses")
      Rel(SystemAA, SystemC, "Sends e-mails", "SMTP")
      Rel(SystemC, customerA, "Sends e-mails to")

      UpdateElementStyle(customerA, $fontColor="red", $bgColor="grey", $borderColor="red")
      UpdateRelStyle(customerA, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
      UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
      UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
      UpdateRelStyle(SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")

      UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```

### Mindmaps

``` mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

### Timeline

``` mermaid
timeline
    title History of Social Media Platform
    2002 : LinkedIn
    2004 : Facebook
         : Google
    2005 : Youtube
    2006 : Twitter
```
### Sankey Diagram

``` mermaid
---
config:
  sankey:
    showValues: false
---
sankey-beta

Agricultural 'waste',Bio-conversion,124.729
Bio-conversion,Liquid,0.597
Bio-conversion,Losses,26.862
Bio-conversion,Solid,280.322
Bio-conversion,Gas,81.144
Biofuel imports,Liquid,35
Biomass imports,Solid,35
Coal imports,Coal,11.606
Coal reserves,Coal,63.965
Coal,Solid,75.571
District heating,Industry,10.639
District heating,Heating and cooling - commercial,22.505
District heating,Heating and cooling - homes,46.184
Electricity grid,Over generation / exports,104.453
Electricity grid,Heating and cooling - homes,113.726
Electricity grid,H2 conversion,27.14
Electricity grid,Industry,342.165
Electricity grid,Road transport,37.797
Electricity grid,Agriculture,4.412
Electricity grid,Heating and cooling - commercial,40.858
Electricity grid,Losses,56.691
Electricity grid,Rail transport,7.863
Electricity grid,Lighting & appliances - commercial,90.008
Electricity grid,Lighting & appliances - homes,93.494
Gas imports,Ngas,40.719
Gas reserves,Ngas,82.233
Gas,Heating and cooling - commercial,0.129
Gas,Losses,1.401
Gas,Thermal generation,151.891
Gas,Agriculture,2.096
Gas,Industry,48.58
Geothermal,Electricity grid,7.013
H2 conversion,H2,20.897
H2 conversion,Losses,6.242
H2,Road transport,20.897
Hydro,Electricity grid,6.995
Liquid,Industry,121.066
Liquid,International shipping,128.69
Liquid,Road transport,135.835
Liquid,Domestic aviation,14.458
Liquid,International aviation,206.267
Liquid,Agriculture,3.64
Liquid,National navigation,33.218
Liquid,Rail transport,4.413
Marine algae,Bio-conversion,4.375
Ngas,Gas,122.952
Nuclear,Thermal generation,839.978
Oil imports,Oil,504.287
Oil reserves,Oil,107.703
Oil,Liquid,611.99
Other waste,Solid,56.587
Other waste,Bio-conversion,77.81
Pumped heat,Heating and cooling - homes,193.026
Pumped heat,Heating and cooling - commercial,70.672
Solar PV,Electricity grid,59.901
Solar Thermal,Heating and cooling - homes,19.263
Solar,Solar Thermal,19.263
Solar,Solar PV,59.901
Solid,Agriculture,0.882
Solid,Thermal generation,400.12
Solid,Industry,46.477
Thermal generation,Electricity grid,525.531
Thermal generation,Losses,787.129
Thermal generation,District heating,79.329
Tidal,Electricity grid,9.452
UK land based bioenergy,Bio-conversion,182.01
Wave,Electricity grid,19.013
Wind,Electricity grid,289.366
```

### XYChart

``` mermaid
xychart-beta
    title "Sales Revenue"
    x-axis [jan, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec]
    y-axis "Revenue (in $)" 4000 --> 11000
    bar [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]
    line [5000, 6000, 7500, 8200, 9500, 10500, 11000, 10200, 9200, 8500, 7000, 6000]
```

## Tables

Align left

| Method   | Description                          |
| -------- | ------------------------------------ |
| `GET`    | :material-check:     Fetch resource  |
| `PUT`    | :material-check-all: Update resource |
| `DELETE` | :material-close:     Delete resource |

Align center

| Method      | Description                          |
| :---------: | :----------------------------------: |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |
Align right

| Method      | Description                          |
| ----------: | -----------------------------------: |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |

> [!todo] TODO
> External files, Sortable columns


## Images


![image](placeholder-image.png)

Code:

```
![image](placeholder-image.png)
```

Like with hyperlinks we can also include images using wiki-style links.


![[activity-pub-mechanics.png]]

## Inline markup

This is **bold**, *italic*, and ***bolditalic***. Code `foo=10`. Keys: ++ctrl+alt+del++, ++a++.

Code:

```
This is **bold**, *italic*, and ***bolditalic***. 
Code `foo=10`. 
Keys: ++esc++, ++a++.
```

Super- and Subscript can be added using HTML tags or with special syntax (more convenient).

- H~2~O  (`H~2~O`)
- A^T^A (`A^T^A`)

## Highlighting text

- {==This was marked==}
- ~~This was deleted~~

{==This whole paragraph will be highlighted.==}

## Buttons

Not sure how useful this is, but we support simple buttons.

[Subscribe](#){ .md-button }

Code:

```
[Subscribe](#){ .md-button }
```
## Links

Inline hyperlink.

Code:

```
[Fontys](https://www.fontys.nl)
```

[Fontys](https://www.fontys.nl)

Code:

```
[Fontys](https://www.fontys.nl){:target="_blank"}
```

[Fontys](https://www.fontys.nl){:target="_blank"}


Explicit hyperlink to other document.

Code:

```
[Methods](Methods.md)
```

[Methods](Methods.md)

Wiki-links

Code:

```
[[xxxx]]
```

[[Methods]]


> [!note] Obsidian
> In Obsidian we prefer so called Wiki-links. These are easier to type and they are also supported.

## Content Tabs

> [!warning] Obsidian
> These are not displayed correctly by Obsidian but they seemed so useful that we did not want to exclude them.

The idea is to start every tab with `===`, when published this will become a panel where each section is shown as a separate tab.

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

## HTML

HTML embedding is allowed but should be used sparingly. We may, one day, turn it off without notice.


