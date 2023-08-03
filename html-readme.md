# HTML

Purpose of HTML is to add structure to the content. Not presentation. ---> Semantic markup.
Choose elements based on what makes sense for the content.

This overall structure is DOM (Dcoument object model).

# Block and inline elements

Block elements start with new line. Browser represent them as thye are in a box. By default, they occupy entire page width. Browser also has some space before and after them.
ex: div, p

inline elements do not start new line.
ex: em, b

# User agent style sheet

All browsers have default style sheet. This is used to determine how h1, h2, em etc will appear.

# Validators

HTML might not break but it may not be semantically valid. Validators allow to check HTML validity.

# Paragraphs

Block element.
May contain images, text and inline elements.
Should not contain h1, list, section and other block level elements. (Browser allows it but not valid HTML.)

# Headings h1 -- h6

Block element.
For assistive readers, create document outline.
Search engines also look at heading as part of algorigthms.

# Horizontal rule <hr/>

# Lists

Block element (Lists as well as list items)
With CSS, the block behaivor can be altered.

1. Unordered list <ul> <li>
2. Ordered list <ol> <li>
3. Description list <dl> <dt> (term) <dd> (description)

# Ogranizing page content

Block elements.
Prior to HTML 5, div was used to group and organize page content. (p, img, li etc)
With HTML 5, new block elements were introduced with meaningful name for struture:

May not work with old browser, css rule can be added to make display block.

- Main content - <main>
  To show main content. Ideally does not include navigation, sidebars etc.
- Header <header>
  To show heading or introductory material for page, <article>, <section>
- Footer <footer>
  Information at end of the page - contact, authors etc
- Sections <section>
  Page can be divided into smaller parts using section. Each section may have it's header.
- Article <article>
  An article can be divided into smaller sections. Article vs section - Article is standalone and can appear on separate site.
- aside <aside>
  Information related to the main content such as quotes, side bars, list of links (references) etc
- nav <nav>
  Site navigation content. Generally contains unordered list.
- address <address>
  Provide address information

Above all elements give more semantic context to the page (before HTML 5 div was used for all these). Presentation is part of CSS. These elements may have some browser default rules (user agent style sheet).

# Text level semantics (inline elements)

All text level semantics like <em>, <strong>, <a> etc are inline elements.
HTML 5 supports <b>, <i>, <s>, <u>. If they have importance from semantic perspective, it's adivsable to use them. But if it is just for styling, css is better alternative. For ex: for bold text - font-weight: bold can be used. for underline <u>, text-decoration: underline can be used.

- abbreviations <abbr>
- code <code>
- datetime <time>
- subscript/ superscript <sub>, <sup>
- highlight <mark>
- breakline <br/>

# Generic elements <div> and <span>

HTML offers two generic elements to deal with scenarios which do not fit with semantically available elements.

- div
  Generic block level element. Allows creating logical group.

- span
  Generic inline element. Can contain only other inline level elements.

With both <div> and <span>, id and class attributes are often used. id allows uniquely identifying the element while class allows classifying elements into groups.

# anchor tag <a>

Allows creating link. Content between anchor tag takes to the link.

```
<a href="about.html">About</a>
<a href="https://googlemaps.com"><img src="map.png"></a>
```

- Linking to fragments
  Any id created in page, can be navigated to by using absolute or relative path in href and providing #id after that.

```
navigate to element with contacts id on about.html page
<a href="about.html#contacts">Contacts</a>

naviagte to elements with references id on the same page
<a href="#refences">References</a>
```

- opening new window and mail links (if default mail program is configured in browser, clicking link will open mail program with to set)

```
<a href="about.html#contacts" target="_blank">Contacts</a>

<a href="mailto:test@test.com"">Contact us</a>
```

# tables

block level element.
If the data needs to be represented semantically in form of rows and columns, then tables should be used.
For presentation perspective if table and rows are required (ex: news headline and summary), CSS offers various ways - nested divs with proper CSS, grid, flex.

- <table>
- <tr> - row
- <th> - header in row (not just about style - holds semantic meaning)
- <td> - data

Spanning cells

- colspan - span multiple columns into one
- rowspan - span multiple rows into one

grouping rows

- <thead> - group headers
- <tbody> - group data
- <tfoot> - columns summary, foot note

grouping columns

- <colgroup> - gives browser details about table semantics that how many columns are grouped. Does not contain any data.

# images

If images are part of the content - it makes sense to include it with img tag.
If images are just for presentation purpose ex: background image in header, body etc css should be used.

# forms

# Embedded content
