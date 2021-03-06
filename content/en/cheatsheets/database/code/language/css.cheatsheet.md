---
title: css.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Box Model
#-#

┌───────────────────────────────────────────┐
│                                           │
│   ┌───────────────────────────────────┐   │
│   │                                   │   │
│   │   ┌───────────────────────────┐   │   │
│   │   │                 padding ──┼───┼───┼── Clears an area around the content.
│   │   │   ┌───────────────────┐   │   │   │   The padding is transparent.
│   │   │   │                   │   │   │   │
│   │   │   │      content  ────┼───┼───┼───┼── The content of the box,
│   │   │   │                   │   │   │   │   where text and images appear. 
│   │   │   └───────────────────┘   │   │   │
│   │   │                           │   │   │
│   │   └───────────────────────────┘   │   │
│   │                          border ──┼───┼── A border that goes around
│   └───────────────────────────────────┘   │   the padding and content.
│   margin                                  │
└─────┼─────────────────────────────────────┘
      └─ Clears an area outside the border.
         The margin is transparent.



#-#
#-# Selectors
#-#

#-# Selector types

Selector              Type                Description
--------              ----           	  ----------
*                     Universal           Any element.
element               Type                Any element of that type.
element, element      Grouping            Multiple elements of different types.
.class                Class               Multiple elements of different sharing the same class.
#id                   Id                  A single element identified by its id.
element element       Descendant          An element that is below another element, no matter how many levels below.
element > element     Child               An element that is directly below another element.
element + element     Adjacent sibling    All elements placed immediately after the specified parent elements.
element ~ element     General sibling     All elements that share the same parent and elements are in the same sequence (not necessarily immediate).
[attribute]           Attribute           All elements with the specified attribute.


#-# Attributes

Attribute             Description
---------             -----------
[attribute]           All elements with the specified attribute.
[attribute=value]     All elements where the specified attribute is equal to 'value'.
[attribute~=value]    All elements with an attribute containing the word 'value'.
[attribute|=value]    All elements with an attribute list starting with 'value'.
[attribute^=value]    All elements with an attribute beginning with 'value'.
[attribute$=value]    All elements with an attribute ending with 'value'.
[attribute*=value]    All elements with an attribute containing the substring 'value'.


#-# Pseudo-classes

Pseudo-class          Description
------------          -----------
:active               An activated element.
:focus                An element while the element has focus.
:visited              A visited link.
:hover                An element when you mouse over it.
:link                 An unvisited link.
:disabled             An element while the element is disabled.
:enabled              An element while the element is enabled.
:checked              An element (form element control) that is checked.
:selection            An element that is currently selected of highlighted by the user.
:lang                 Allows the author to specify a language to use in a specified element.
:nth-child(n)         An element that is the n-th sibling.
:nth-last-child(n)    An element that is the n-th sibling counting from the last sibling.
:first-child          An element that is the first sibling.
:last-child           An element that is the last sibling.
:only-child           An element that is the only child.
:nth-of-type(n)       An element that is the n-th sibling of its type. 
:nth-last-of-type(n)  An element that is the n-th sibling of its type counting from the last sibling.
:last-of-type         An element that is the first sibling of its type.
:first-of-type        An element that is the last sibling of its type.
:only-of-type         An element that is the only child of that type.
:empty                An element that has no children.
:root                 Root element within the document.
:not(x)               An element not represented by the argument 'x'.
:target               A target element as specified by a target in a URI.


#-# Pseudo-elements

Pseudo-element       Description
--------------       -----------
::first-letter       Adds special style to the first letter of a text.
::first-line         Adds special style to the first line of a text.
::before             Inserts some content before an element. 
::after              Inserts some content after an element.



