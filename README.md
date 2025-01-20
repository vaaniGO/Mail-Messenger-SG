# Mail-Messenger-SG

The goal of the project is to create an automated 'events' calendar for a user directly from assessing emails in a specific label in the user's gmail inbox. For example, if the user receives an event email for an event happening on a certain date and time, it should automatically be added to the events calender. The task is to 
1. Distinguish a non-event email from an event email
2. In case it is True that the email corresponds to an event, we want a JSON object of a specified format containing relevant event details (these can be modified easily as well)

The LLM and Script perform the above two tasks with 100% accuracy. 

In the case where the email has multiple Reply emails (the email is a thread), the following algorithm is followed: 
1. If the message ID has duplicates the message ID array, then
2. Find all messages with the same ID
3. Concatenate them giving appropriate disclaimer that they are follow up and reply emails and just build onto the original one (original = one with earliest timestamp)
4. Pass this compact string to the LLM to identify the latest event details

Notes: 
1. To make this process efficient, we must only begin searching / looping emails after a certain timestamp (current - 1 day) or something. Because otherwise, every 60 seconds, ALL emails in the label are fetched and unnecessarily processed again.

