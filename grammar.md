# Minimal HTML Grammar (EBNF)

This document defines a simplified HTML grammar **Extended Backus-Norus Form (EBNF)**.
It is not a full specification but illustrates the core structure of an HTML document.
---
## Grammer
```ebnf
Document		      = "<!DOCTYPE html>" HtmlElement
HtmlElement	      = "<html>" HeadElement BodyElement "</html>"
HeadElement	      = "<head>" HeadContent "</head>"
HeadContent	      = (TitleElement | MetaElement | LinkElement)*
TitleElement	    = "<title>" Text "</title>"
MetaElement		    = "<meta" Attribute* ">"
LinkElement		    = "<link" Attribute* ">"
BodyElement		    = "<body>" Content* "</body>"
Content 			    = Element | Text
Element 			    = DivElement
							    | ParagraphElement
							    | HeadingElement
							    | ImageElement
							    | ListElement
DivElement 		    = "<div" Attribute* ">" Content* "</div>"
ParagraphElement	=	"<p>" Text "</p>"
HeadingElement		= "<h1>" Text "</h1>"
									|	"<h2>" Text "</h2>"
									| "<h3>" Text "</h3"
ImageElement			= "<img" Attribute* "/>"
ListElement				= UnorderedList | OrderedList
UnorderedList			= "<ul>" ListItem+ "</ul>"
OrderedList				= "<ol>" ListItem+ "</ol>"
ListItem					= "<li>" Content*	"</li>"
Attribute					= Name "=" "\"" Value "\""
Name							= Letter {Letter | Digit | "-"}
Value							= {Letter | Digit | " "	| "." | "/" | "-"}
Text							= {Letter | Digit | " " | "!" | "?"	| "."	| ","	}	
Letter						= "a" | ...	| "z" | "A" | ... | "Z"
Digit             = "0" | ... | "9"
```
## Notes
- {...} -> zero or more repetitions
- {... | ...} -> alternatives
- [...] -> optional (not used here)
- ε -> empty (nothing)

## Example Parse
For the following HTML:
```html
<div>
	<p> Hello, World! </p>
</div>
```
We can expand it as:
```html
DivElement
 └── <div>
     Content
      └── ParagraphElement
          └── <p>
              Text → "Hello, world!"
          └── </p>
     └── </div>

```
