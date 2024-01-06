# Exporting diagrams

The diagram itself is an HTML element, but the main issue is that browsers do not provide a way to export an HTML element as an image.

The current solution is to capture the diagram element, convert to a data URL, then download it as an image.

The conversion step is handled by [html-to-image](https://github.com/bubkoo/html-to-image).
It provides simple APIs to capture an HTML element and convert it to a data URL.
In the project, I used `toPng`, `toSvg` and `toJpeg` functions.

The download step is handled by [FileSaver.js](https://github.com/eligrey/FileSaver.js)

Here is a snippet of the code:

```ts
const HTMLNode = document.getElementById(
	"structogram-preview",
);
if (HTMLNode === null) {
	return;
}
toSvg(HTMLNode).then((blob) => {
	if (blob === null) {
		return;
	}
	if (window.saveAs) {
		window.saveAs(blob, "diagram");
	} else {
		saveAs(blob, "diagram");
	}
});
```
