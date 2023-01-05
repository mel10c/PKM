---
title: "Cognitive Psychology"
---

#INFO/MOC #FIELD/Psych/Cog

# Definition

<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
<em>Cognitive</em> psychology studies how people think and learn
</div>

- Focus on **memory** (remember & forget), **language** (speak, read, write); **attention**, **problems solving**, **decisions making**

# Works in the Field



### Important Concepts

```dataview
Table

join(filter(Field, (x) => !contains(x, [[Social Psychology]]))) as "Related Fields",
join(Fact) as "Related Fact",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Cog AND #INFO/Concept 
SORT length(file.inlinks) DESC
```


### Important Sub-Concepts

```dataview
Table

join(Main) as "Parent Concept",
join(filter(file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Neuro"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Cog AND #INFO/Sub-Concept 
SORT length(file.inlinks) DESC
```


### Important Phenomenon

```dataview
Table

join(Concept) as "Related Concept",
join(Study) as "Related Study",
join(filter( file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Cog"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Cog AND #INFO/Primary/Phenomenon  
SORT length(file.inlinks) DESC
```


### Important Theories

```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
Year as "Year",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Cog AND #INFO/Primary/Theory
SORT length(file.inlinks) DESC
```

### Important Studies


```dataview
Table

join(Theory) as "Related Theory",
join(Concept) as "Related Concept",
Psychologist as "Psychologist",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Cog AND #INFO/Primary/Study
SORT length(file.inlinks) DESC
```
