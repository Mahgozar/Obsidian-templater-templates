---
template-version: 3.0.1
aliases: [<% await tp.system.prompt("are there any aliases for this note?", " ") %>]
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
tags: [<%* 
  tR+= tp.file.folder() + "  "
  const loweredStr = tp.file.title.toLowerCase();
  const matchingElements = [];
  const searchTerms = ["diagnos","imaging", "lab", "clinical", "risk", "treatment", "management", "therapy", "therapi", "physical", "etiology", "patho" , "symptom", "approach", "differential", "ECG", "EKG", "electrocardiography"] 
  const response =[" diagnosis ", " imaging ", " Lab_eval ", " clinical_manifestation ", " risk_factors ", " treatment "," treatment "," treatment "," treatment ", " physical_exam ", " etiology "," pathogenesis "," clinical_manifestation " , " approach ", " Differential-Diagnosis "," EKG "," EKG "," EKG "]
  for (let i = 0; i < searchTerms.length; i++)
   {
	    if (loweredStr.includes(searchTerms[i].toLowerCase()))
	    {
		    tR+=response[i]
    
	    }
    }
%>]
note-type: default
cssclasses:
  - list-cards
  - cards
---

<%*  
const exec = await tp.system.suggester(["Yes", "No"], [true, false],false ,"is this file extracted from anything else?")  
if (exec==true)  
{  
  tR+=("extracted-from::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles())).basename + "]]")  
}  
-%>
