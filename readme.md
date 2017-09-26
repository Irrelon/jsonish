# JSONish - A JSON Pre-Processor

JSONish is a JSON pre-processor inspired by CSS pre-processors like
LESS and SASS. It extends the JSON language adding the ability to import
JSON into other JSON files. This allows you to spread your JSON data
over multiple files such as when your application needs a single file
for each language it is translated in but you want to keep your
translation files in the same folder as the HTML, CSS and JS for each
component of your application.

In the following example of JSONish, we import another JSON file into
our main one:

Our example file structure is:

```
- Root
|-- en.jsonish
|-- components
    |-- home
        |-- home.json
        |-- home.html
        |-- home.js
        |-- home.less
```    

### en.jsonish

```jsonish
{
	"homeComponent": @import("./components/home/home.json"),
	"otherStuff": {
		"hello": "Hey ya!",
		"goodbye": "See ya!"
	}
}
```

> Note that the import directives can take either a .json file OR a .jsonish
file. If the file extension is not specified the processor checks for a jsonish
file by that name first, then a json file.

The import directive is replaced by the processed contents of the file that
it references.

If ./components/home/home.json had this contents:

```json
{
	"homeTitle": "Welcome"
}
```

Then the processed en.jsonish file would output:

```json
{
	"homeComponent": {
    	"homeTitle": "Welcome"
    },
	"otherStuff": {
		"hello": "Hey ya!",
		"goodbye": "See ya!"
	}
}
```

This allows you to spread the JSON data for your application across multiple
files and folders allowing you to organise data in a more clean and structured
way like LESS and SASS have done for CSS.

# Usage

## JetBRains IDE File Watcher

1) Add a new file type called "JSONish" to your IDE with the file extension "jsonish"

2) Add a new file watcher to execute jsonish to preprocess your jsonish files

