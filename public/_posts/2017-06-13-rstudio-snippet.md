<!-- 
---
layout: post
title: "R Studio Code Snippets"
date: 2017-06-13
---
-->
I have a long standing (bad) habit of not leveraging all of R Studio's
feature to my advantage. It's only been in the last couple of months
that I've started using the autocomplete functionality. But I've had
good motivation to look further into the perks that the Integrated
Development Environment has to offer me.

<!--excerpt-->
I am under strict configuration control procedures at BGCAPP, which has
largely been a blessing. One of the few disadvantages I encountered with
the configuration control procedures is that I was unable to immediately
take advantage of [Document
Templates](http://rmarkdown.rstudio.com/developer_document_templates.html)
when they were first released--the version of R Studio I had in my
configuration didn't yet support it.

Fortunately, I've recently developed a good need to upgrade my version
of R (I'm currently using 3.2.2), and while I'm making upgrades to R, I
may as well upgrade all of the software that supports my Statistical
Computing Environment. Thus, I finally get to adopt Document Templates
(yay!)

While I was exploring the latest verison of R Studio in my development
environment, I began to look at additional features. I turned on the
auto completion and for once it didn't annoy me. In fact, I've come to
love it. I installed a Document Template for my Laboratory's document
style, and I already love being able to access it easily. The only thing
more I could want is an R script template.

Oh wait! R Studio supports that...sort of.

While R Studio doesn't offer script templates, per se, it does support
code snippets. And truthfully, they're even better. A script template
would be a static template, while code snippets let you both insert code
and designate places you can quickly tab to in order to insert the
relevant code for your current needs.

As an example, one of the default code snippets is

    snippet if
        if (${1:condition}) {
            ${0}
        }

When calling this snippet, the `if` block is inserted into your code,
and the cursor automatically moves between the `if` parentheses. After
typing your condition, hitting `TAB` moves the cursor to the next `$`
position inside the braces.

By defining code snippets for yourself, you can create building blocks
that you use often, insert them when you need them, and fill in the
non-static parts easily.

One of my personalized snippets is the code to load all of the packages
I use on a regular basis.

    snippet pkgs
      library(broom)
      library(dplyr)
      library(ggplot2)
      library(magrittr)
      library(pixiedust)
      library(reshape2)
      library(stringr)
      library(tidyr)

And now I can insert all of that code with just the key strokes `p`,
`k`, `g`, and `TAB`.

The rest of these snippets are what I have defined in my non-work
environment where I develop packages. There are a few concepts I use
often that have a few variations. I've defined snippets to address each
of those variations, as its faster to insert the snippet than it is to
type out all of the code. Some of these are modifications of R Studios
default snippets that conform to my personal coding style.

Don't forget that you can also define snippets for Markdown, C++, and
several other languages under Tools &gt; Global Options &gt; Code &gt;
Edit Snippets

    snippet pkgs
        library(broom)
        library(dplyr)
        library(ggplot2)
        library(magrittr)
        library(pixiedust)
        library(reshape2)
        library(stringr)
        library(tidyr)

    snippet fnanon
        ${1} <- function(${2})
        {
            ${3}
        }
        
    snippet fnpkg
        #' @name ${1}
        #' @title ${2}
        #' 
        #' @description ${3}
        #' 
        #' @param ${4}
        #'
        #' @details ${5}
        #' 
        #' @author Benjamin Nutter
        #' 
        #' @section Functional Requirements:
        #' \enumerate{
        #'  \item 
        #' }
        #'
        #' @export
        ${6} <- function(${7})
        {
            ${8}
        }
        
    snippet checkmate
        coll <- checkmate::makeAssertCollection()
        
        ${1}
        
        checkmate::reportAssertions(coll)

    snippet assert_char
        checkmate::assert_character(x = ${1})
        
    snippet assert_char_add
        checkmate::assert_character(x = ${1},
                                    add = coll)
        
    snippet nullassert_char
        if (!is.null(${1}))
        {
            checkmate::assert_character(x = ${2})
        }
        
    snippet nullassert_char_add
        if (!is.null(${1}))
        {
            checkmate::assert_character(x = ${2},
                                        add = coll)
        }
        
    snippet assert_lgl
        checkmate::assert_logical(x = ${1})
        
    snippet assert_lgl_add
        checkmate::assert_logical(x = ${1},
                                  add = coll)
        
    snippet nullassert_lgl
        if (!is.null(${1}))
        {
            checkmate::assert_logical(x = ${2})
        }
        
    snippet nullassert_lgl_add
        if (!is.null(${1}))
        {
            checkmate::assert_logical(x = ${2},
                                      add = coll)
        }
        
    snippet assert_int
        checkmate::assert_integerish(x = ${1})
        
    snippet assert_int_add
        checkmate::assert_integerish(x = ${1},
                                     add = coll)    
        
    snippet nullassert_int
        if (!is.null(${1}))
        {
            checkmate::assert_integerish(x = ${2})
        }
        
    snippet nullassert_int_add
        if (!is.null(${1}))
        {
            checkmate::assert_integerish(x = ${2},
                                         add = coll)
        }
        
    snippet assert_num
        checkmate::assert_numeric(x = ${1})
        
    snippet assert_num_add
        checkmate::assert_numeric(x = ${1},
                                  add = coll)
        
    snippet nullassert_num
        if (!is.null(${1}))
        {
            checkmate::assert_numeric(x = ${2})
        }
        
    snippet nullassert_num_add
        if (!is.null(${1}))
        {
            checkmate::assert_numeric(x = ${2},
                                      add = coll)
        }
        
    snippet if_nutter
        if (${1}) 
        {
            ${0}
        }

    snippet else_nutter
        else 
        {
            ${0}
        }

    snippet elseif_nutter
        else if (${1}) 
        {
            ${0}
        }

    snippet fun
        ${1:name} <- function(${2}) 
        {
            ${0}
        }

    snippet for
        for (${1} in ${2}) 
        {
            ${0}
        }

    snippet while
        while (${1}) 
        {
            ${0}
        }

    snippet switch
        switch (
            ${1},
            ${2} = ${3}
        )

    snippet apply
        apply(X = ${1}, 
                  MARGIN = ${2}, 
                  FUN = ${3})

    snippet lapply
        lapply(X = ${1}, 
                   FUN = ${2})

    snippet sapply
        sapply(X = ${1}, 
               FUN = ${2})

    snippet mapply
        mapply(FUN = ${1}, 
               ${2})

    snippet vapply
        vapply(X = ${1}, 
               FUN = ${2}, 
               FUN.VALUE = ${3})
