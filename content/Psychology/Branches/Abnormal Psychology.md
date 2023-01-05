---
title: "Abnormal Psychology"
---

#INFO/MOC #FIELD/Psych/Abnormal 

# Definition

<div style="padding: 15px; border: 1px solid transparent; border-color: transparent; margin-bottom: 20px; border-radius: 4px; color: #31708f; background-color: #d9edf7; border-color: #bce8f1;">
<em>Abnormal</em> psychology studies psychopathology and abnormal behavior
</div>



# Disorders

[[Mental Disorders]]
```dataview
Table

Category as "Category",
join(Concept) as "Related Concept",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Abnormal AND #INFO/Secondary/Classification
SORT length(file.inlinks) DESC
```

# Works in the Field

### Important Concepts

```dataview
Table

join(filter(Field, (x) => !contains(x, [[Social Psychology]]))) as "Related Fields",
join(Fact) as "Related Fact",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Abnormal AND #INFO/Concept 
SORT length(file.inlinks) DESC
```


### Important Sub-Concepts

```dataview
Table

join(Main) as "Parent Concept",
join(filter(file.etags, (x) => !contains(x, "#INFO") AND !contains(x, "#FIELD/Psych/Abnormal"))) as "Related Topic",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Abnormal  AND #INFO/Sub-Concept 
SORT length(file.inlinks) DESC
```

### Important Theories

```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
Year as "Year",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Abnormal AND #INFO/Primary/Theory
SORT length(file.inlinks) DESC
```

### Important Studies


```dataview
Table

join(Concept) as "Related Concept",
Psychologist as "Psychologist",
length(file.inlinks) as "🔗"

FROM #FIELD/Psych/Abnormal AND #INFO/Primary/Study
SORT length(file.inlinks) DESC
```
