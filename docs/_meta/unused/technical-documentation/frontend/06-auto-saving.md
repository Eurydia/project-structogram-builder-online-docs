# Auto-saving

The save the progress of the user, the application automatically saves the content of the code editor to the browser's local storage when a change has been made to the code editor.

```ts
useEffect(() => {
	localStorage.setItem(
		"editorContent",
		editorContent,
	);
}, [editorContent]);
```

This is a very simple solution, but it is not perfect.

There will be cases where the user opened a sharable link while having some previous progress saved in the local storage.
In this case, the content of the code editor will be overwritten by the content of the sharable link.

I have decided that the sharable link should take precedence over the local storage, so the content of the sharable link will be loaded into the code editor if it is available.

```ts
const url = new URL(window.location.href);
const content = url.searchParams.get("content");
if (content !== null) {
	window.localStorage.setItem("content", content);
	return content;
}

const savedContent =
	window.localStorage.getItem("content");
if (savedContent !== null) {
	return savedContent;
}
return "";
```
