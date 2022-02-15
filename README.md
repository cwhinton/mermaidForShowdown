# mermaidForShowdown
My take on a mermaid extension for showdown

I use this to create Markdown based documentation that renders entirely in the browser, not requiring a Mermaid-enabled Markdown server.  Each page stands alone.

## Use
This does of course require a browser friendly (not a simple local file system) to host the extension file.

A single HTML document with Markdown and Mermaid is constructed as such:

```
<html>
<head>
<script src="https://unpkg.com/showdown/dist/showdown.min.js"></script>
<script src="https://unpkg.com/mermaid/dist/mermaid.min.js"></script>
<script type="text/javascript" src="https://myhostingurl.here/mermaidForShowdown.js"></script>
</head>
<body>
<div id="markdown">
# Markdown text here
Some mermaid
::: mermaid
	flowchart TD
	id1([Thing1])
	id2([Thing2])
	id3[[Thing3]]
	id4[[Thing4]]
	id5([Thing5])
	id6([Thing6])
	id1 <--> id3 <--> id5
	id2 --> id6 --> id4 --> id5
:::
</div>
<script>
	var target = document.getElementById('markdown'),
	converter = new showdown.Converter({extensions:['mermaid']});
	converter.setOption('tables','true');
	converter.setOption('strikethrough','true');
	var text = document.getElementById('markdown').innerHTML;
	var html = converter.makeHtml(text);
	target.innerHTML = html;
</script>
<script>
    mermaid.initialize({
      startOnLoad: true,
	  logLevel: 2
    });
  </script>
</body>
</html>
```
