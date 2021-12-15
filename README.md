# SQL-Projects

These are the SQL queries I have written:

1. Formatted Name:

This script was written to create a new joint formatted name of Person1 and their spouse using the formulas provided: 

Formula: 
If Person1 has no spouse, but has a set prefix in the dataset  -> 	"Prefix" + "Last Name"	
If Person1 has spouse, both have set prefixes and have the same last name in the dataset	-> "Prefix"	&	(Spouse) "Prefix" + (Spouse) "Last Name"
If Person1 has spouse, both have set prefixes	but have different last name in the dataset -> "Prefix" + "Last Name"	&	(Spouse) "Prefix" + (Spouse) "Last Name"
If Person1 has spouse, but only 1 or none have set prefix in the dataset ->	"First Name"	&	(Spouse) "First Name"
If Person1 has no spouse and no set prefix -> 	"First Name"


This script consists of 2 different table
 1. First table: This table consists of information regarding Person1 and spouse (like: Prefix, person1 first name and last name and spouse first name and last name)
 2. Second Table: This table consists of the new formatted name without the education flag*
 3. Third Table: This table consists of the new formatted name with the education flag*

This information is then used to update our CRM. 

*Eudcation Flag: Education flag is set to check is Person1 is alumni or not. If alumni, the alumni's prefix and name should come before the spouse

2. Barred From Campus:

This script was written to get all the people that were barred from campus from the dataset. The purpose of this query was to get "do not contact" list, to make sure we never contact them through mail, email, and remove them from all subscriptions. 

This information is then used to update our CRM, therefore setting all their contact preferences to 'No' . 

 
