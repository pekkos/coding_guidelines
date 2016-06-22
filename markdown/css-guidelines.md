## CSS pre-processing WITH LESS

No CSS is written manually, all CSS has to be compiled from LESS (http://lesscss.org). LESS is a CSS pre-processor, that helps keeping the CSS source code structured and re-usable. LESS comes with a lot of functions, such as declaring variables that can be re-used throughout the project, mixins that can be included into a selector declaration, color management and much more. LESS is also setup to help serving the right styles for various media query based screen sizes, and to serve legacy versions of Internet Explorer. A tutorial on LESS can be found here: http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/get-into-less-the-programmable-stylesheet-language/.

LESS needs to be compiled to CSS before loading into a browser. To compile the code, you need a compiler, such as the LESS app for Mac or WinLESS for Windows. These are both free to download and use. However, for Mac there’s an excellent app called CodeKit that besides compiling LESS to can be configured to debug and minify Javascript, among other things. Highly recommended! More on CodeKit further on.

## CSS basics

Write structured CSS/LESS, and comment the code generously.
  * Put a space after :
  * Put a space after // for comments
  * Put a space after commas (e.g. ''rgba(101, 101, 101, 0.6)'' )
  * Use only RGB and RGBA format for colors
  * Avoid ID:s and stick to classes

## LESS

LESS code is written much in the same way as CSS, with additional features of declaring variables and functions. Mixins can be generalised and take input values to cater for various uses. Mixins are also very usable to take care of cases when vendor prefixes such as -webkit-, -moz- or -ms- need to be used.

A mixin called border-radius has a default border-radius of 10px for all corners, and it contains the vendor prefixed declarations.

<code css>
.border-radius (@radius: 10px 10px 10px 10px) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     border-radius: @radius;
}
</code>

The selector .example-box has some CSS declarations and includes the mixin .border-radius with an input value of 5px.

<code css>
.example-box {
     padding: 10px;
     background-color: rgb(101,101,101);
    .border-radius(5px);
}
</code>

The result in compiled CSS will as follows:

<code css>
.example-box {
     padding: 10px;
     background-color: rgb(101,101,101);
     -webkit-border-radius: 5px;
     -moz-border-radius: 5px;
     border-radius: 5px;
}
</code>

## Responsive Web Design

Responsive Web Design is a technique that uses fluid layout, flexible media and media queries to cater for optimal user experiences in various screen sizes. Media queries, such as @media (min-width: 400px), are understood by modern browsers, and by setting up breakpoints and combining min-widths with max-widths we can serve different screen sizes different designs.

## No mediaqueries

The first media query is the lack of media queries, which means that there has to be a basic design and layout for browsers that don’t understand media queries.

## Media queries and the CSS cascade

Then using a set of breakpoints, we layer designs onto the basic experience using the CSS cascade from small screens up to large screens. Using the cascade means that a browser in large screen mode gets all the css declarations from small up to large, so at every breakpoint only the additions and alterations need to be included, since the previous declarations are already included.

Any declarations that are only applicable to a certain screen size range, say in between two breakpoints should be put in a media query that uses both min-width and max-width. The current design has a fixed max-width, so the page content area never exceeds 1040px, except the Hero module, which is “full screen width”.

## Legacy Internet Explorer

Internet Explorer version 8 and lower don’t understand media queries, so IE7 and IE8 receives a CSS file that adds the cascading CSS without media query declarations. IE6 receives only the basic experience, though.

Internet Explorer 8 and below don’t handle fluid layouts well, without writing up lots och workarounds in the CSS. Due to this and the fact that these browsers can’t understand media queries, IE8 and below gets a fixed width layout, and thus not the responsive fluid layout.


## Breakpoints

Breakpoints shouldn’t be set to contemporary, popular device screen sizes. Content should imply where a breakpoint is needed. In the current design of telia.se, the list layout module is used to find suitable breakpoints. The list layout switches from 1 or 2 columns in the smallest width up to 4 or 5 columns in the largest width. The breakpoints are set where the layout list module needs to add more columns in order to keep looking good.

* Every module should have a base file that contains the standard behavior. Each mediaquery is then added on top of that with modifications for each screensize.
* The naming conventions for these files are:
    * basefile: `[modulename]/[modulename].less`
    * each mediaquery file: `[modulename]/[modulename]-mq-[nameofbreakpoint].less`
* **Never have inline mediaqueries.** I.e. do not write a `@media...` within an existing file. Instead use the import pattern.
* Each module mq file should be imported thru either `all.less` or `ie-lte8.less`. The projects themselves shouldn't need to care about a modules different files.

###Standard breakpoints:

LESS variable | Width | in px (approx.) | Comment           |
--------------|-------|-----------------|-------------------|
@mq-xsmall    | 13em  | 200px           |-                  |
@mq-lt-small  | -     | -               | Lower than Small  |
@mq-small     | 31em  | 500px           |-                  |
@mq-lt-medium | -     | -               | Lower than Medium |
@mq-medium    | 44em  | 700px           |-                  |
@mq-lt-large  | -     | -               | Lower than Large  |
@mq-large     | 56em  | 900px           |-                  |
@mq-lt-xlarge | -     | -               | Lower than XLarge |
@mq-xlarge    | 75em  | 1200px          |-                  |

##Template for `all.less`

`@import "[modulename]"`

`@media only screen and (min-width: @mq-xsmall) 								{ @import "[modulename]-mq-xsmall"; }`
`@media only screen and (min-width: @mq-xsmall) and (max-width: @mq-lt-small) 	{ @import "[modulename]-mq-xsmall-only"; }`
`@media only screen and (min-width: @mq-xsmall) and (max-width: @mq-lt-medium) 	{ @import "[modulename]-mq-xsmall--small"; }`
`@media only screen and (min-width: @mq-xsmall) and (max-width: @mq-lt-large) 	{ @import "[modulename]-mq-xsmall--medium"; }`
`@media only screen and (min-width: @mq-small) 									{ @import "[modulename]-mq-small"; }`
`@media only screen and (min-width: @mq-small) and (max-width: @mq-lt-medium)	{ @import "[modulename]-mq-small-only"; }`
`@media only screen and (min-width: @mq-small) and (max-width: @mq-lt-large) 	{ @import "[modulename]-mq-small--medium"; }`
`@media only screen and (min-width: @mq-medium) 								{ @import "[modulename]-mq-medium"; }`
`@media only screen and (min-width: @mq-medium) and (max-width: @mq-lt-large) 	{ @import "[modulename]-mq-medium-only"; }`
`@media only screen and (min-width: @mq-large) 									{ @import "[modulename]-mq-large"; }`


##Template for `ie-lte8.less`
For the IE < 8 stuff we don't include the basefile for the module and the mediaqueries that has a defined span. The basefile is already included inte the main CSS and the mq:s with spans will mess shit up if included.

`@media only screen and (min-width: @mq-xsmall) 								{ @import "[modulename]-mq-xsmall"; }`
`@media only screen and (min-width: @mq-small) 									{ @import "[modulename]-mq-small"; }`
`@media only screen and (min-width: @mq-medium) 								{ @import "[modulename]-mq-medium"; }`
`@media only screen and (min-width: @mq-large) 									{ @import "[modulename]-mq-large"; }`




## Naming conventions



Use the Telia Sonera namespace “ts” for class names, e.g. ''**.tsHeader**'', and use lowerCamelCase for class names with more than one word, e.g. ''**.tsNavPrimary**''





## Modules

Note: Module files should be named in the singular, unless your module's name is plural. For example: ''/modules/header/header.less''
Modules are broken down into the base module, submodules, modifiers, and states. If your module or submodule name is two words, use camelCase. For example, ''.tsModuleName''.

## Submodules

Submodules use the hyphen - separator to denote that it is a submodule to another module. For example, tsModule-SubModule.
Note: If you have a plural module (e.g. .tsTabs), you can name your submodule .tsTab as an exception to this rule. The assumption is made that .tsTab is a submodule of .tsTabs.


## Modifiers

Use ''--'' for a modifier on a module or submodule. For example:

   * .tsModule--Modifier
   * .tsModule-SubModule--Modifier.

Example .tsBtn--Primary

## States


Use the is-state, is-module-state, is-module-submodule-state pattern for your states. For example:

   * .is-active
   * .is-NavPrimary-TopLevelItem-active





## File structure

Every module has its own folder in the LESS folder under ''/modules/'', e.g. ''/modules/header/''. In that folder there are several LESS files, one base file, one for every media query and/or combinated media query ranges. There are also a couple of files that imports the other files to be included in the master LESS file.


  * ''/modules/header/header.less'' - This file contains the base experience
  * ''/modules/header/header-mq-xsmall.less'' - This file contains the styles for screen sizes of xsmall and up
  * ''/modules/header/all.less'' - This file imports the base file and the styles files for different screen sizes. The file contains the actual media queries
  * ''/modules/header/ie-lte8.less'' - This file imports the styles within the media query files, but without media queries, to add the whole cascading styles for IE8 and lower.
  * ''/modules/header/print.less'' - This file imports the media query files and any additional styles required for printing the module. Modules may be hidden completely from print here too, using display: none;
