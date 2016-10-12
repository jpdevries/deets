# deets

HTML5 tree component that works entirely without JavaScript and web&nbsp;fonts.

[Try it out](http://jpdevries.github.io/deets).

![](http://j4p.us/1V3M3k2y0D1U/deets.gif)

## Usage
[HTML5 Rocks](https://www.html5rocks.com). That's how this asynchronous component is architected with pure HTML5 and a sprinkle of&nbsp;CSS3.

### Pattern
You'll need to wrap everything in a `<details>` tag so create one of those:
```html
<details>
</details>
```

Next create a summary. Summaries define the persisting area of each element in the&nbsp;tree.
```html
<details>
  <summary>
    <a href="#">
      Blog
    </a>
  </summary>
  <!-- stuff to show when expanded goes here -->
</details>
```

And the add the stuff to display when the element is expanded! This can be any HTML so by nesting `<details>` you can create a familiar tree component that allows each item to act as a&nbsp;container.

```html
<details>
  <summary>
    <a href="#">
      Blog
    </a>
  </summary>
  <details>
    <summary>
      <a href="#">
        MODX
      </a>
    </summary>
    <ul>
      <li><a href="#">RTFM</a></li>
      <li><a href="#">Forums</a></li>
      <li><a href="#">MAB</a></li>
      <li><a href="#">MODX Cloud</a></li>
    </ul>
  </details>
  <details>
    <summary>
      <a href="#">
        HTML5
      </a>
    </summary>
    <ul>
      <li><a href="#">caniuse</a></li>
      <li><a href="#">W3C</a></li>
    </ul>
  </details>
</details>
```

[Visit this&nbsp;example](http://jpdevries.github.io/deets).

### icons
There are a few patterns to add&nbsp;icons.

#### SVG Use
Our [icon example](https://jpdevries.github.io/deets/icons.html) uses a SVG `<use>`&nbsp;pattern.
##### HTML
```html
<summary>
  <a href="#">
    <svg role="img" class="folder icon">
      <use xlink:href="assets/img/icons.svg#icon-folder"></use>
    </svg>
    <svg hidden role="img" class="folder-open icon">
      <use xlink:href="assets/img/icons.svg#icon-folder-open"></use>
    </svg>
    MODX
  </a>
</summary>
```

##### CSS
```css
details[open] > summary > a .folder {
  display:none; /* hide the folder icon when open */
}

details[open] > summary > a .folder-open {
  display:inline-block; /* show the folder-open icon when open */
}
```

##### Pros
 - Any number of SVG icons can be contained in a sprite file or inlined in the&nbsp;HTML
 - Accessible and semantic delivery of icons
 - Dynamic color with `color:currentColor`
 - Can [color an icon with CSS&nbsp;Properties](https://codepen.io/jpdevries/pen/MKbrrX)

##### Cons
 - Markup weight

##### Costs
  - an HTTP request

#### CSS Pseudo
Our [CSS Pseudo example](https://jpdevries.github.io/deets/icons-pseudo.html) is CSS only and therefore the icons aren't delivered semantically or accessible. But depending on your situation they may not need to be. For example, a screen reader user may not need to be informed there's an icon that indicates a folder is open if their assistive technology had already indicated&nbsp;that.

The CSS pattern requires no&nbsp;markup.

##### CSS
```css
summary > a:before {
  content:' ';
  position:absolute;
  left:0;
  bottom:0;
  width:1em;
  top:0;
  display:block;
  background:transparent url('assets/img/folder.svg') no-repeat center center;
  background-size:contain;
}

details[open] > summary > a:before {
  background:transparent url('assets/img/folder-open.svg') no-repeat center center;
}
```

##### Pros
 - Light HTML
 - Style where style goes

##### Cons
 - Unsemantic icons
 - Can't change icon color(s) with CSS

##### Costs
- Multiple HTTP requests

 _These may not be cons or costly if you are serving over HTTP/2 and icons don't need to be semantic or&nbsp;accessible_

### `no-marker`
If this attribute is present on the `<details>` node or any parent node the triangular marker which indicates if summaries are expanded or closed will not be&nbsp;displayed.
