# CSS Styleguide #

## Coding Style ##

* Use soft-tabs with a two space indent.
* Put spaces after `:` in property declarations.
* Put spaces before `{` in rule declarations.
* Use hex color codes `#000` unless using rgba.
* Use `//` or `#` for comment blocks (instead of `/* */`).

Here's a good example:

    .styleguide-format {
      border: 1px solid #0f0;
      color: #000;
      background: rgba(0,0,0,0.5);
    }

## SCSS Style ##

Any `$variable` or `@mixin` that is used in more than one file should be put in `partials/_base.scss`. Others should be put at the top of the file where they're used.

As a rule of thumb, don't nest further than 3 levels deep. If you find yourself going further, think about reorganizing your rules (either the specificity needed, or the layout of the nesting).

## File Organization ##

In general, file organization goes like this:

    app/assets/stylesheets
    ├── application.css.scss
    ├── formatting.css.scss
    ├── home.css.scss
    ├── ie.css.scss
    ├── layout.css.scss
    ├── partials
    │   ├── _base.css.scss
    │   ├── _buttons.css.scss
    │   └── _forms.css.scss
    ├── print.css.scss
    ├── refinery
    │   └── site_bar.css.scss
    ├── refinery-custom.css.scss
    ├── search.scss

Use SASS to include files instead of Sprokets. Example:

    # application.css.scss
    @import 'refinery/site_bar';
    @import 'partials/base';
    @import 'formatting';
    @import 'partials/forms';
    @import 'partials/buttons';
    @import 'layout';
    @import 'search';

## Pixels vs. Ems ##

Use `px` for `font-size`, because it offers absolute control over text. Additionally, unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

## Specificity (classes vs. ids) ##

Elements that occur **exactly once** inside a page should use IDs, otherwise, use classes. When in doubt, use a class name.

* **Good** candidates for ids: header, footer, modal popups.
* **Bad** candidates for ids: navigation, item listings, item view pages (ex: issue view).

Here's an example:

    <ul class="category-list">
      <li class="item">Category 1</li>
      <li class="item">Category 2</li>
      <li class="item">Category 3</li>
    </ul>

    .category-list {
      &> li {
        list-style-type: disc;
      }
      a {
        color: #ff0000;
      }
    }

### CSS Specificity guidelines

If you must use an id selector (`#selector`) make sure that you have no more than one in your rule declaration. A rule like `#header .search #quicksearch { ... }` is considered harmful.

When modifying an existing element for a specific use, try to use specific class names. Instead of `.listings-layout.bigger` use rules like `.listings-layout.listings-bigger`. Think about ack/greping your code in the future.

The class names `disabled`, `mousedown`, `danger`, `hover`, `selected`, and `active` should always be namespaced by a class (`button.classy.selected` is a good example).
