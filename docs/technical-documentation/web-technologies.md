# Web techologies

In this project, I have used quite a few third party libraries and frameworks, so let's discuss about them and their roles in this project.

## JavaScript frameworks

The project is built with [React](https://reactjs.org/) [TypeScript](https://www.typescriptlang.org/) and [Vite](https://vitejs.dev/).

There is no particular reason why I chose them apart from the fact that I am most comfortable with them.

## UI libraries

I have used [Material UI](https://material-ui.com/) for the UI components.
I think the components are very well designed and they are easy to use, on top of looking modern and clean.

The icons are from the same library.
I was tempted to use other icon libraries like [Font Awesome](https://fontawesome.com/) or [Feather Icons](https://feathericons.com/), but I decided to stick with Material UI for style consistency.

## Snackbars and notifications

I used [Notistack](https://iamhosseindhv.com/notistack) for snackbars and notifications.
It provides nice APIs for snackbars and notifications, and it is very easy to use.
But the primary reason is because Notistack is built on top of Material UI, so it is very easy to integrate it with Material UI.

## Text editor

I used [CodeMirror](https://codemirror.net/) for this project.

## Export to image

One of the main features of this project is the ability to export the diagram as an image.

Unfornately, browsers do not provide a way to export an HTML element as an image, so I had to use [html-to-image](https://github.com/bubkoo/html-to-image) to convert the diagram to an image, then download it with [FileSaver.js](https://github.com/eligrey/FileSaver.js)
