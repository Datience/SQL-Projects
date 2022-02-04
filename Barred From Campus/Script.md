```sql
/* Purpose: This script is to review who ever has been Barred from Campus 
- Find out their Contact preferences and set them to No 
- We want to make sure we don't contact this person 

	SOURCE TABLES:
		elcn_businessrelationship
		elcn_contactpreference

	HISTORY:
		10/22/2021	Dikshya	Pandey created
		CRM last updated: 11/8/2021
*/

SELECT 
br.PersonId
,cp.contactpreferenceId
,br.PersonIdName
,br.OrganizationIdName
,br.BusinessRelationshipStatusIdName
,cp.ContactPreferenceTypeIdName

,CASE WHEN cp.appointment = 1 THEN 0 ELSE 0 END appointment
,CASE WHEN cp.Email  = 1 THEN 0 ELSE 0 END Email
,CASE WHEN cp.letter = 1 THEN 0 ELSE 0 END letter
,CASE WHEN cp.phone = 1 THEN 0 ELSE 0 END phone
,CASE WHEN cp.text = 1 THEN 0 ELSE 0 END text
--into #temptable
FROM businessrelationship br
LEFT JOIN contactpreference cp on cp.PersonId = br.PersonId
WHERE OrganizationIdName like '%Barred From Campus%'
AND br.statecode = 0 and br.statuscode = 1
AND businessRelationshipStatusIdName='Current'

-- DROP TABLE IF EXISTS #temptable

--Distinct Name of the people barred from campus
--select distinct #temptable.PersonIdName from #temptable
```
