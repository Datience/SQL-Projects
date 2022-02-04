# Formatted Name

This script was written to create a new joint formatted name of Alumni's and their spouse using the formulas provided below. Then, update the CRM. The reason behind creating new joint formatted name was to ensure that all the alumni's and their spouse have correct names in the mail they receive. 

### Formula: 

1. If Person1 has no spouse, but has a set prefix in the dataset -> ##"Prefix"## + "Last Name"

2. If Person1 has spouse, both have set prefixes and have the same last name in the dataset -> "Prefix" & (Spouse) "Prefix" + (Spouse) "Last Name"

3. If Person1 has spouse, both have set prefixes but have different last name in the dataset -> "Prefix" + "Last Name" & (Spouse) "Prefix" + (Spouse) "Last Name"

4. If Person1 has spouse, but only 1 or none have set prefix in the dataset -> "First Name" & (Spouse) "First Name"

5. If Person1 has no spouse and no set prefix -> "First Name"

This script consists of 2 different table

- First table: This table consists of information regarding Person1 and spouse (like: Prefix, person1 first name and last name and spouse first name and last name)

- Second Table: This table consists of the new formatted name without the education flag*

- Third Table: This table consists of the new formatted name with the education flag*

This information is then used to update our CRM.

*Eudcation Flag: Education flag is set to check is Person1 is alumni or not. If alumni, the alumni's prefix and name should come before the spouse
