---
created: 2024-09-26T08:35
updated: 2024-09-26T08:35
---
# What is it? 
A tracker that second time around moms can take inventory of what they already have for baby number two and easily access that information from a web app 

Other useful versions [[kids closet]] [[minimalist closet]]


## The problem: 
I have things from my first child that I can use again with my second. The problem is that I have no idea what I have down in the basement. I would like to get an inventory for what is there and be able to categorize everything visually rather than keep this information in my head or on a notebook somewhere. 

## The solution: 
A web app that allows you to inventory your baby clothes based on gender, weather, and size. 

Will have three views: 
1. a landing page where you can play with the tracker to show on my portfolio as well as to my family as a baby announcement.
2. Behind a sign in wall, users can track their own information 
3. Behind a sign in wall, users can download a file with their information 

User Stories: 
1. As an expecting mom, I want to know how many I have of the following clothes:
	 - long sleeve onsies
	 - short sleeve onsies
	 - full body "pyjamas"
	 - pants 
	 - tops
	 - Weather dependent stuff like jackets, swim suits, etc
	 - pregnancy clothes! 
1. I want to take inventory of the following gear:
	-  pump
	- bed sheets
	- matress/crib
	- baby bath
	- burp cloths
	- nursing bras
	- etc	
1. I want to be able to specify "for every day" and "for special occasion" for an item, with the default being "for every day".
2. I want to pick a default gender for the clothes I already have as "girl", "boy", "neutral" with a one click button to change the gender for a specific item. 
3. I want to be able to see my inventory at a glance
4. I want to be able to print my inventory
5. I want this to work on mobile and desktop 

For the database, it can just be clothes table. Loop through table x times and add new data. If there are changes, add that type or ENUM 

~~Check out [[vaadin]] for front end? Uses Java~~ 
Use [[react]] for front end because it is so in demand 