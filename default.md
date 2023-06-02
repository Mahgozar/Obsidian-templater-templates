---
template-version: 3.0
aliases: [<% await tp.system.prompt("are there any aliases for this note?", " ") %>]
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
%%the scrpit for tags uses a dictionary of search terms to automatically tag stuff from your note's name%%
tags: [<%* 
  tR+= tp.file.folder() + "  "
  const loweredStr = tp.file.title.toLowerCase();
  const matchingElements = [];
  const searchTerms = [key words to look for in your note's name should come in a comma seperated list here] 
  const response =[" tag1 ", " tag2 " note the spaces around each tag they should be there so the tags are properly seperated]
  for (let i = 0; i < searchTerms.length; i++)
   {
	    if (loweredStr.includes(searchTerms[i].toLowerCase()))
	    {
		    tR+=response[i]
    
	    }
    }
%>]
note-type: default
linked-up: false
---

<%*  
const exec = await tp.system.suggester(["Yes", "No"], [true, false],false ,"is this file extracted from anything else?")  
if (exec==true)  
{  
  tR+=("extracted-from::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles())).basename + "]]")  
}  
-%>
