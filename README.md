# The Rails Initialization Process

This book walks through from Go-to-Woah for the Rails initialization process, starting at "rails server" and finishing up with a request being served through a controller to render a view.

## Generating from AsciiDoc

To generate this book, install the bundle:

    bundle install

To generate the book, pick a format and run the appropriate rake command:

    asciidoctor book.adoc
    rake init:html
    rake init:epub
    rake init:mobi
    rake init:pdf


## Contributing

Contributions to this book are done via GitHub Issues and Pull Requests. If you find something wrong, the first step is to file an issue about it. Please include:

1. The chapter where the issue occurs
2. The text around the issue so that we can locate it
3. Any other info you deem necessary

If you want to submit a Pull Request to fix this issue, all the better! AsciiDoc isn't as bad as [some formats](http://www.docbook.org/)
