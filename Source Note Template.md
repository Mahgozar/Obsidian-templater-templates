%%this is a template for loading specific PDFs, often a chapter from a book, the book-name field can be simply Article to indicate that its not a pdf from a book. note that the pdf should be in the attachments folder and it should have the same name as your note. this template uses the annotator plugin for loading pdfs. it also uses the breadcrumbs note to make any source note as an MOC%%
---
page-count: <% await tp.system.prompt("how many pages?", " ") %>
template-version: 3.8
note-type: source_note
aliases: []
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
book-name: <% await tp.system.suggester([comma seperated list of books and different sources you might want to use],[comma seperated list of books and different sources you might want to use]) %>
annotation-target: '<% tp.file.title %>.pdf'
read: false
broken-down: false
linked-up: false
%%the scrpit for tags uses a dictionary of search terms to automatically tag stuff from your note's name%%
tags: [source <%* 
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
status: undone 
BC-link-note: extracted-from
---

%%  
link to pdf: [[<% tp.file.title %>.pdf ]] open note in new tab: [[<% tp.file.title %>]]  
%% 

<%*  
let exec = "true"  
while (exec=="true" || exec=="PDF")  
{  
	exec = await tp.system.suggester(["Yes", "No","YES PDF"], ["true", "false","PDF"],false ,"do you want to add additional resources?")  
	if (exec=="PDF")  
	{  
		tR+= "related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + ".pdf]]\n"  
	}  
	else if (exec == "true")  
	{  
		tR+= "related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + "]]\n"  
	}  
}  
%>
