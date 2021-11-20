# SQL-Projects

These are the SQL queries I have written:

1. Formatted Name:

This script is to create a new joint formatted name of Person1 and spouse using the formulas provided: 

This script consists of 2 different table
 1. First table: This table consists of information regarding Person1 and spouse (like: Prefix, person1 first name and last name and spouse first name and last name)
 2. Second Table: This table consists of the new formatted name without the education flag*
 3. Third Table: This table consists of the new formatted name with the education flag*

Formula: 
If ID has no spouse, has prefix -> 	"Prefix" + "Last Name"	
If ID has spouse, both have prefixes and with same last name	-> "Prefix"	&	(Spouse) "Prefix" + (Spouse) "Last Name"
If ID has spouse, both have prefixes	-> "Prefix" + "Last Name"	&	(Spouse) "Prefix" + (Spouse) "Last Name"
If ID has spouse, but only 1 or none have prefix ->	"First Name"	&	(Spouse) "First Name"
If ID has no spouse and no prefix -> 	"First Name"

This information is then used to update our CRM. 

*Eudcation Flag: The alumni's prefix and name should come before the spouse

2. Barred From Campus:

This script is to get all the people that were barred from campus. We want to make sure to never contact them, therefore, with this query I change all their contact preferences to 'No' and update the information in the CRM.
 
