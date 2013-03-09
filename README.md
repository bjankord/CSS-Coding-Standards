CSS-Coding-Standards
====================

Personal coding standards for crafting CSS

This is a living document. My goal is to update this as my knowledge evolves and promote more consistency in my own code.

## Format

* Prefer tabs to spaces when indenting CSS. (Developers can change Tab Size in their editors to choose desired width)
* Add a single space after your selector(s).
* If more than 3 selectors are in use, separated by commas, put each selector on a new line.
* Put each declaration on its own line. (Multi-lined)
* Indent each declaration by 1 tab.
* Use quotes when need in selctors or values.
* Prefer double qoutes in when used. `input[type="checkbox"]`
* Prefer shorthand hex values for colors. `background-color: #fff;`
* Use lowercase for properties and values.
* When using zero as a value, leave it unitless. `margin: 0;`
* Order your CSS rules alphabetically.
* Put prefixed rules before the unprefixed rules.
* Line up prefixed declarations so values are in line vertically.
* Add a space between properties and values after the colon.
* Include a semi-colon after every declaration, including the last declaration.
* Place closing bracket of declaration block on its own line.
* Add one blank line bewteen rulesets.


**Formating Example:**

    .success {
    	background-color: #dff0d8;
    	border-color: #d6e9c6;
    	color: #468847;
    	-webkit-border-radius: 15px;
    	   -moz-border-radius: 15px;
    	        border-radius: 15px;
    	font-weight: 700;
        margin: .5em 0;
        padding: .3em;
    }

    .error {
    	background-color: #f2dede;
    	border-color: #eed3d7;
    	color: #b94a48;
    	-webkit-border-radius: 15px;
    	   -moz-border-radius: 15px;
    	        border-radius: 15px;
        font-weight: 700;
        margin: .5em 0;
        padding: .3em;
    }

## Stucture

Currently, the [most efficient way to serve CSS for multiple devices is via 1 stylesheet](http://andydavies.me/blog/2012/12/29/think-twice-before-using-matchmedia-to-conditionally-load-stylesheets/). Try to keep all styles in one stylesheet to avoid additional HTTP requests. 

### Ordering your styles

Follow the SMACSS ordering strucure:

* **Base**
* **Layout**
* **Modules**
* **States**

### Base Styles

These consist of all HTML elements. Create styles just for the HTML elements you have on your site. If your building a CMS theme, where content will be generated by users, create styles for all HTML elements in case users add them through the CMS.

If you find that you have to overwrite your base styles often, refactor your base styles so the are more generic and make better defaults.

### Layout Styles

In SMACSS, Johnathan talks about using the prefix `l-` to designate layout styles. I have not found a need for this in my stylesheets, though it is important to be aware of this practice. I know other developers have adopted this practice.

Layout styles should be wrappers for modules, these are things like your website's header, footer, body, sidebar. These will typically match up with ARIA Landmark Roles. Use classes for your layout styles. I've seen some people use attribute selectors like [role=header]. I'm on the fence about this, in one case it ties styles to just one instance and makes them less reusable, at the same time, you will probly only have one sidebar, one site footer, one site header. I prefer to add classes instead of attribute selectors for these instances.

### Modules

Modules make up a majority of a websites styles. There are three parts to modules.

* Modules
* Modifiers
* Subcomponents


Move common stlyes into a module and create module modifiers for unique instances.

Below as an example of an alert module with 2 modifiers.

**Module Example 1**

    .alert {
        -webkit-border-radius: 15px;
           -moz-border-radius: 15px;
                border-radius: 15px;
    	font-weight: 700;
        margin: .5em 0;
        padding: .3em;
    }
    
    .alert--success {
        background-color: #dff0d8;
    	border-color: #d6e9c6;
    	color: #468847;
    }

    .alert--error {
    	background-color: #f2dede;
    	border-color: #eed3d7;
    	color: #b94a48;
    }
    

**Module Naming Conventions**

There are [various naming conventions](http://www.brettjankord.com/2013/03/06/more-thoughts-on-html-class-naming-conventions/). Below is my preferred naming convention for modules, modifiers, and subcomponents.

    .module {...}
    .module--modifier {...}  /* Use double dash for modifiers */
    .module-subcomponent {...}  /* Use single dash for subcomponents */
    .module-subcomponent--modifier {...} /* A modifier on a subcomponent */

If your module name is two or more words, use camel case. This allow dashes to represent distinctions between modules, modifiers, and subcomponents. 

    .moduleName {...} /* Correct module naming *
    .productReviews {...}  /* Correct module  naming */
    .product-reviews {...} /* Incorrect module naming */
    
**Subcomponent Naming Conventions**

A header, body, and footer are common subcomponents of modules. In OOCSS, the these subcomponents have these class names: `.hd, .bd, .ft`

If I am abbreviating class names, I use 3 letters at minimum. `.hdr, .bdy, .ftr`
    
**Full example of the three parts of modules.**

    .entry {...} /* Module */
    .entry-hdr {...}   /* Module Subcomponent */
    .entry-title {...} /* Module Subcomponent */
    .entry-meta {...}  /* Module Subcomponent */
    .entry-bdy {...}  /* Module Subcomponent */
    .entry-meta--sub {...} /* Module Subcomponent Modifier */
    .entry--featured {...} /* Module Modifier */

### States

States styles are things like media queries, :hover, :focus, etc., and JavaScript states.

* Include state styles that after the styles they are affecting.
* Prefix JavaScript states with `js-`
* Prefer classes for JavaScript hooks compared to IDs or data-attributes. This allows them to be reusable, though still performant in querying the DOM.

As for generic states like, `js-is-hidden`, include these in a **State section** following your **Modules section** in your stylesheet.

## Comments

I've adopted Nicholas Gallagehr's commenting guidelines from [Idiomatic CSS](https://github.com/necolas/idiomatic-css) with my own minor adjustments.

* Place comments on a new line above their subject.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Create a comment for each main section, base, layout, modules, and state.
* Create comments for sub-sections, typically I add these above modules.
* Add 3 lines before sub-section comments when they follow styles. See below example 2.
* There should be no lines sections and sub-section comments
* There should be no lines between sections/sub-sections and multiline comments.


**Comment types example inspired by Idiomatic CSS comments**
 
    /*----------------------------------------------------------------------------
     * Section comment block
    ----------------------------------------------------------------------------*/

    /* Sub-section comment block
    --------------------------------------*/
    
    /**
     * The first sentence of the long description starts here and continues on this
     * line for a while finally concluding here at the end of this paragraph.
     *
     * The long description is ideal for more detailed explanations and
     * documentation. It can include example HTML, URLs, or any other information
     * that is deemed necessary or useful.
     */
    
    /* Basic comment */

**Comment spacing example**

    /*----------------------------------------------------------------------------
     * Modules
    ----------------------------------------------------------------------------*/
    /* Post Entries
    --------------------------------------*/
    /**
     * Styles post entries and featured post entries. Included here could be more
     * details about the styles for other developers.
     */
    
    .entry {...} 
    .entry--featured {
      *display: inline; /* IE7 and lower fix */
      *zoom: 1; /* IE7 and lower fix */
    }
    
    
    /* Buttons
    --------------------------------------*/
    .btn {...} 
    .btn--primary {...}
    
## Additional recommendations
* Avoid using IDs for styling. IDs can be used for anchor links, though do not use them for styling. The specifity they add can be difficult work with.
* If you are minifing your CSS, include a link in a comment to view the unminified CSS.
