---
cssclasses:
  - list-cards
  - cards 
template-version: "4.1.8"
note-type: source_note
aliases: []
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") -%>
<%*
let target = ""
let flag =  await tp.system.suggester(["harrison","cecile","Robins","Catzung","article ","case-files","bates", "web","Lawrence","Learning clinical reasoning","other "],["harrison","cecile","Robins","Catzung","article ","case-files","bates","web","Lawrence","Learning clinical reasoning","UpToDate","other"])
tR+= "\nbook-name: " + flag
if (flag=="web")
{
	target = await tp.system.prompt("Enter the URL of the source", "")
	tR += "\nannotation-target: " + target + "\nannotation-target-type: web"
} 
else if (flag=="UpToDate")
{
	tR+="\nlink: " + await tp.system.prompt("what is the URL", "") 
	tR+="\nannotation-target: "+ tp.file.title + " - UpToDate.pdf"
	tR+="\npage-count: "+ await tp.system.prompt("how many pages?", " ")
} 
else
{
	tR+="\nannotation-target: "+tp.file.title+".pdf"
	tR+="\npage-count: "+ await tp.system.prompt("how many pages?", " ")
}
tR+="\n"
-%>
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
-%>
tags: [source, <%* 
  tR+= tp.file.folder() + "  "
  const loweredStr = tp.file.title.toLowerCase();
  const matchingElements = [];
  const searchTerms = ["diagnos","imaging", "lab", "clinical", "risk", "treatment", "management", "therapy", "therapi", "physical", "etiology", "patho" , "symptom", "approach", "differential"] 
  const response =[" diagnosis ", " imaging ", " Lab_eval ", " clinical_manifestation ", " risk_factors ", " treatment "," treatment "," treatment "," treatment ", " physical_exam ", " etiology "," pathogenesis "," clinical_manifestation " , " approach ", " Differential-Diagnosis "]
  for (let i = 0; i < searchTerms.length; i++)
   {
	    if (loweredStr.includes(searchTerms[i].toLowerCase()))
	    {
		    tR+=response[i] +", "
    
	    }
    }
-%>]
BC-link-note: Child 
undone-part: all of it
---

```ad-example
title: Important links
<%* 
tR+="\n"
let exec = "true"  
if (flag=="web")
{
	tR+="[link to source]("+target+")\n"
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
}
else 
{
	tR+="link to pdf: [["+tp.file.title+".pdf ]]\nopen note in new tab [["+tp.file.title+"]]\n"  
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
}	  
%>
```
