```sql
/* 
Purpose: This script is to create a new joint formatted name of Person1 (alumni) and spouse using formula's provided
This script consists of 2 different table
 1. First table: This table consists of information regarding Person1 and spouse (like: Prefix, person1 first name and last name and spouse first name and last name)
 2. Second Table: This table consists of the new formatted name without the education flag
 3. Third Table: This table consists of the new formatted name with the education flag

	SOURCE TABLES:
		contact base
		elcn_education
		elcn_personname
		elcn_personalrelationship
		elcn_formattedname

	HISTORY:
		11/09/2021	Dikshya	Pandey created
		
*/

SELECT DISTINCT 
pn.prefixidName as person1prefix
, cb.ContactId
, cb.FirstName as Person1FirstName
, cb.LastName as Person1LastName
--, cb.MiddleName as Person1MiddleName
, pr.Person1IdName
, pn2.prefixidName as person2prefix
, cb2.ContactId as spouseID
, cb2.FirstName  as Person2FirstName
--, cb2.MiddleName as Person2MiddleName
, cb2.LastName as Person2LastName
, pr.Person2IdName
, fn.formattedname
, fn.formattednameId
, fn.typeidName
into #fulltable
FROM ContactBase cb 
INNER JOIN personname pn on pn.personid = cb.ContactId and pn.nametypeName = 'primary'
LEFT JOIN  personalrelationship pr on pr.Person1Id = cb.ContactId AND pr.statecode = 0 AND pr.statuscode =1
INNER JOIN formattedname fn on fn.personid = cb.ContactId
LEFT JOIN contactBase cb2 on pr.Person2Id = cb2.ContactId AND cb2.statecode = 0 AND cb2.statuscode =1
INNER JOIN personname pn2 on pr.Person2Id = pn2.personid and pn2.nametypeName = 'primary' 

WHERE typeidName IN ('Formal Joint Salutation')
AND pr.RelationshipType1IdName IN ('Spouse', 'Domestic Partner', 'Companion')
--AND lower(fn.formattedname) not like '%duplicate%' or lower(fn.formattedname) not like '% (test)'
AND cb.statecode = 0
AND cb.statuscode = 1
AND pn.statecode = 0 
AND pn.statuscode =1
AND fn.statecode = 0
AND fn.statuscode =1
AND pn2.statecode = 0 
AND pn2.statuscode =1
; 

--DROP TABLE IF EXISTS #fulltable


-- The code below is the new formatted name without the education flag

SELECT
 #fulltable.ContactId
, #fulltable.spouseID
, #fulltable.formattednameId
, #fulltable.person1prefix
, #fulltable.person2prefix
, #fulltable.Person1LastName
, #fulltable.Person2LastName
, #fulltable.Person1FirstName
, #fulltable.Person2FirstName
, #fulltable.formattedname
, #fulltable.typeidName


, CASE 
	   WHEN  #fulltable.Person1LastName = #fulltable.Person2LastName 
		AND #fulltable.person1prefix IS NOT NULL 
		AND #fulltable.person2prefix IS NOT NULL
			THEN  CONCAT(#fulltable.person1prefix,' ' , '&' , ' ',#fulltable.person2prefix, ' ', #fulltable.Person1LastName)
	   WHEN  #fulltable.Person1LastName <>  #fulltable.Person2LastName 
		AND #fulltable.person1prefix IS NOT NULL 
		AND #fulltable.person2prefix IS NOT NULL
			THEN CONCAT(#fulltable.person1prefix,' ', #fulltable.Person1LastName , ' ','&' , ' ', #fulltable.person2prefix, ' ',#fulltable.Person2LastName) 
	   WHEN #fulltable.person1prefix IS NULL 
		OR #fulltable.person2prefix IS NULL 
			THEN CONCAT (#fulltable.Person1FirstName,' ' ,'& ',' ',#fulltable.Person2FirstName )
	   END AS new_formattedname
into #newtb
FROM #fulltable ;

-- DROP TABLE IF EXISTS #newtb


-- SELECT * from #newtb

-- The code below is for creating the education flag for Person 1 and spouse and is the new formatted name with the education flag

SELECT DISTINCT ft.* 
, case when ed.PersonId IS NOT NULL then 1 else 0 end Person1flag
, case when ed2.PersonId IS NOT NULL then 1 else 0 end Spouseflag
, CASE 
		WHEN ed2.PersonId IS NOT NULL
		AND ed.PersonId IS NULL
		AND ft.person1prefix IS NOT NULL 
		AND ft.person2prefix IS NOT NULL
		AND ft.Person1LastName = ft.Person2LastName
			THEN  CONCAT(ft.person2prefix,' ' , '&' , ' ',ft.person1prefix, ' ', ft.Person2LastName)
		WHEN ed2.PersonId IS NOT NULL
		AND ed.PersonId IS NULL
		AND ft.person1prefix IS NOT NULL 
		AND ft.person2prefix IS NOT NULL
		AND  ft.Person1LastName <> ft.Person2LastName
			THEN CONCAT (ft.person2prefix,' ', ft.Person2LastName , ' ','&' , ' ', ft.person1prefix, ' ',ft.Person1LastName )
		WHEN ed2.PersonId IS NOT NULL
		AND ed.PersonId IS NULL
		AND ft.person1prefix IS  NULL 
	     OR ft.person2prefix IS NULL
			THEN CONCAT (ft.Person2FirstName,' ' ,'& ',' ',ft.Person1FirstName)
			ELSE ft.new_formattedname
	END AS FINAL_formattedname




from #newtb ft

LEFT JOIN education ed on ft.ContactId = ed.PersonId AND ed.InstitutionIdName = '**** University' AND ed.graduationstatusIdName = 'Completed' AND ed.statecode = 0 AND ed.statuscode = 1
LEFT JOIN education ed2 on ft.spouseID = ed2.PersonId AND ed2.InstitutionIdName = '**** University' AND ed2.graduationstatusIdName = 'Completed' AND ed2.statecode = 0 AND ed2.statuscode = 1
;
```
