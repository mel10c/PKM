---
title: "Social Psychology"
---

#INFO/MOC #FIELD/Psych/Social

# Definition

<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
<em>Social</em> psychology studies feelings, thoughts, and behaviours of individuals in social situations
</div>

- Studies the **power of the situation**

# Works in the Field


### Important Concepts

```dataview
Table

join(filter(Field, (x) => !contains(x, [[Social Psychology]]))) as "Related Fields",
join(Fact) as "Related Fact",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Social AND #INFO/Concept 
SORT length(file.inlinks) DESC
```


### Important Sub-Concepts

```dataview
Table

join(Main) as "Parent Concept",
join(filter(file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Neuro"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Social  AND #INFO/Sub-Concept 
SORT length(file.inlinks) DESC
```

### Important Phenomenon

```dataview
Table

join(Concept) as "Related Concept",
join(filter( file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Social"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Social AND #INFO/Primary/Phenomenon  
SORT length(file.inlinks) DESC
```


### Important Theories

```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
Year as "Year",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Social AND #INFO/Primary/Theory
SORT length(file.inlinks) DESC
```

### Important Studies


```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Social AND #INFO/Primary/Study
SORT length(file.inlinks) DESC
```
