# Rådata fra State of frontend

## Kolonne-beskrivelse

Det er tre kolonner som heter "Frontend teknologi"
1. Hvilken frontend teknologi bruker du nå
2. Hvilken frontend teknologi ser du for deg at du bruker i ditt neste prosjekt
3. Hvilken frontend teknologi bruker du på ditt hobbyprosjekt

## Nyttige queries

Hvor godt synes du teknolgien passer
```sql
-- Hvor godt synes vi teknologien passer?
select DISTINCT ans."Frontend teknologi_8", 
	round((select 
		sum(a."Hvor godt synes du denne frontend-teknologien passer i ditt nåværende prosjekt")/(select count(b."Frontend teknologi_8")*1.0
		from answers b  where b."Frontend teknologi_8" = ans."Frontend teknologi_8"  
		group by b."Frontend teknologi_8") as snitt from answers a 
		where a."Frontend teknologi_8" = ans."Frontend teknologi_8"
	), 2) as snitt,
	(select count(c."Frontend teknologi_8") from answers c where c."Frontend teknologi_8" = ans."Frontend teknologi_8"  group by c."Frontend teknologi_8") as antall_stemmer
from answers ans where antall_stemmer > 3 order by snitt desc;
```
