# Easy LMS SCSS Styleguide
> For writing well structured stylesheets.

Loosely based on the [Airbnb CSS / Sass Styleguide](https://github.com/airbnb/css)

## Table of Contents

  - [CSS](#css)
    - [Rule declaration](#rule-declaration)
    - [Selectors](#selectors)
        - [ID selectors](#id-selectors)
        - [Body classes](#body-classes)
    - [Properties](#properties)
    - [Formatting](#formatting)
  	- [Border](#border)
  	- [Z-index](#z-index)
    - [Comments](#comments)
    - [OOCSS and BEM](#oocss-and-bem)
  - [SCSS](#scss)
	- [General](#general)
	- [Vendor prefixes](#vendor-prefixes)
    - [Ordering](#ordering-of-property-declarations)
    - [Variables](#variables)
    - [If/else](#ifelse)
    - [Mixins](#mixins)
    - [Extend directive](#extend-directive)
    - [Nested selectors](#nested-selectors)
  - [JavaScript hooks](#javascript-hooks)

## CSS

### Rule declaration
A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties.

* Put blank lines between rule declarations.
* Single line declarations are not allowed
```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}

.item {
  font-size: 12px;
  line-height: inherit;
}
```

### Selectors
In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties.
Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:
* Use kebab-case (dashes) for class names, no camelCasing or other naming conventions. Underscores (double) are okay when using BEM (see [BEM](#bem) below).
* Do not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Avoid qualifying elements in selectors e.g. no `ul.list` but just `.list`.

```css
/* bad */
.my-element-class, .another-element, .dontCamelCase {
  /* ... */
}

/* good */
[aria-hidden],
.hidden-element {
  /* ... */
}
```

#### ID selectors
Again **DON'T USE ID SELECTORS!** for styling purposes. You and only you will be held responsible for doing it anyway.

#### Body classes
Use of body classes should be prevented if at all possible. When using a body class is inevitable, apply it like a modifier (see [BEM](#bem) below) e.g.
```css
.page--pagetype {
  /* ... */
}
```

### Properties
Properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

* In properties, put a space after, but not before, the `:` character.
* Never use color names e.g. yellow. These are for kids, so use 6 number hex values instead.
* Remove trailing zeros for numeric values with a decimal point.
* Add spaces after commas.
* Values should be written in lowercase.
* Properties should be sorted alphabetically.

```css
/* bad */ {
  color : #333;
  border-top: 1px solid rgba(0,0,0,0.50);
  background : #f1f;
  border-radius: 50%;
}

/* good */ {
  background: #f1f1f1;
  border-radius: 50%;
  border-top: 1px solid rgba(0, 0, 0, .5);
  color: #333333;
}
```

### Formatting
* Use 2 spaces for indentation (and set up your IDE so this is done automatically).
* Use spaces for aligning properties in block lists.
* Put a space before the opening brace `{` in rule declarations.
* Put closing braces `}` of rule declarations on a new line.
* Don't use unnecessary indentation.
* Use single stringquotes e.g. `content: 'hello';`. These are easier to type (no shift required).

### Border

Use `0` instead of `none` to specify that a style has no border.

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```

### Z-index

Don't go overboard with z-indexes like 9999. This is bad for performance and also not well maintanable.

Instead, check where the breakpoint for your z-index is. You can always use intervals of 10. A general rule of thumb is:
* 0 - 100: Any specific component layering, e.g. a caption over an image.
* 100 - 200: Tooltips and other small, local, interactive overlays.
* 200 - 300: Dropdowns. Common examples include menus and select boxes.
* 300 - 400: Fixed position elements. Fixed headers and footers are clear examples of fixed page elements, but it could also include a drag-and-drop element in a drag state.
* 400 - 500: Dialogs and other full-page overlays. Slide panes are another good example of a common UI pattern in this range. It includes any widget that is intended to cover all page content, or that often is used with an underlay.
* 500 +*: Alerts and special cases. Toast notifications could potentially be in this range, or any component important enough to interrupt all other interaction.

### Comments

* Use as little comments as possible. Your code should be so clear, it should speak for itself. Don't write comments in abundance.
* Never comment out styling, just remove it entirely. If you wish to get it back later, you can retrieve it from Version Control.
* Prefer line comments (`//`) to block comments. Block comments for linters (only if absolutely necessary) or right-to-left exceptions are OK.
* Put comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-explanatory e.g. compatibility or overrides for third-party plugins.

**Bad**

```css
/* Card */
.card {
  padding: 1rem;
  // margin: 1rem;
}
```

**Good**

```css
// Do not use to hide for screenreaders. Use 'show-for-sr' instead!
.hide {
  display: none !important;
}

.knowly {
  left: 0 #{'/*! rtl:ignore */'};
}
```

### OOCSS and BEM

We encourage some combination of OOCSS and BEM for these reasons:

  * It helps create clear, strict relationships between CSS and HTML
  * It helps us create reusable, composable components
  * It allows for less nesting and lower specificity
  * It helps in building scalable stylesheets

**OOCSS**, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusable, repeatable snippets that can be used independently throughout a website.
To learn more about OOCSS read [OOCSS wiki](https://github.com/stubbornella/oocss/wiki) and [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/).

**BEM**, or “Block-Element-Modifier”, is a _naming convention_ for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.
To learn more about BEM read: [BEM 101](https://css-tricks.com/bem-101/) and [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/).

* Apply BEM to clearly distinguishable components (objects) e.g. don't do an entire pagefooter in one BEM instance. You can make separate components of linklists etc.
* Make the the components as small as possible, so it is easy the re-use those blocks in the future.
* Use only one level of BEM depth (no .block__element__element--modifier).

```css
/* block.css */
.block { }
.block__title { }
.block__content { }
.block--modifier { }
```

## SCSS

### General

* Use the `.scss` syntax, never the original `.sass` syntax
* Put blank lines between rule declarations, mixins and functions.
* Each Components gets its own file in /components, preceding the file name with an underscore: _component-name.scss.
* Each Component SCSS file should have a max of 100 lines, if it's longer it should be split up into separate components.

### Vendor prefixes

Don't write vendor prefixes, these will be auto added to the generated CSS by [Autoprefixer](https://github.com/postcss/autoprefixer).

```scss
/* bad */ {
  border-radius: 50%;
  -moz-border-radius: 50%;
  -webkit-border-radius: 50%;
}

/* good */ {
  border-radius: 50%;
}
```

### Ordering of property declarations

1. Property declarations

List all standard property declarations, anything that isn't an `@include` or a nested selector. Sort properties following alphabetically.

```scss
.button {
  background: $green;
  font-weight: bold;
  transition: background .2s ease-in-out;
}
```

2. `@include` declarations

    Grouping `@include`s at the beginning makes it easier to read the entire selector. Overwriting stuff in the include is also easier.

```scss
.button {
  @include transition(background .5s ease);
  background: $green;
  font-weight: bold;
  // ...
}
```

3. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Don't add blank lines between blocks. Apply the same guidelines as above to your nested selectors.

```scss
.button {
  @include transition(background .5s ease);
  background: $green;
  font-weight: bold;
  .icon {
    margin-right: 10px;
  }
}
```

3. BEM selectors

Nest BEM elements and modifiers. BEM selectors go after any declarations and before nested selectors. Elements come first and modifiers come second. Separate with a blank line. Writing modifier blocks is ok.
```scss
.button {
  @include transition(background .5s ease);
  background: $green;
  font-weight: bold;
  &__element {
    float: right;
  }
  .icon {
    margin-right: 10px;
  }
  &--expanded {
    width: 100%;
  }
  &--small  {
    width: 25%;
  }
  &--medium {
    width: 50%;
  }
  &--large  {
    width: 75%;
  }
}
```

We use a set order for the nested blocks as following:

```scss
.block {
  // First all the BEM-children
  &__title {}
  &__content {}
  // Then all the non-BEM-children
  .intro {}
  p {}
  // Then all the modifiers, because you can also modify the children within the modifiers more easily
  &--modifier {}
  // Then optionally the parents that modify the block
  .parent & {}
}
```

### Variables
Global variables should be declared in **_settings.scss**. BEM variables should be declared at the start of the BEM component and their names should resemble that of the component.
* Don't use hex values directly in rule declarations. Instead use variables like `$primary-color` where possible.
* Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names.

```scss
/* bad */
$primaryColor: rgba(0,0,0,.5);

/* good */
$primary-color: rgba(0, 0, 0, .5);
```

### If/else
If and else should be placed on their own lines.
```scss
@if {
  ...
}
@else {
  ...
}
```

### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.
* Mixin names should be written in hyphenated lowercase (kebab-case).
* Global mixins should be placed in _mixins.scss. Component-only usage mixins should be in their respective component files.

### Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins. Furthermore, this is usually a sign that your component is too big and needs to be split up into separate components.

### Nested selectors
**Do not nest selectors more than three levels deep!**

```scss
.page-container {
  .content {
    .profile {
    // STOP!
    }
  }
}
```
When selectors become this long, you're likely writing CSS that is:

* Strongly coupled to the HTML (fragile) *—OR—*
* Overly specific (powerful) *—OR—*
* Not reusable
* Not component-based

Again: **never nest ID selectors!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

## JavaScript hooks

Avoid binding to CSS classes with JavaScript. By mixing these two, design and functionality are mixed, which causes dependencies on both sides. You should be able to freely change the CSS classes without having to worry to break the Javascript, and vice versa. Keep them separated!

Create data-attributes to bind to and add CSS classes for changing the appearance of an element based on the interaction. If you change the way something looks, use a CSS class. If you are changing the behavior, use a data-attribute:

```html
<button data-open="bookingModal" class="button button--cta">Request to Book</button>
<div id="bookingModal" data-modal class="modal modal--open" data-modal>...</div>
```
