---
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
tags: daily 
note-type: daily 
exercise: 
running: 
---

%%links  
[[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>|yesterday]]  
[[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>|tomorrow]]  
%%

# Note to Self

# Dashboard

## Random Note of the Day
%%this section loads 5 random notes and some notes that you've marked as to_read so you can see and be reminded of them every day%%
```ad-important
title: to read
collapse: open
```dataview
LIST
FROM #to_read
```

<%*
const noOfNotes = 5
const dv = this.DataviewAPI
const files = await dv.tryQuery(`
  LIST
  FROM "specifiy the folders you want to choose your random notes from"
`)

let randomList = []

for (let i = 0; i < noOfNotes; i++) {
  const random = Math.floor(Math.random() *
                            (files.values.length - 1))
  randomList.push(files.values[random])
}

tR += dv.markdownList(randomList)
%>
## Other Dashboards 


```ad-important
title: Notes created Today
collapse: closed
```dataview
table 
	file.cday as "created date"  
WHERE file.cday=date(<% tp.file.creation_date("YYYY-MM-DD") %>)
SORT file.cday DESC 
```

```ad-important
title: Notes modified Today
collapse: closed
```dataview
table 
	file.mday as "modified date"  
WHERE file.mday=date(<% tp.file.creation_date("YYYY-MM-DD") %>)
SORT file.mday DESC 
```

