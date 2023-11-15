<%*  

let words = tp.file.title.split(' ');  
  for (let i = 0; i < words.length; i++) {  
	words[i] = words[i].toLowerCase();  
	words[i] = words[i].charAt(0).toUpperCase() + words[i].slice(1);  
  }  
await tp.file.rename(words.join(' '))  
-%>
