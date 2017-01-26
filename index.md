<!doctype html>
<html>
<head>
<meta charset='UTF-8'><meta name='viewport' content='width=device-width initial-scale=1'>
<title>Linux 意外操作后如何进行数据抢救.md</title><link href='http://fonts.googleapis.com/css?family=Open+Sans:400italic,700italic,700,400&subset=latin,latin-ext' rel='stylesheet' type='text/css'><style type='text/css'>html, body {overflow-x: initial !important;}.CodeMirror { height: auto; }
.CodeMirror-scroll { overflow-y: hidden; overflow-x: auto; }
.CodeMirror-lines { padding: 4px 0px; }
.CodeMirror pre { }
.CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler { background-color: white; }
.CodeMirror-gutters { border-right: 1px solid rgb(221, 221, 221); background-color: rgb(247, 247, 247); white-space: nowrap; }
.CodeMirror-linenumbers { }
.CodeMirror-linenumber { padding: 0px 3px 0px 5px; text-align: right; color: rgb(153, 153, 153); }
.CodeMirror div.CodeMirror-cursor { border-left: 1px solid black; z-index: 3; }
.CodeMirror div.CodeMirror-secondarycursor { border-left: 1px solid silver; }
.CodeMirror.cm-keymap-fat-cursor div.CodeMirror-cursor { width: auto; border: 0px; background: rgb(119, 238, 119); z-index: 1; }
.CodeMirror div.CodeMirror-cursor.CodeMirror-overwrite { }
.cm-tab { display: inline-block; }
.cm-s-typora-default .cm-header, .cm-s-typora-default .cm-property { color: rgb(217, 79, 138); }
.cm-s-typora-default pre.cm-header1:not(.cm-atom) :not(.cm-overlay) { font-size: 2rem; line-height: 2rem; }
.cm-s-typora-default pre.cm-header2:not(.cm-atom) :not(.cm-overlay) { font-size: 1.4rem; line-height: 1.4rem; }
.cm-s-typora-default .cm-atom, .cm-s-typora-default .cm-number { color: rgb(149, 132, 134); }
.cm-s-typora-default .cm-table-row, .cm-s-typora-default .cm-block-start { font-family: monospace; }
.cm-s-typora-default .cm-comment, .cm-s-typora-default .cm-code { color: rgb(74, 90, 159); font-family: monospace; }
.cm-s-typora-default .cm-tag { color: rgb(169, 68, 66); }
.cm-s-typora-default .cm-string { color: rgb(126, 134, 169); }
.cm-s-typora-default .cm-link { color: rgb(196, 122, 15); text-decoration: underline; }
.cm-s-typora-default .cm-variable-2, .cm-s-typora-default .cm-variable-1 { color: inherit; }
.cm-s-typora-default .cm-overlay { font-size: 1rem; font-family: monospace; }
.CodeMirror.cm-s-typora-default div.CodeMirror-cursor { border-left: 3px solid rgb(228, 98, 154); }
.cm-s-typora-default .CodeMirror-activeline-background { left: -60px; right: -30px; background: rgba(204, 204, 204, 0.2); }
.cm-s-typora-default .CodeMirror-gutters { border-right: none; background-color: inherit; }
.cm-s-typora-default .cm-trailing-space-new-line::after, .cm-startspace::after, .cm-starttab .cm-tab::after { content: "•"; position: absolute; left: 0px; opacity: 0; font-family: LetterGothicStd, monospace; }
.os-windows .cm-startspace::after, .os-windows .cm-starttab .cm-tab::after { left: -0.1em; }
.cm-starttab .cm-tab::after { content: " "; }
.cm-startspace, .cm-tab, .cm-starttab, .cm-trailing-space-a, .cm-trailing-space-b, .cm-trailing-space-new-line { font-family: monospace; position: relative; }
.cm-s-typora-default .cm-trailing-space-new-line::after { content: "↓"; opacity: 0.3; }
.cm-s-inner .cm-keyword { color: rgb(119, 0, 136); }
.cm-s-inner .cm-atom, .cm-s-inner.cm-atom { color: rgb(34, 17, 153); }
.cm-s-inner .cm-number { color: rgb(17, 102, 68); }
.cm-s-inner .cm-def { color: rgb(0, 0, 255); }
.cm-s-inner .cm-variable { color: black; }
.cm-s-inner .cm-variable-2 { color: rgb(0, 85, 170); }
.cm-s-inner .cm-variable-3 { color: rgb(0, 136, 85); }
.cm-s-inner .cm-property { color: black; }
.cm-s-inner .cm-operator { color: rgb(152, 26, 26); }
.cm-s-inner .cm-comment, .cm-s-inner.cm-comment { color: rgb(170, 85, 0); }
.cm-s-inner .cm-string { color: rgb(170, 17, 17); }
.cm-s-inner .cm-string-2 { color: rgb(255, 85, 0); }
.cm-s-inner .cm-meta { color: rgb(85, 85, 85); }
.cm-s-inner .cm-qualifier { color: rgb(85, 85, 85); }
.cm-s-inner .cm-builtin { color: rgb(51, 0, 170); }
.cm-s-inner .cm-bracket { color: rgb(153, 153, 119); }
.cm-s-inner .cm-tag { color: rgb(17, 119, 0); }
.cm-s-inner .cm-attribute { color: rgb(0, 0, 204); }
.cm-s-inner .cm-header, .cm-s-inner.cm-header { color: blue; }
.cm-s-inner .cm-quote, .cm-s-inner.cm-quote { color: rgb(0, 153, 0); }
.cm-s-inner .cm-hr, .cm-s-inner.cm-hr { color: rgb(153, 153, 153); }
.cm-s-inner .cm-link, .cm-s-inner.cm-link { color: rgb(0, 0, 204); }
.cm-negative { color: rgb(221, 68, 68); }
.cm-positive { color: rgb(34, 153, 34); }
.cm-header, .cm-strong { font-weight: bold; }
.cm-del { text-decoration: line-through; }
.cm-em { font-style: italic; }
.cm-link { text-decoration: underline; }
.cm-error { color: rgb(255, 0, 0); }
.cm-invalidchar { color: rgb(255, 0, 0); }
.cm-constant { color: rgb(38, 139, 210); }
.cm-defined { color: rgb(181, 137, 0); }
div.CodeMirror span.CodeMirror-matchingbracket { color: rgb(0, 255, 0); }
div.CodeMirror span.CodeMirror-nonmatchingbracket { color: rgb(255, 34, 34); }
.cm-s-inner .CodeMirror-activeline-background { background: inherit; }
.CodeMirror { position: relative; overflow: hidden; }
.CodeMirror-scroll { margin-bottom: -30px; margin-right: -30px; padding-bottom: 30px; padding-right: 30px; height: 100%; outline: none; position: relative; box-sizing: content-box; }
.CodeMirror-sizer { position: relative; }
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler { position: absolute; z-index: 6; display: none; }
.CodeMirror-vscrollbar { right: 0px; top: 0px; overflow-x: hidden; overflow-y: scroll; }
.CodeMirror-hscrollbar { bottom: 0px; left: 0px; overflow-y: hidden; overflow-x: scroll; }
.CodeMirror-scrollbar-filler { right: 0px; bottom: 0px; }
.CodeMirror-gutter-filler { left: 0px; bottom: 0px; }
.CodeMirror-gutters { position: absolute; left: 0px; top: 0px; padding-bottom: 30px; z-index: 3; }
.CodeMirror-gutter { white-space: normal; height: 100%; box-sizing: content-box; padding-bottom: 30px; margin-bottom: -32px; display: inline-block; }
.CodeMirror-gutter-elt { position: absolute; cursor: default; z-index: 4; }
.CodeMirror-lines { cursor: text; }
.CodeMirror pre { border-radius: 0px; border-width: 0px; background: transparent; font-family: inherit; font-size: inherit; margin: 0px; white-space: pre; word-wrap: normal; color: inherit; z-index: 2; position: relative; overflow: visible; }
.CodeMirror-wrap pre { word-wrap: break-word; white-space: pre-wrap; word-break: normal; }
.CodeMirror-code pre { border-right: 30px solid transparent; width: fit-content; }
.CodeMirror-wrap .CodeMirror-code pre { border-right: none; width: auto; }
.CodeMirror-linebackground { position: absolute; left: 0px; right: 0px; top: 0px; bottom: 0px; z-index: 0; }
.CodeMirror-linewidget { position: relative; z-index: 2; overflow: auto; }
.CodeMirror-widget { }
.CodeMirror-wrap .CodeMirror-scroll { overflow-x: hidden; }
.CodeMirror-measure { position: absolute; width: 100%; height: 0px; overflow: hidden; visibility: hidden; }
.CodeMirror-measure pre { position: static; }
.CodeMirror div.CodeMirror-cursor { position: absolute; visibility: hidden; border-right: none; width: 0px; }
.CodeMirror div.CodeMirror-cursor { visibility: hidden; }
.CodeMirror-focused div.CodeMirror-cursor { visibility: inherit; }
.CodeMirror-selected { background: rgb(217, 217, 217); }
.CodeMirror-focused .CodeMirror-selected { background: rgb(215, 212, 240); }
.cm-searching { background: rgba(255, 255, 0, 0.4); }
.CodeMirror span { }
@media print { 
  .CodeMirror div.CodeMirror-cursor { visibility: hidden; }
}
.CodeMirror-lint-markers { width: 16px; }
.CodeMirror-lint-tooltip { background-color: infobackground; border: 1px solid black; border-radius: 4px; color: infotext; font-family: monospace; overflow: hidden; padding: 2px 5px; position: fixed; white-space: pre-wrap; z-index: 10000; max-width: 600px; opacity: 0; transition: opacity 0.4s; font-size: 0.8em; }
.CodeMirror-lint-mark-error, .CodeMirror-lint-mark-warning { background-position: left bottom; background-repeat: repeat-x; }
.CodeMirror-lint-mark-error { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAQAAAADCAYAAAC09K7GAAAAAXNSR0IArs4c6QAAAAZiS0dEAP8A/wD/oL2nkwAAAAlwSFlzAAALEwAACxMBAJqcGAAAAAd0SU1FB9sJDw4cOCW1/KIAAAAZdEVYdENvbW1lbnQAQ3JlYXRlZCB3aXRoIEdJTVBXgQ4XAAAAHElEQVQI12NggIL/DAz/GdA5/xkY/qPKMDAwAADLZwf5rvm+LQAAAABJRU5ErkJggg=="); }
.CodeMirror-lint-marker-error, .CodeMirror-lint-marker-warning { background-position: center center; background-repeat: no-repeat; cursor: pointer; display: inline-block; height: 16px; width: 16px; vertical-align: middle; position: relative; }
.CodeMirror-lint-message-error, .CodeMirror-lint-message-warning { padding-left: 18px; background-position: left top; background-repeat: no-repeat; }
.CodeMirror-lint-marker-error, .CodeMirror-lint-message-error { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAAHlBMVEW7AAC7AACxAAC7AAC7AAAAAAC4AAC5AAD///+7AAAUdclpAAAABnRSTlMXnORSiwCK0ZKSAAAATUlEQVR42mWPOQ7AQAgDuQLx/z8csYRmPRIFIwRGnosRrpamvkKi0FTIiMASR3hhKW+hAN6/tIWhu9PDWiTGNEkTtIOucA5Oyr9ckPgAWm0GPBog6v4AAAAASUVORK5CYII="); }
.CodeMirror-lint-marker-warning, .CodeMirror-lint-message-warning { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAMAAAAoLQ9TAAAANlBMVEX/uwDvrwD/uwD/uwD/uwD/uwD/uwD/uwD/uwD6twD/uwAAAADurwD2tQD7uAD+ugAAAAD/uwDhmeTRAAAADHRSTlMJ8mN1EYcbmiixgACm7WbuAAAAVklEQVR42n3PUQqAIBBFUU1LLc3u/jdbOJoW1P08DA9Gba8+YWJ6gNJoNYIBzAA2chBth5kLmG9YUoG0NHAUwFXwO9LuBQL1giCQb8gC9Oro2vp5rncCIY8L8uEx5ZkAAAAASUVORK5CYII="); }
.CodeMirror-lint-marker-multiple { background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAcAAAAHCAMAAADzjKfhAAAACVBMVEUAAAAAAAC/v7914kyHAAAAAXRSTlMAQObYZgAAACNJREFUeNo1ioEJAAAIwmz/H90iFFSGJgFMe3gaLZ0od+9/AQZ0ADosbYraAAAAAElFTkSuQmCC"); background-repeat: no-repeat; background-position: right bottom; width: 100%; height: 100%; }


html { font-size: 14px; background-color: rgb(255, 255, 255); color: rgb(51, 51, 51); }
body { margin: 0px; padding: 0px; height: auto; bottom: 0px; top: 0px; left: 0px; right: 0px; font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; font-size: 1rem; line-height: 1.42857; overflow-x: hidden; background: inherit; }
a:active, a:hover { outline: 0px; }
.in-text-selection, ::selection { background: rgb(181, 214, 252); text-shadow: none; }
#write { margin: 0px auto; height: auto; width: inherit; word-break: normal; word-wrap: break-word; position: relative; padding-bottom: 70px; white-space: pre-wrap; overflow-x: auto; }
.for-image #write { padding-left: 8px; padding-right: 8px; }
body.typora-export { padding-left: 30px; padding-right: 30px; }
@media screen and (max-width: 500px) { 
  body.typora-export { padding-left: 0px; padding-right: 0px; }
  .CodeMirror-sizer { margin-left: 0px !important; }
  .CodeMirror-gutters { display: none !important; }
}
.typora-export #write { margin: 0px auto; }
#write > p:first-child, #write > ul:first-child, #write > ol:first-child, #write > pre:first-child, #write > blockquote:first-child, #write > div:first-child, #write > table:first-child { margin-top: 30px; }
#write li > table:first-child { margin-top: -20px; }
img { max-width: 100%; vertical-align: middle; }
input, button, select, textarea { color: inherit; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; font-size: inherit; line-height: inherit; font-family: inherit; }
input[type="checkbox"], input[type="radio"] { line-height: normal; padding: 0px; }
::before, ::after, * { box-sizing: border-box; }
#write p, #write h1, #write h2, #write h3, #write h4, #write h5, #write h6, #write div, #write pre { width: inherit; }
#write p, #write h1, #write h2, #write h3, #write h4, #write h5, #write h6 { position: relative; }
h1 { font-size: 2rem; }
h2 { font-size: 1.8rem; }
h3 { font-size: 1.6rem; }
h4 { font-size: 1.4rem; }
h5 { font-size: 1.2rem; }
h6 { font-size: 1rem; }
p { -webkit-margin-before: 1rem; -webkit-margin-after: 1rem; -webkit-margin-start: 0px; -webkit-margin-end: 0px; }
.mathjax-block { margin-top: 0px; margin-bottom: 0px; -webkit-margin-before: 0rem; -webkit-margin-after: 0rem; }
.hidden { display: none; }
.md-blockmeta { color: rgb(204, 204, 204); font-weight: bold; font-style: italic; }
a { cursor: pointer; }
#write input[type="checkbox"] { cursor: pointer; width: inherit; height: inherit; margin: 4px 0px 0px; }
tr { break-inside: avoid; break-after: auto; }
thead { display: table-header-group; }
table { border-collapse: collapse; border-spacing: 0px; width: 100%; overflow: auto; break-inside: auto; text-align: left; }
table.md-table td { min-width: 80px; }
.CodeMirror-gutters { border-right: 0px; background-color: inherit; }
.CodeMirror { text-align: left; }
.CodeMirror-placeholder { opacity: 0.3; }
.CodeMirror pre { padding: 0px 4px; }
.CodeMirror-lines { padding: 0px; }
div.hr:focus { cursor: none; }
pre { white-space: pre-wrap; }
.CodeMirror-gutters { margin-right: 4px; }
.md-fences { font-size: 0.9rem; display: block; break-inside: avoid; text-align: left; overflow: visible; white-space: pre; background: inherit; position: relative !important; }
.md-diagram-panel { width: 100%; margin-top: 10px; text-align: center; padding-top: 0px; padding-bottom: 8px; overflow-x: auto; }
.md-fences .CodeMirror.CodeMirror-wrap { top: -1.6em; margin-bottom: -1.6em; }
.md-fences.mock-cm { white-space: pre-wrap; }
.show-fences-line-number .md-fences { padding-left: 0px; }
.show-fences-line-number .md-fences.mock-cm { padding-left: 40px; }
.footnotes { opacity: 0.8; font-size: 0.9rem; padding-top: 1em; padding-bottom: 1em; }
.footnotes + .footnotes { margin-top: -1em; }
.md-reset { margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: top; background: transparent; text-decoration: none; text-shadow: none; float: none; position: static; width: auto; height: auto; white-space: nowrap; cursor: inherit; -webkit-tap-highlight-color: transparent; line-height: normal; font-weight: normal; text-align: left; box-sizing: content-box; direction: ltr; }
li div { padding-top: 0px; }
blockquote { margin: 1rem 0px; }
li p, li .mathjax-block { margin: 0.5rem 0px; }
li { margin: 0px; position: relative; }
blockquote > :last-child { margin-bottom: 0px; }
blockquote > :first-child { margin-top: 0px; }
.footnotes-area { color: rgb(136, 136, 136); margin-top: 0.714rem; padding-bottom: 0.143rem; }
@media print { 
  html, body { height: 100%; }
  .typora-export * { -webkit-print-color-adjust: exact; }
  h1, h2, h3, h4, h5, h6 { break-after: avoid-page; orphans: 2; }
  p { orphans: 4; }
  html.blink-to-pdf { font-size: 13px; }
  .typora-export #write { padding-left: 1cm; padding-right: 1cm; }
  .typora-export #write::after { height: 0px; }
  @page { margin: 20mm 0mm; }
}
.footnote-line { margin-top: 0.714em; font-size: 0.7em; }
a img, img a { cursor: pointer; }
pre.md-meta-block { font-size: 0.8rem; min-height: 2.86rem; white-space: pre-wrap; background: rgb(204, 204, 204); display: block; overflow-x: hidden; }
p .md-image:only-child { display: inline-block; width: 100%; text-align: center; }
#write .MathJax_Display { margin: 0.8em 0px 0px; }
.mathjax-block { white-space: pre; overflow: hidden; width: 100%; }
p + .mathjax-block { margin-top: -1.143rem; }
.mathjax-block:not(:empty)::after { display: none; }
[contenteditable="true"]:active, [contenteditable="true"]:focus { outline: none; box-shadow: none; }
.task-list { list-style-type: none; }
.task-list-item { position: relative; padding-left: 1em; }
.task-list-item input { position: absolute; top: 0px; left: 0px; }
.math { font-size: 1rem; }
.md-toc { min-height: 3.58rem; position: relative; font-size: 0.9rem; border-radius: 10px; }
.md-toc-content { position: relative; margin-left: 0px; }
.md-toc::after, .md-toc-content::after { display: none; }
.md-toc-item { display: block; color: rgb(65, 131, 196); text-decoration: none; }
.md-toc-inner:hover { }
.md-toc-inner { display: inline-block; cursor: pointer; }
.md-toc-h1 .md-toc-inner { margin-left: 0px; font-weight: bold; }
.md-toc-h2 .md-toc-inner { margin-left: 2em; }
.md-toc-h3 .md-toc-inner { margin-left: 4em; }
.md-toc-h4 .md-toc-inner { margin-left: 6em; }
.md-toc-h5 .md-toc-inner { margin-left: 8em; }
.md-toc-h6 .md-toc-inner { margin-left: 10em; }
@media screen and (max-width: 48em) { 
  .md-toc-h3 .md-toc-inner { margin-left: 3.5em; }
  .md-toc-h4 .md-toc-inner { margin-left: 5em; }
  .md-toc-h5 .md-toc-inner { margin-left: 6.5em; }
  .md-toc-h6 .md-toc-inner { margin-left: 8em; }
}
a.md-toc-inner { font-size: inherit; font-style: inherit; font-weight: inherit; line-height: inherit; }
.footnote-line a:not(.reversefootnote) { color: inherit; }
.md-attr { display: none; }
.md-fn-count::after { content: "."; }
.md-tag { opacity: 0.5; }
.md-comment { color: rgb(162, 127, 3); opacity: 0.8; font-family: monospace; }
code { text-align: left; }
h1 .md-tag, h2 .md-tag, h3 .md-tag, h4 .md-tag, h5 .md-tag, h6 .md-tag { font-weight: initial; opacity: 0.35; }
a.md-print-anchor { border-width: initial !important; border-style: none !important; border-color: initial !important; display: inline-block !important; position: absolute !important; width: 1px !important; right: 0px !important; outline: none !important; background: transparent !important; text-decoration: initial !important; text-shadow: initial !important; }
.md-inline-math .MathJax_SVG .noError { display: none !important; }
.mathjax-block .MathJax_SVG_Display { text-align: center; margin: 1em 0em; position: relative; text-indent: 0px; max-width: none; max-height: none; min-height: 0px; min-width: 100%; width: auto; display: block !important; }
.MathJax_SVG_Display, .md-inline-math .MathJax_SVG_Display { width: auto; margin: inherit; display: inline-block !important; }
.MathJax_SVG .MJX-monospace { font-family: monospace; }
.MathJax_SVG .MJX-sans-serif { font-family: sans-serif; }
.MathJax_SVG { display: inline; font-style: normal; font-weight: normal; line-height: normal; zoom: 90%; text-indent: 0px; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0px; min-height: 0px; border: 0px; padding: 0px; margin: 0px; }
.MathJax_SVG * { transition: none; }


@font-face { font-family: "Open Sans"; font-style: normal; font-weight: normal; src: local("Open Sans Regular"), url("./github/400.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: italic; font-weight: normal; src: local("Open Sans Italic"), url("./github/400i.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: normal; font-weight: bold; src: local("Open Sans Bold"), url("./github/700.woff") format("woff"); }
@font-face { font-family: "Open Sans"; font-style: italic; font-weight: bold; src: local("Open Sans Bold Italic"), url("./github/700i.woff") format("woff"); }
html { font-size: 16px; }
body { font-family: "Open Sans", "Clear Sans", "Helvetica Neue", Helvetica, Arial, sans-serif; color: rgb(51, 51, 51); line-height: 1.6; }
#write { max-width: 860px; margin: 0px auto; padding: 20px 30px 100px; }
#write > ul:first-child, #write > ol:first-child { margin-top: 30px; }
body > :first-child { margin-top: 0px !important; }
body > :last-child { margin-bottom: 0px !important; }
a { color: rgb(65, 131, 196); }
h1, h2, h3, h4, h5, h6 { position: relative; margin-top: 1rem; margin-bottom: 1rem; font-weight: bold; line-height: 1.4; cursor: text; }
h1:hover a.anchor, h2:hover a.anchor, h3:hover a.anchor, h4:hover a.anchor, h5:hover a.anchor, h6:hover a.anchor { text-decoration: none; }
h1 tt, h1 code { font-size: inherit; }
h2 tt, h2 code { font-size: inherit; }
h3 tt, h3 code { font-size: inherit; }
h4 tt, h4 code { font-size: inherit; }
h5 tt, h5 code { font-size: inherit; }
h6 tt, h6 code { font-size: inherit; }
h1 { padding-bottom: 0.3em; font-size: 2.25em; line-height: 1.2; border-bottom: 1px solid rgb(238, 238, 238); }
h2 { padding-bottom: 0.3em; font-size: 1.75em; line-height: 1.225; border-bottom: 1px solid rgb(238, 238, 238); }
h3 { font-size: 1.5em; line-height: 1.43; }
h4 { font-size: 1.25em; }
h5 { font-size: 1em; }
h6 { font-size: 1em; color: rgb(119, 119, 119); }
p, blockquote, ul, ol, dl, table { margin: 0.8em 0px; }
li > ol, li > ul { margin: 0px; }
hr { height: 4px; padding: 0px; margin: 16px 0px; background-color: rgb(231, 231, 231); border-width: 0px 0px 1px; border-style: none none solid; border-top-color: initial; border-right-color: initial; border-left-color: initial; border-image: initial; overflow: hidden; box-sizing: content-box; border-bottom-color: rgb(221, 221, 221); }
body > h2:first-child { margin-top: 0px; padding-top: 0px; }
body > h1:first-child { margin-top: 0px; padding-top: 0px; }
body > h1:first-child + h2 { margin-top: 0px; padding-top: 0px; }
body > h3:first-child, body > h4:first-child, body > h5:first-child, body > h6:first-child { margin-top: 0px; padding-top: 0px; }
a:first-child h1, a:first-child h2, a:first-child h3, a:first-child h4, a:first-child h5, a:first-child h6 { margin-top: 0px; padding-top: 0px; }
h1 p, h2 p, h3 p, h4 p, h5 p, h6 p { margin-top: 0px; }
li p.first { display: inline-block; }
ul, ol { padding-left: 30px; }
ul:first-child, ol:first-child { margin-top: 0px; }
ul:last-child, ol:last-child { margin-bottom: 0px; }
blockquote { border-left: 4px solid rgb(221, 221, 221); padding: 0px 15px; color: rgb(119, 119, 119); }
blockquote blockquote { padding-right: 0px; }
table { padding: 0px; word-break: initial; }
#write { overflow-x: auto; }
table tr { border-top: 1px solid rgb(204, 204, 204); background-color: white; margin: 0px; padding: 0px; }
table tr:nth-child(2n) { background-color: rgb(248, 248, 248); }
table tr th { font-weight: bold; border: 1px solid rgb(204, 204, 204); text-align: left; margin: 0px; padding: 6px 13px; }
table tr td { border: 1px solid rgb(204, 204, 204); text-align: left; margin: 0px; padding: 6px 13px; }
table tr th:first-child, table tr td:first-child { margin-top: 0px; }
table tr th:last-child, table tr td:last-child { margin-bottom: 0px; }
.CodeMirror-gutters { border-right: 1px solid rgb(221, 221, 221); }
.md-fences, code, tt { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); border-radius: 3px; font-family: Consolas, "Liberation Mono", Courier, monospace; padding: 2px 4px 0px; font-size: 0.9em; }
.md-fences { margin-bottom: 15px; margin-top: 15px; padding: 8px 1em 6px; }
.task-list { padding-left: 0px; }
.task-list-item { padding-left: 32px; }
.task-list-item input { top: 3px; left: 8px; }
@media screen and (min-width: 914px) { 
}
@media print { 
  html { font-size: 13px; }
  table, pre { break-inside: avoid; }
  pre { word-wrap: break-word; }
}
.md-fences { background-color: rgb(248, 248, 248); }
#write pre.md-meta-block { padding: 1rem; font-size: 85%; line-height: 1.45; background-color: rgb(247, 247, 247); border: 0px; border-radius: 3px; color: rgb(119, 119, 119); margin-top: 0px !important; }
.mathjax-block > .code-tooltip { bottom: 0.375rem; }
#write > h3.md-focus::before { left: -1.5625rem; top: 0.375rem; }
#write > h4.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h5.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
#write > h6.md-focus::before { left: -1.5625rem; top: 0.285714rem; }
.md-image > .md-meta { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); border-radius: 3px; font-family: Consolas, "Liberation Mono", Courier, monospace; padding: 2px 4px 0px; font-size: 0.9em; color: inherit; }
.md-tag { color: inherit; }
.md-toc { margin-top: 20px; padding-bottom: 20px; }
#typora-quick-open { border: 1px solid rgb(221, 221, 221); background-color: rgb(248, 248, 248); }
#typora-quick-open-item { background-color: rgb(250, 250, 250); border-color: rgb(254, 254, 254) rgb(229, 229, 229) rgb(229, 229, 229) rgb(238, 238, 238); border-style: solid; border-width: 1px; }
#md-notification::before { top: 10px; }
.on-focus-mode blockquote { border-left-color: rgba(85, 85, 85, 0.117647); }
header, .context-menu, .megamenu-content, footer { font-family: "Segoe UI", Arial, sans-serif; }






</style>
</head>
<body class='typora-export' >
<div  id='write'  class = 'is-node'><h2><a name='header-c179' class='md-header-anchor '></a>Linux 意外操作后如何进行数据抢救</h2><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125120304628-720092779.png" width="800px"></p><p>在 GUI 中使用  <code>shift + delete</code>  组合键或是 CLI 下使用 <code>rm -rf</code> 删除选项，这个文件并没有从硬盘（或是其它存储设备）上彻底销毁。它仅仅是从系统的目录结构中被移除，然后你在删除文件的目录下就看不到该文件了，但是这个文件仍然存在你磁盘中的某个 <code>block</code> 物理位置上。（ <code>ls -li</code> 或 <code>stat</code> 查询、显示一个文件名所对应的 <a href='https://en.wikipedia.org/wiki/Inode'>inode</a> 的元信息数据。 ）。</p><p>注意：<strong><a href='https://en.wikipedia.org/wiki/RAID'>独立硬盘冗余阵列</a></strong>（<strong>RAID</strong>, <strong>R</strong>edundant <strong>A</strong>rray of <strong>I</strong>ndependent <strong>D</strong>isks）损坏或数据丢失，不在本次范围。</p><hr /><p><strong>Linux 系统管理员守则中有这么一条：“慎用 rm -rf 命令，除非你知道此命令所带来的后果“</strong></p><p></p><h3><a name='header-c192' class='md-header-anchor '></a>一、实验环境</h3><p>VMware® Workstation 12 Pro 12.5.2 build-4638234</p><p>CentOS-6.5-x86_64-bin-DVD1.iso</p><h3><a name='header-c197' class='md-header-anchor '></a>二、恢复工具</h3><hr /><h4><a name='header-c199' class='md-header-anchor '></a><a href='http://extundelete.sourceforge.net' target='_blank' title='完成'>extundelete</a></h4><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125200144456-989913250.png" width="800px"></p><p><center>注意：即便不能实现重新只读挂载当前数据盘，也绝对不能在需要恢复文件的目录下进行操作。</center></p><h5><a name='header-c204' class='md-header-anchor '></a>1 -&gt; 安装</h5><pre class='md-fences mock-cm' style='display:block;position:relative'># curl -O https://nchc.dl.sourceforge.net/project/extundelete/extundelete/0.2.4/extundelete-0.2.4.tar.bz2
# tar -jxvf extundelete-0.2.4.tar.bz2 &amp;&amp; cd extundelete-0.2.4 
# ./configure --prefix=/usr/local/extundelete
-------------------
configure: error: C++ compiler cannot create executables
# yum install gcc gcc-c++ -y
configure: error: Can&#39;t find ext2fs library
# yum install e2fsprogs.x86_64 e2fsprogs-devel.x86_64 e2fsprogs-libs.x86_64  -y
-------------------
make &amp;&amp; make install</pre><h5><a name='header-c206' class='md-header-anchor '></a>2 --&gt;选项</h5><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete /dev/sdb1 --inode 2
查找可恢复的数据信息，标记为Deleted状态的是已经删除的文件或目录。</pre><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170126105005769-348282016.png" width="800px"></p><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete /dev/sdb1 --restore-inode 12,13
extundelete /dev/sdb1 --restore-file fstab
extundelete  /dev/sdb1 --after 1293877800  --restore-all
在当前目录的 &quot;RECOVERED_FILES&quot; 下恢复恢复1293877800秒后的所有误删文件
Note: date -d &quot;Jan 01 18:30 2011&quot; +%s</pre><pre class='md-fences mock-cm' style='display:block;position:relative'>extundelete --help
用法: extundelete [选项] [--] 设备-文件
选项:
  --version, -[vV]       打印版本并且正常退出.
  --help,                打印帮助并且正常退出.
  --[superblock](http://baike.baidu.com/view/1102790.htm)           
                         除了剩余的内容之外，还打印超级块的内容。
                         默认选项
  --journal              显示日志内容
  --after dtime          只处理在 &#39;dtime&#39; 后被删除的条目
  --before dtime         只处理在 &#39;dtime&#39; 前被删除的条目
功能:
  --inode ino            显示 &#39;ino&#39; 的 索引节点 信息
  --block blk            显示 &#39;blk&#39; 的    块   信息
  --restore-inode ino[,ino,...]
                         恢复具有已知索引节点号 &#39;ino&#39;,
                         已恢复的文件在当前目录的RECOVERED_FILES文件夹里创建
                         而文件的索引节点号作为扩展(ie:file.12345)
  --restore-file &#39;path&#39;  将恢复文件 &#39;path&#39;. &#39;path&#39; 是相对于根分区而言的，并且不以 &#39;/&#39; 开头
                         已恢复的文件在当前目录的 &#39;RECOVERED_FILES/path&#39;.
  --restore-files &#39;path&#39; 列出将在 &#39;path&#39; 恢复的文件.
                         每个文件名格式应该与选项 --restore-file 相同，并且每行都应该有一个.
  --restore-directory &#39;path&#39;
                         恢复文件夹 &#39;path&#39;.
                         &#39;path&#39; 是相对于文件系统的根目录而言的.
                         已恢复的文件夹输出目录在&#39;path&#39;。
  --restore-all          尝试去恢复一切
  -j journal             从一个已命名的文件读取外部日志
  -b blocknumber         当打开系统文件时，使用一个块数字备份超级快.
  -B blocksize           当打开系统文件，使用 blocksize 作为一个块大小.
                         这个数字应该以 bytes 为单位.
  --log 0                程序静默执行
  --log filename         记录所有消息到文件.
  --log D1=0,D2=filename 自定义控制以逗号分隔的日志消息
示例如下:                 列出选项. Dn 必须是 info,warn 或者 error 中一个。
   --log info,error      略去 ‘=name’ 信息中的结果
   --log warn=0          将指定的级别记录到计算机控制台.如果变量为 &#39;=0&#39;,指定的级别记录将被关闭.
   --log error=filename  如果变量为&#39;=filename&#39;，写入具有该级别的消息到文件名.
   -o directory          保存恢复的文件到指定目录.
                         默认情况下，恢复的文件被创建在 &#39;RECOVERED_FILES&#39; 文件夹.</pre><h5><a name='header-c212' class='md-header-anchor '></a>3--&gt;过程</h5><h6><a name='header-c213' class='md-header-anchor '></a>	3.1 模拟故障</h6><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125173350159-1301898238.png" width="800px"></p><h6><a name='header-c216' class='md-header-anchor '></a>	3.2 故障恢复</h6><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170125192505972-1219673026.png" width="800px"></p><h5><a name='header-c219' class='md-header-anchor '></a>4 -&gt; 结果</h5><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170126104355300-329601232.png" width="800px"></p><h4><a name='header-c224' class='md-header-anchor '></a><a href='http://code.google.com/p/ext3grep/' target='_blank' title='去除'>ext3grep</a></h4><p><img style="vertical-align: middle;" src="http://images2015.cnblogs.com/blog/952608/201701/952608-20170126122707222-1732017307.png" width="800px"></p><p></p><h3><a name='header-c231' class='md-header-anchor '></a>三、综合展示</h3><table><thead><tr><th style='text-align:center;' >功能\名字</th><th style='text-align:center;' >Safecopy</th><th style='text-align:center;' >TestDisk</th><th style='text-align:center;' >PhotoRec</th><th style='text-align:center;' >ext3grep</th><th>extundelete</th></tr></thead><tbody><tr><td style='text-align:center;' >null</td><td style='text-align:center;' >null</td><td style='text-align:center;' >null</td><td style='text-align:center;' >null</td><td style='text-align:center;' >null</td><td>null</td></tr></tbody></table><pre class='md-fences mock-cm' style='display:block;position:relative'></pre></div>
</body>
</html>