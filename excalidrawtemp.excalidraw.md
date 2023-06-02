---
template-version: 1.1
excalidraw-plugin: parsed
tags: [excalidraw]
status: new
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==
javascript
%%
<% await tp.file.rename( await tp.system.prompt("name the drawing", "be atomic")+".excalidraw" ) %>
extracted-from::[[<% (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles())).basename %>]]
%%
%%
# Drawing
```json
{"type":"excalidraw","version":2,"source":"https://excalidraw.com","elements":[],"appState":{"theme":"light","gridSize":null,"viewBackgroundColor":"black"}}
```
%%