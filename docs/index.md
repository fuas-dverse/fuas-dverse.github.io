
Documentation for 2024 Spring project. See [[Methods]].

This page documents the various Markdown markup instructions. Some will not be supported in Obsidian but will only show correctly when rendered with Mkdocs.

## Annotations

Provides a way to add annotations, give inline comments.

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!



- Mark
	- ==mark me==
	- ==smart=mark==
	- bla

## Chapter 2

! tilde strikethrough does not work yet
! choose

Foo~~bar~~!!!

Instead use it only for sub/superscript. Or rather, use caret extension.

H^2^O and ^^insert me^^

CH~3~CH~2~OH

Then use PyMdown critic for marking text ++added++, --removed--.

{--

* test remove
* test remove
* test remove
    * test remove
* test remove

--}

{++

* test add
* test add
* test add
    * test add
* test add

++}


<div style="width:95%; margin:auto;">
  <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>
  This work is licensed under a Creative Commons Attribution 4.0 ShareAlike License (including images & stylesheets).
</div>

