====================================================================================================
    A QUICK HOW-TO ABOUT CRAYON LANGUAGE FILES v.1.0
    For updated info, visit http://ak.net84.net/ or check out twitter.com/crayonsyntax
====================================================================================================

----------------------------------------------------------------------------------------------------
    KNOWN ELEMENTS
----------------------------------------------------------------------------------------------------
These are known, recognised and highlighted by Crayon. You can defined others, but if you want to 
highlight them, you must add your custom CSS class into a Theme file.

    NAME                    CSS Class     
  -------------------------------------
    COMMENT                 [c]
    STRING                  [s]

    KEYWORD                 [k]
        STATEMENT           [st]
        RESERVED            [r]
        TYPE                [t]
        MODIFIER            [m]

    IDENTIFIER              [i]
        ENTITY              [e]
        VARIABLE            [v]

    CONSTANT                [cn]

    OPERATOR                [o]

    SYMBOL                  [sy]
    
    NOTATION                [n]
    
    FADED                   [f]
    
    HTML_CHAR               [h]
    
Read more about these in the online documentation (see link above).

----------------------------------------------------------------------------------------------------
    RULES
----------------------------------------------------------------------------------------------------
# Global
    - Whitespace must be used to separate element names, css classes and regex
    - Must be defined on a single line
# Elements
    - Defined as ELEMENT_NAME [css] REGEX, in that order only
    - Names cannot contain whitespace: [-_a-zA-Z]+[-_a-zA-Z0-9]*
    - When defining an unknown element, you can specify a fallback with a colon:
        e.g. MAGIC_WORD:KEYWORD [mg] \bmagic|words|here\b
        - If the Theme doesn't support the '.mg' class, it will still highlight using the KEYWORD 
          class '.k'
        - Add support for the '.mg' class by adding it at the bottom of the Theme CSS file, after 
          the fallback
    - If duplicate exists, it replaces previous
# CSS
    - CSS classes are defined in [square brackets], they are optional.
    - No need to use '.' in class name. All characters are converted to lowercase and dots removed.
    - If you use a space, then two classes are applied to the element matches.
        e.g. [first second]
    - If not specified, either default is used (if element is known), or element name is used
    - Class can be applied to multiple elements
    - Class should be valid: [-_a-zA-Z]+[-_a-zA-Z0-9]*
    - If class is invalid, element is still parsed, error reported
# Regex
    - Written as per normal, without delimiters or escaping
    - Applied in the order they appear in the file
        If language has reserved keywords, these should be higher than variables
    - Whitespace around regex is ignored - only first character to last forms regex
    - If single space is intended, use \s to avoid conflict with whitespace used for separation
        e.g. TEST [t] \s\s\shello
# Comments
    - can be added to this file using # // or /* */
    - // # and /* must be the first non-whitespace characters on that line
    - The */ must be on a line by itself

----------------------------------------------------------------------------------------------------
    SPECIAL FUNCTIONS
----------------------------------------------------------------------------------------------------
    - Written inside regex, replaced by their outputs when regex is parsed.
# (?alt:file.txt)
    - Import lines from a file and separate with alternation
        e.g. catdog|dog|cat
    - File should list words from longest to shortest to avoid clashes
# (?default)
  (?default:element_name)
    - Substitute regex with Default language's regex for that element, or a specific element
      given after a colon.
# (?html:somechars)
    - Convert somechars to html entities
        e.g. (?html:<>"'&) becomes &lt;&gt;&quot;&amp;
