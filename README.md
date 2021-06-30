
# Software Installation
Since all of this was tested and installed on my Mac, the information given in
this docment is Mac-centric.  I use Homebrew, but I imagine that MacPorts and
Fink would work just fine as well.  Some of the file locations will be
different if you use those package managers.


## xmllint
My Mac already had xmllint installed.  It is in `/usr/local`, so it must have
been installed as a dependency somewhere along the way.  The conversion script
to output `*.odt` files first converts the asciidoc file to DocBook format using
Asciidoc/Ascidoctor then uses pandoc to convert to `*.odt`.  Pandoc doesn't set
some of the template variables needed for my templates so I use xmllint to
extract the needed data from the DocBook xml.  This data is then passed to
pandoc via command line arguments to set the variables manually.


## Pandoc
Pandoc is used by my scripts to convert to `*.odt` and `*.docx` formats.
Installation instructions can be found here: https://pandoc.org/installing.html


## Asciidoc
Asciidoc is the Python implementation.  It is the original implementation and is
not being continued.  It remains available and is quite capable.

### Install Asciidoc
`brew install asciidoc`

### Scripts
`asciidocs/build_scripts/a2h` Converts an asciidoc document to html (Functional)

`asciidocs/build_scripts/a2o` Converts an asciidoc document to an ODT document (Functional)

`asciidocs/build_scripts/a2p` Converts an asciidoc document to a PDF (Functional)

`asciidocs/build_scripts/a2w` Converts an asciidoc document to a word document (No templates possible)

### Templates


## Asciidoctor (Ruby implementation - current standard)
I started with the `brew` packaged version of asciidoctor, but quickly found out
that I had no idea how to add new gems to the installation.  Instead, I decided
to install ruby and some of the pre-requisites via `brew` and then use the `gem`
command to install asciidoctor.

### Install Asciidoctor pre-requisites:
Install ruby and some pre-requisites for the ruby gems:
```bash
brew install ruby
brew install glib gdk-pixbuf cairo pango cmake
brew link gettext --force
```

- *Tilt* allows you to create your own templates for asciidoctor to use.
- *pygments.rb* is used by asciidoctor to perform syntax highlighting

```bash
gem install tilt
gem install pygments.rb
```

### Install Asciidoctor
I found an extension to asciidoctor called `asciidoctor-pdf`[1].  This extension,
coupled with an add-on called `asciidoctor-mathematical` [2] allows you to
embed latex math equations in your document and produce high quality PDFs.  As a
bonus, when you install the extension, asciidoctor gets installed as a
dependency.

[1] https://asciidoctor.org/docs/asciidoctor-pdf/#install-the-published-gem)

[2] https://github.com/asciidoctor/asciidoctor-mathematical)

```bash
gem install asciidoctor-pdf --pre
gem install asciidoctor-mathematical
```

### Scripts
`asciidoctor/build_scripts/a2h` Converts an asciidoc document to html (Not implemented yet)

`asciidoctor/build_scripts/a2o` Converts an asciidoc document to an ODT document (Functional)

`asciidoctor/build_scripts/a2p` Converts an asciidoc document to a PDF (No templates yet)

`asciidoctor/build_scripts/a2w` Converts an asciidoc document to a word document (No templates possible)

### Templates
