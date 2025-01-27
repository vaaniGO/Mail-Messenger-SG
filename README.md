# Mail-Messenger-SG

The goal of the project is to create an automated 'events' calendar directly from assessing emails in a specific label in the user's gmail inbox. For example, if the user receives an event email for an event happening on a certain date and time, it should automatically be added to the events calender. There will be a listener connected to a specific label (this label can only contain emails for Clubs / Socs / Depts. etc. - essentially we can control what kind of emails we are considering in the first place) and, through the return of a JSON object as below, we will be able to add events to our calender. 

The tuple contains of two parts: True/False denoting if the email is corresponding to an event (True) else False. The second part, if the email is an event-email is a JSON object containing event detials, else it is an empty object. <br>
Example of a tuple of an email that does correspond to an 'event': <br>
True,{<br>
"Name of the event": "Political Science Colloquium 28 Jan | Violence as Craft: How Violence Shapes Voter Preferences",<br>
"Organising Body": ["Dept. of Political Science"],<br>
"Date, Time, Venue": {<br>
"Date": "2025-01-28",<br>
"Time": "1:45 to 3:00  P.M. (IST)",<br>
"Venue": "LR - AC-02-LR-003"<br>
},<br>
<br>
The task is to 
1. Distinguish a non-event email from an event email
2. In case it is True that the email corresponds to an event, we want a JSON object of a specified format containing relevant event details (these can be modified easily as well)
3. Account for changes in events by looking at thread emails and processing them correctly

The LLM and Script performs task 1 with 100% accuracy, and prompt improvement will help us achieve the maximum performance on tasks 2 and 3.

In the case where the email has multiple Reply emails (the email is a thread), the following algorithm is followed: 
1. If the message ID has 'references' then
2. Append the body of the current email to the 'body' variable with a disclaimer that it is a thread
3. The next email in the loop will be the 'reference' the previous email was talking about (because emails are traversed recent most to earliest in a thread by default)
4. Keep on appending the bodies of all subsequent thread emails till the end of the thread is reached
5. Pass the content to the LLM with the prompt as usual

Notes: 
1. We must run a variety of test-cases to see how we can prompt the LLM even better.

