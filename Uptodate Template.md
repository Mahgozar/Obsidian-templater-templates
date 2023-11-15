---
cssclasses:
  - list-cards
  - cards
page-count: <% await tp.system.prompt("how many pages?", " ") %>
template-version: 3.9.5
note-type: source_note
aliases: []
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
book-name: UpToDate
link: "<% await tp.system.prompt("what is the URL", "") %>"
annotation-target: '<% tp.file.title %> - UpToDate.pdf'
<%*  
let exec1 = "true"  
while (exec1=="true")  
{  
	exec1 = await tp.system.suggester(["Yes", "No"], ["true", "false"],false ,"do you want to change the initial status of this source?(read, broken down or linked up)")  
	if (exec1=="true")  
	{  
		read = await tp.system.suggester(["Yes", "No"], ["true", "false"],false ,"have you already read this source?")
		tR+= "read: " + read + "\n"
		broken = await tp.system.suggester(["Yes", "No"], ["true", "false"],false ,"have you already broken down this sourcce?")
		tR+= "broken-down: " + broken + "\n"
	}  
	else 
	{  
		tR+= "read: false\nbroken-down: false\n"
	}  
}  
%>
tags: [source <%* 
  tR+= tp.file.folder() + "  "
  const loweredStr = tp.file.title.toLowerCase();
  const matchingElements = [];
  const searchTerms = ["diagnos","imaging", "lab", "clinical", "risk", "treatment", "management", "therapy", "therapi", "physical", "etiology", "patho" , "symptom", "approach", "differential"] 
  const response =[" diagnosis ", " imaging ", " Lab_eval ", " clinical_manifestation ", " risk_factors ", " treatment "," treatment "," treatment "," treatment ", " physical_exam ", " etiology "," pathogenesis "," clinical_manifestation " , " approach ", " Differential-Diagnosis "]
  for (let i = 0; i < searchTerms.length; i++)
   {
	    if (loweredStr.includes(searchTerms[i].toLowerCase()))
	    {
		    tR+=response[i]
    
	    }
    }
%>]
BC-link-note: Child 
---

```ad-example
title: Important links

link to pdf: [[<% tp.file.title %> - UpToDate.pdf]]
open note in new tab: [[<% tp.file.title %>]]  

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
-%>
```


