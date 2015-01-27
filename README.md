# Coq website
This repository contains the static pages of the Coq website

Pre-html sources are in `pages/` and `news/`, while final html files
will be assembled in `dest/`.

## Prerequisites
The html files are pre-processed by [Yamlpp](http://www.lri.fr/~filliatr/yamlpp.en.html). A copy of
yamlpp is included in this repository, we simply need an OCaml
toplevel to run it as a script. If you further modify the source
file `yamlpp.mll` to customize the pre-processing, you will also need
`ocamllex` to regenerate `yamlpp.ml`.

## How to edit an existing page?
* Look in the PAGES file which is the corresponding source file.
   For instance "download/" is pages/3.html
   Nota: for the moment, these numbers in pages/ correspond
   to former Drupal nodes.
* Edit this source file
* Run "make" and check that the produced file is ok (e.g. dest/node/3.html)
   If that may help, "make run" launches a small local webserver
* Commit your change and push it to the main repository
   The update of coq.inria.fr should then be automatic (TODO)

## How to create a new page?
* Add your new file in pages/. File name is up to you, but please
   avoid strange ones. Files in pages/ will be pre-processed by Yamlpp
   (see yamlpp-*/README for me details). Basically, to be uniform with
   the other pages of the site, your file should look like:

   <#def TITLE> your page title </#def>
   <#include "incl/header.html">
   Your html code corresponding roughly to the inner of the html body
   <#include "incl/footer.html">

   In addition, you could add just after the TITLE two other macro definitions:
   - HEAD : anything in it will be added at the end of the <head> section
   - PATH : some code displayed before the title of your page, usually
     a sequence of links to your page ancestors. See Drupal's breadcrumb.
     By default: <a href="/">Home</a>.

* Ensure that your page is built and installed. Normally, this amounts to
   adding a new line to the PAGES file, with the shape "localname:nicename".
   You could add multiple lines to have multiple aliases for the same page.

   Nota: for pages converted from Drupal, the relevant part of the url is
   now a directory, in with we place an index.html. This approach is also
   recommended for new pages, but not mandatory.

* make, verify, commit, push as for the edition of an existing page below.

## And for news?
* Add a new file in news/ with an increased number as filename.
   You can for instance copy news/template and adapt it, or any existing
   news files. See news/template for details about the expected syntax.

* In the file NEWS, add your news number, with an optional url alias.
   In the Makefile, update the $(RECENTNEWS) variable.

* make, verify, commit, push as usual
