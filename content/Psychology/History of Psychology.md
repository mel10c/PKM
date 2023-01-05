---
title: "History of Psychology"
---

#INFO/Secondary #FIELD/Psych [Full Timeline of Psychology](https://en.wikipedia.org/wiki/Timeline_of_psychology)

# Timeline


```dataview
Table

Year as "Year",
Psychologist as "Psychologist", 
join(filter( file.etags, (x) => !contains(x, "#INFO"))) as "Other Fields"

FROM #FIELD/Psych AND #INFO/Primary/Theory 
SORT Year
```
