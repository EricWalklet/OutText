# OutText #

OutText is a jQuery plugin that generates for randomly-selected (and not-so-randomly-selected) words throughout an HTML document.

## Dependencies ##

* jQuery 1.11.0

## Features ##

* Can be used on the entire page, or within a select portion of the document.
* Random link generation according to a configurable frequency.
* Restricts link creation within certain element types.
* Allows configurable "priority words" that will always yield OutText links.
* Recognizes leading and trailing punctuation, ignoring them when creating links.

## Usage ##

OutText can be registered in two different ways.

* Apply OutText to the entire document:

```javascript
$.OutText({
	// ...
});
```

* Apply OutText to a selected portion of the document:

```javascript
$("#bodyText").OutText({
	// ...
});
```

There are a number of configuration properties supported at registration time, but none of them are required.

### Configuring the OutText Link ###

The HREF of the link created by OutText can be specified using the <code>link_template</code> property.

```javascript
$.OutText({
	link_template: "https://www.google.com/#q={t}"
});
```

The <code>{t}</code> token represents where the inner text of an OutText link will be used to construct the URL.  For example, if an OutText link is generated from the word <code>javascript</code> using the above example, the final link will resemble the following:

```html
<a href="https://www.google.com/#q=javascript">javascript</a>
```

If no <code>{t}</code> token is present, the HREF will be created exactly as specified.

**Default:** <code>#</code>

### Configuring the Frequency of Link Generation ###

The default behavior of OutText is to randomly-generate links from the pool of available words on the page.  The frequency at which links are generated can be configured using the <code>frequency</code> property.

```javascript
$.OutText({
	frequency: 0.3
});
```

The <code>frequency</code> property accepts any number between zero (no OutText links will be randomly generated) and one (all available words will be turned into OutText links).

*Default:* <code>0.1</code>

### Blocking Link Generation within Certain Element Types ###

On most web pages, there are a number of elements that may not behave or appear correctly if an OutText link were to be created within them.  At registration time, these elements can be excluded from consideration when generating links.

```javascript
$.OutText({
	excluded_elements: ["p", "b", "i", "u"]
});
```

The <code>excluded_elements</code> accepts an array of case-insensitive strings, each element of which is the name of an HTML node.  If a matching node is encountered anywhere within the OutText registration area, no OutText links will be created within it.

This property has the highest priority of all available configuration properties.  Even with a configured frequency of 100%, no OutText links will be created within these nodes.

**Default:** <code>["button", "a"]</code>

### Always Generate Links from Specific Words ###

If OutText is to be used in some sort of a targeted link campaign, it may be valuable to *always* generate an OutText link from a specific set of words.  This is possible.

```javascript
$.OutText({
	forced_words: ["bacon", "hoagie"]
});
```

When OutText encounters these words in the document, it will ignore any configured frequency setting and always generate a link from this word.  This setting will still respect, however, any configured excluded element types.

OutText will not force link generation on a word that contains extra characters, including leading or trailing punctuation, or a word that is split by additional inner HTML tags.

```html
<!-- This will generate a forced OnText link. -->
George: Some bacon would be really nice right now.

<!-- So will this. -->
Bob: But you ATE ALL THE BACON last night!

<!-- But this won't. -->
George: I can't help it if I can't resist the wonders of bacon!

<!-- And neither will this. -->
Bob: Stop saying B<b>A</b>C<i>O</i>N so much!
```

**Default:** <code>[]</code>

## Author ##

* [Eric Walklet](https://github.com/Renaissance2K)