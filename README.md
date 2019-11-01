# epub-wordcount

Given an epub file, do our best to count the number of words in it.

## Basic Usage

On the CLI:

```
% word-count path/to/book.epub

The Strange Case of Dr. Jekyll and Mr. Hyde
-------------------------------------------
  * 26,341 words
```

In code:

```ts
// TS:
import { countWords } from 'epub-wordcount'

// JS:
// const { countWords } = require('epub-wordcount')

countWords('./books/some-book.epub').then(numWords => {
  console.log(`There are ${numWords} words`)
})
// There are 106190 words
```

## CLI

There's also a cli tool to quickly get the count of any epub file! Invoke it via:

```bash
word-count path/to/file.epub
```

or

```bash
word-count directory/of/books
```

See `word-count -h` for more info

### Options

- `-c, --chars` - Print the character count instead of the world count
- `-r, --raw` - Instead of printing the nice title, just print out a numeral
- `-t, --text` - Print out the whole text of the book. Great for passing into other unix functions, like `wc`.

## Code API

There are a number of functions exported from this package. Each one takes either a path to a file or an already-parsed file. Mostly you'll use the path, but if the epub you're parsing is in a non-standard format, then you might use that function to ensure the file parses correctly. See [here](https://github.com/julien-c/epub#usage) for the options available.

- `countWords(pathOrEpub) => Promise<number>`
- `countCharacters(pathOrEpub) => Promise<number>`
- `getText(pathOrEpub) => Promise<string[]>`

Each of the above can be passed the result of the following:

- `parseEpubAtPath(path) => Promise<EPub>`

## Limitations

There's no programmatic representation for the table of contents in epub and it's hard to skip over the reviews, copyright, etc. An effort is made to only parse the actual story text, but there's a margin of error. Probably no more than ~500 words.

Pull requests welcome.

## Test Books

Unit tests are run on the following e-books:

- Stevenson's _THE STRANGE CASE OF DR. JEKYLL AND MR. HYDE_, from the public domain, provided by [Standard Ebooks](https://standardebooks.org/ebooks/robert-louis-stevenson/the-strange-case-of-dr-jekyll-and-mr-hyde)
- A copy of _The Martian_, by Andy Weir. This is my copy, purchased from Apple Books. It's DRM encumbered, so releasing it publicly should not be seen as copyright infringement.
