---
cssclasses:
  - list-cards
  - cards 
  - cards-cols-3
template-version: "4.2.7"
note-type: source_note
aliases: []
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") -%>
<%*
let target = ""
let suggestionlist =["harrison","cecile","Robins","Catzung","article ","case-files","bates","web","Lawrence","Learning clinical reasoning","UpToDate", "Schwartz" , "Kaplan" , "Novel" , "other"];
let flag =  await tp.system.suggester(suggestionlist,suggestionlist)
tR+= "\nbook-name: " + flag
let defaultuse="true"
if (flag != "web")
{
	defaultuse= await tp.system.suggester(["Yes", "No"], ["true", "false"],true ,"would you like to use the default name for the PDF?")
}

let namefile=" "
if (defaultuse =="true")
{
	if (flag=="UpToDate"){
		namefile="iMD - Uptodate - " + tp.file.title +".pdf"
	}
	else{
		namefile = tp.file.title + ".pdf"
	}
}
else 
{
	if (flag=="UpToDate")
	{
		namefile1 = await tp.system.prompt("what is the name of the source, enter only the title of the article", " ")
		namefile="iMD - Uptodate - " + namefile1 +".pdf"
	}
	else
	{
		namefile=await tp.system.prompt("what is the name of the source", " ")
	}	
}
if (flag=="web")
{
	target = await tp.system.prompt("Enter the URL of the source", "")
	tR += "\nannotation-target: " + target + "\nannotation-target-type: web"
} 
else 
{
	tR += "\nannotation-target: " + namefile 
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
		exec1 = "false"
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
  const searchTerms = ["diagnos","imaging", "lab", "clinical", "risk", "treatment", "management", "therapy", "therapi", "physical", "etiology", "patho" , "symptom", "approach", "differential", "drugs","drug","agents"] 
  const response =[" diagnosis ", " imaging ", " Lab_eval ", " clinical_manifestation ", " risk_factors ", " treatment "," treatment "," treatment "," treatment ", " physical_exam ", " etiology "," pathogenesis "," clinical_manifestation " , " approach ", " Differential-Diagnosis ", " pharmacology ", " pharmacology "]
  for (let i = 0; i < searchTerms.length; i++)
   {
	    if (loweredStr.includes(searchTerms[i].toLowerCase()))
	    {
		    tR+=response[i] +", "
    
	    }
    }
-%>]
BC-link-note: Child 
---

> [!important links]  
<%*  
let exec = "true"  
if (flag=="web")  
{  
	tR+="> [link to source]("+target+")\n"  
	while (exec=="true" || exec=="PDF")  
	{  
		exec = await tp.system.suggester(["extracted-from", "related","Related PDF","nothing"], ["extracted-from", "related","PDF","nothing"],"nothing","do you want to add additional resources?")  
		if (exec=="PDF")  
		{  
			tR+= "> related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + ".pdf]]\n"  
		}  
		else if (exec == "related")  
		{  
			tR+= "> related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + "]]\n"  
		}  
		else if (exec == "extracted-from")  
		{  
			tR+= "> extracted-from::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + "]]\n"  
		}  
	}  
}  
else  
{  
	tR+="> link to pdf: [[" + namefile + "]]\n"  
	while (exec=="true" || exec=="PDF")  
	{  
		exec = await tp.system.suggester(["extracted-from", "related","Related PDF","nothing"], ["extracted-from", "related","PDF","nothing"],"nothing","do you want to add additional resources?")  
		if (exec=="PDF")  
		{  
			tR+= "> related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + ".pdf]]\n"  
		}  
		else if (exec == "related")  
		{  
			tR+= "> related::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + "]]\n"  
		}  
		else if (exec == "extracted-from")  
		{  
			tR+= "> extracted-from::[[" + (await tp.system.suggester((item) => item.basename, app.vault.getFiles())).basename + "]]\n"  
		}  
	}  
}  

-%>> link to excalidraw ->
