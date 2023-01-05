---
title: "Biological Psychology"
---

#INFO/MOC #FIELD/Psych/Neuro

# Definition

<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
<em>Biological</em> psychology studies sensations and perceptions of human being. Also includes thoughts from the evolutionary perspective
</div>

- Studies the [[Sensation]] and [[Perception]]

# Works in the Field


### Important Concepts

```dataview
Table

join(filter(Field, (x) => !contains(x, [[Social Psychology]]))) as "Related Fields",
join(Fact) as "Related Facts",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Neuro AND #INFO/Concept
SORT length(file.inlinks) DESC
```

### Important Sub-Concepts

```dataview
Table

join(Main) as "Related Fields",
join(filter(file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Neuro"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Neuro AND #INFO/Sub-Concept
SORT length(file.inlinks) DESC
```


### Important Phenomenon

```dataview
Table

join(Concept) as "Related Concept",
join(Study) as "Related Study",
join(filter( file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Neuro"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Neuro AND #INFO/Primary/Phenomenon
SORT length(file.inlinks) DESC
```


### Important Theories

```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
Year as "Year",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Neuro AND #INFO/Primary/Theory
SORT length(file.inlinks) DESC
```

### Important Studies


```dataview
Table

join(Theory) as "Related Theory",
join(Concept) as "Related Concept",
Psychologist as "Psychologist",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Neuro AND #INFO/Primary/Study
SORT length(file.inlinks) DESC
```
