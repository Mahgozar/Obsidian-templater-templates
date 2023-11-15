---
creation date: <% tp.file.creation_date() %>
modification date: 2023-11-13T12:49:02+03:30
tags:
  - daily
note-type: daily
template version: 3.1.5
cssclasses:
  - cards
  - cards-cover
  - cards-2-3
  - table-max
  - list-cards
---
```ad-example
title: Relevant Links 
- [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>|yesterday]]
- [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>|tomorrow]]
- [[<%tp.file.title%>#Dashboard|Dashboards]]
%%
```

# Note to Self

# Dashboard
## Currently Reading

```dataview
table without id 
	cover  as Cover,
	file.link as Title,
	string(publish) as Year, 
	"by " + author as author,
	"⭐ " + rating as "⭐ rating",
	status as "status"
from #to_read
where cover != null and cover != "{{coverUrl}}"
```
## Read 
```dataview
table without id 
	cover as Cover,
	file.link as Title,
	string(publish) as Year, 
	"by " + author as author,
	"⭐ " + rating as "⭐ rating",
	status as "status"
from #book
where cover != null and cover != "{{coverUrl}}"
```
## Movie list 
```dataview
table without id 
	("![](" + poster + ")") as Poster,
	file.link as Title,
	string(year) as Year, 
	"by " + director as Director,
	"⭐ " + scoreImdb as "⭐ IMDB",
	rating,
	watched
from #movies 
where poster != null and poster != "{{VALUE:Poster}}"
```

## Notes created and modified 
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


