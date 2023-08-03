# Style rule

contains:
Selector: which all elements be affected
declarations: how element will be rendered (property: value)

# Referencnig external style

```
<link href="style.css" rel="stylesheet">

<style>
    @import url("/path/stylesheet.css");
</style>
```

# Selectors

- element type selector

```
p { }
```

- class based selector

```
.className { }
```

targets specific element type using class

```
// applies to only p elements that have class className

p.className {

}
```

- id based selector

```
#id { }
```

- grouped selector - applies rules to all specified selectors

```
h1, h2, #introuction, p {
    border: 1px solid red;
}
```

- descendant selector (not just child, could be any level deep)

```
// rule will apply h1 that appear in p in div

div p h1 {

}

// rule will apply to p inside element with id 'info'

#info p {

}

```

- descendant selector combined with grouped selector
  // rule will apply to both h1 and h2 inside p inside div

div p h1, div p h2 {
color: red
}

- child selector (immediate child only)

```
// p that are immediate child of div

div > p {

}
```

- Next sibling selector
  targets direct sibling

```
targets h2 that comes immediately after h1

h1 + h2 {

}
```

- sibling selector

```
any h2 that comes after h1 (same level)

h1 ~ h2 {

}
```

- attibute selector

```
[attributeName] {

}

element[attributeName] {

}
```

- universal selector
  applies to all elements where property is applicable

```
* {

}
```

- pseudo selector

anchor specific

```
a:link {} -- unclicked link
a:visited {} -- visited link
```

action on element

```
:hover - rules to apply on hover
:focus - rules to apply on focus
:active - rules to apply on active
```

Structural pseudo-classes
Allow selection based on where the element is in the structure of the document (the document tree):

```
:root
:empty
:first-child
:last-child
:only-child
:first-of-type
:last-of-type
:only-of-type
:nth-child()
:nth-last-child()
:nth-of-type()
:nth-last-of-type()
```

Input pseudo-classes
These selectors apply to states that are typical for form inputs:

```
:enabled
:disabled
:checked
```

# CSS cascading, specificity

- Cascading nature of CSS allows assigning multiple styles to html elements at different places and via different selectors. When multiple conflicting styles are applied on page, CSS determines which to apply based on the priority of style rule source, specificity of the selector and rule order.

- Which all rules are applied on an element based on selector and their specificity order can be seen from browser's developer tools.

- priority order - which source takes priority
  inline style > external style sheet > reader style sheet > user agent style sheet (browser)
  exception: !important is used

If conflicting properties are applied, using the same selector - last one wins.

```
--- style.css ---
p {color : red }
p {color : blue}

// blue will be applied
```

- Specificity order - How specific the selector is

```
inline style >
    #id selector
        > .class and ::pseudo class & [attributes] selector
            > element and ::pseudo-element selector, * selector
                > browser default style
                    > inherited styles from parent


```

- Various possbilities

1. If multiple rules apply to html element due to different selectors type - css rules are merged - conflicting rules are overriden based on specificity and source priorirty.

```
h1 {
  color: white;
  font-family: sans-serif;
}

.section-title {
  color: #2ddf5c;
}

<h1 class="section-title">This is sample<h1>

---
h1 will have following rules applied
color: #2ddf5c;
font-family: sans-serif;
```

2. If different rules are defined using same selectors type - last set of rules defined for given selector will only be applied. Any previous rules for the selector will be discarded.

```
h1 {
  color: white;
  font-family: sans-serif;
}

h1 {
  color: #2ddf5c;
}

<h1>This is sample</h1>

--- h1 will have following rules applied
color: #2ddf5c;     // font family does not get applied
```

3. If using combinators to define rules - combinators will take more preference over more general selectors.
   When applying multiple combinators that apply to same element using same base selector - more specific combinator takes precedence.

```
# product-overview h1 will be applied

#product-overview h1 {
  color: white;
  font-family: sans-serif;
}

h1 {
  font-family: "Courier New", Courier, monospace;
}
```

4. style rule marked !important takes precedence over all other styles.

```
p {color: blue !important;}

// the above rule will takes precendence over any color rule applied on p, even if it is declared inline
```

# Rules inheritance

Rules applied on parent elements applies on child elements.
Applies on only few rules ex: font-family etc. In general, properties related to the styling of text—font size, color, style, and the like are passed down.
If font-color style is applied on paragraph and it contains <em>, then rule will be applied on <em> as well.

Properties such as borders, margins, backgrounds, and so on that affect the boxed area around the element tend not to be passed down.

Inherited properties has lowest specificity. Inhertiance specifity can be increase by selecting value as inherit for given css rule.

```
h1 {
    font-family: inherit;
}
```

# box model

Every element in css is represented by block - block level as well as inline.

Block level element by default consumes entire parent container width while inline consumes width based on content size by default.

Each box has properties padding, border, margin. Margin.
Padding - gap between content and border.
border - outlines the border of the element.
margin - not direclty part of the element. Defines gap between element and other elements (could be sibllings, parent/child).

Each box also has background property. Box can be repositioned, width and height can be controlled.

# units of measurement

- Absolute
  px - pixel (1/96 inch) - most used till some time back. Very rigid and not goes well with fluid design.
  still very useful while defining border widths, and other fixed sizes.
  in - inches, mm - millimeters, cm - centimeters etc

- Relative
  Relative units are based on the size of something else

<strong>em</strong> : a unit of measurement equal to the current font size.
For font-size, this property for element is based on inherited font size.
For borders, margin it is determined from current element font size.
For 16px font-size, 1em is 16px. For 24px font-size, 1em is 24px.
Other rules may use em example: margin: 2em. Here, em will be determined based on text size.

<strong>ex</strong> : x-height, approximately the height of a lowercase “x” in the font.

<strong>rem</strong> : root em, equal to the font size (em) of the root element (html).
Default is 16px. So, 10rem by default means 160px.

<strong>ch</strong> : zero width, equal to the width of a zero (0) in the current font and size.

<strong>vw</strong> : viewport width unit, equal to 1/100 of the current viewport (browser window) width.
<strong>vh</strong> : viewport height unit, equal to 1/100 of the current viewport height.

vw and vh are used in making images, text width/heigth relative to window size.
Full window size { width: 100vw, heigh: 100 vw}

<strong>vmin</strong> : viewport minimum unit, equal to the value of vw or vh, whichever is smaller.

- Percentages:

1. Common measurement value for web page elements. Percentages are calculated relative to another value, such as the value of a property applied to the current element or its parent or ancestor. The spec always says what a percentage value for a property is calculated on.
2. When used for page layouts, percentage values ensure that page elements stay proportional.
3. Child elements do not inherit the relative values of their parent, but rather the resulting calculated value.

# height, width

heigth and width properties on any element in percentage takes surrounding element's height and width in account .

block level element by default takes 100% width. Can be reduced using width.
block level element by default takes only as much height as required.
Fro child block level element height is with respect to height made available by the parent container. This "made available" height is calculated dynamically based on what other elements are in the parent container and how much height do they need.
For ex: setting height: 100% for div inside body will not make div cover the entire page. As body will by default take only as much height as required.

inline level elements width and height is controlled by content.

height and widht by default are applied to content. So setting width as 100% will make padding and border on the right not visible.
To avoid this issue, height and width can be applied till border.
So, width = content width + padding + border

This can be done using:
box-sizing: border-box;

inheritance won't work while setting up box-sizing: border-box as block element by default use box-sizing: content-box.
To still apply it on all elements, use universal selector.

# CSS wide keywords

All properties expect CSS wide keywords

- initial: explicitly set the property to initial (default) value.
- inherit: explicitly force element to inherit property from the parent. inherited properties have least priorirty and this helps apply it forcefully.
- unset: erases any declared values. Make property accepts either initial or inherit value.

# Font properties

1. Font-family
   allows setting which font type to use.
   Values: one or more font or generic font family names, separated by commas
   Default: depends on the browser
   Applies to: all elements
   Inherits: yes

```
p { font-family: "Duru Sans", Verdana, sans-serif; }

This will apply "Duru Sans", if browser does not support it, will apply Verdana, if browser does not support it, will apply font from sans-serif family.
```

sans-serif is one of the five generic font families available. when specifying font familty browser selects font from that category.
sans-serif:Verdana, Trebuchet MS, Arial, Arial Blck
serif
monospace
cursive
fantasy

- Font family strategy
  Start with specific font, then give more common, then generic font family.

2. Font-size

sllows setting size
Values: length unit | percentage | xx-small | x-small | small | medium | large |
x-large | xx-large | smaller | larger
Default: medium
Applies to: all elements
Inherits: yes

```
// 1.5 times the default font size
h1 {
    font-size: 1.5em;
}
```

Preferred way to set the font size is using relative units (em, rem) and percentage.

best practice: rem provides one common points to use for font-size.

```
// html will be set to default size generally 16px, but can be different
html {
   font-size: 100%;
}

// h1 will relatively stand out, this will make default size 24px
h1 {
    font-size: 1.5rem;
}
```

Em units are based on the font size of the current element. When you specify font-size in ems, it will be relative to the inherited size for that element.

3. font-weight

font boldness.
Values: normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800
| 900
Default: normal
Applies to: all elements
Inherits: yes

4. font-style

Values: normal | italic | oblique
Default: normal
Applies to: all elements
Inherits: yes

5. font-stretch

Values: normal | ultra-condensed | extra-condensed | condensed | semi-condensed | semi-expanded | expanded | extra-expanded | ultra-expanded
Default: normal
Applies to: all elements
Inherits: yes

6. font (shorthand property)

Values: font-style font-weight font-variant font-stretch font-size/line-height
font-family | caption | icon | menu | message-box | small-caption | status-bar
Default: depends on default value for each property listed
Applies to: all elements
Inherits: yes

```
// line-height defines hap between lines

h3 { font: oblique bold small-caps 1.5em/1.8em Verdana, sans-serif; }
h2 { font: bold 1.75em/2 sans-serif; }
```

7. color

Values: color value (name or numeric)
Default: depends on the browser and user’s preferences
Applies to: all elements
Inherits: yes

8. line-height
   gap between lines

Values: number | length measurement | percentage | normal
Default: normal
Applies to: all elements
Inherits: yes

9. text-align

Values: left | right | center | justify | start | end
Default: start
Applies to: block containers
Inherits: yes

10. text-decoration

Values: none | underline | overline | line-through | blink
Default: none
Applies to: all elements
Inherits: no, but since lines are drawn across child elements, they may look like
they are “decorated” too

11. text-transform

Values: none | capitalize | lowercase | uppercase | full-width
Default: none
Applies to: all elements
Inherits: yes

12. other properties
    word-break: Specifies whether to break lines within words
    word-spacing: Inserts space between words
    word-wrap: Indicates whether the browser can break lines within words to prevent overflow (same as overflow-wrap)

# colors

1. color
   sets foreground color

2. background-color
   sets background color

3. opacity
   adds transparency

# Background properties

1. background-color
2. background-image

Values: url(location of image) | none
Default: none
Applies to: all elements
Inherits: no

3. background-repeat
   background image by default starts tiling (repating) horizontally and vertically. To control this

Values: repeat | no-repeat | repeat-x | repeat-y | space | round
Default: repeat
Applies to: all elements
Inherits: no

4. background-position
   set position of background image. If no-repeat is not set, image will tile based on the position.

Values: length measurement | percentage | left | center | right | top | bottom
Default: 0% 0% (same as left top)
Applies to: all elements
Inherits: no

5. background-attachment
   controls if the background image should scroll or remain fixed when content is scrolled

Values: scroll | fixed | local
Default: scroll
Applies to: all elements
Inherits: no

6. background-clip
   default background color/image extends till border. background-clip provides option to restrict it.

background-clip
Values: border-box | padding-box | content-box
Default: border-box
Applies to: all elements
Inherits: no

7. background-size
   provide size for the image instead of using default

Values: length | percentage | auto | cover | contain
Default: auto
Applies to: all elements
Inherits: no 8. background

8. background

Values: background-color background-image background-repeat background-attachment background-position background-clip background-origin background-size
Default: see individual properties
Applies to: all elements
Inherits: no

# gradients

A gradient is a transition from one color to another, sometimes through multiple colors.

1. Linear gradient

```
background-image: linear-gradient(180deg, aqua, green);
```

2. Radial gradient
   Radial gradients, like the name says, radiate out from a point in a circle along
   a gradient ray

```
background-image: radial-gradient(yellow, green);
```

# The box model

Each box has:

1. content area
2. padding area
3. border
4. margin area (always transparent)

Space required by any element = content area + padding area + border + margin area

# box dimensions

1. width
2. height

width and height are applicable to block elements and replaced inline elements (images). By default do not apply to text inline elements.
However, display: block can be set on inline elements, post which height, width can be applied.

To fix the max height and width, following can be used
max-height, max-width,
min-height, min-width

3. box-sizing
   Values: content-box | border-box
   Default: content-box
   Applies to: all elements
   Inherits: no

By default - content-box model is followed. i.e. given width is just for content.
padding, border and margin is not counted.

```
p {
  background: #f2f5d5;
  width: 500px;
  height: 150px;
  padding: 20px;
  border: 5px solid gray;
  margin: 20px;
}

With content-box

Visible element box (includes width + padding + border)
5px + 20px + 500px width + 20px + 5px = 550 pixel

Element box (includes width + padding + border + margin)
20px + 5px + 20px + 500px width + 20px + 5px + 20px = 590 pixels

However, with border-box
visible element box = 500 px (includes width + padding + border), browser auto adjusts

element box = 540 px (includes width + padding + border + margin)

```

4. overflow
   If element is too small for it's contents

Values: visible | hidden | scroll | auto
Default: visible
Applies to: block-level elements and replaced inline elements (such as images)
Inherits: no

5. padding
6. border
7. margin

Margin behavior:

- collapsing margins:
  The most significant margin behavior to be aware of is that the top and bottom margins of neighboring elements collapse. This means that instead of accumulating, adjacent margins overlap, and only the largest value is used.

8. display

The display property defines the type of element box an element generates in the layout.
Type of element box - inline, block etc

This does not change html semantic i.e. if block property is applied on an inline element, that inline element cannot contain block element.

display: none; removes the content entirely.

9. box-shadow

   Values: ‘horizontal offset’ ‘vertical offset’ ‘blur distance’ ‘spread distance’ color
   inset | none
   Default: none
   Applies to: all elements
   Inherits: no
