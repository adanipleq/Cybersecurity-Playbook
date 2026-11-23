Weeks 4–5 Professional Practice Record
Name: Ada Niple
Vendor activity: 4.2-4.3 Data and Tools in netacad
Evidence link:  https://www.netacad.com/launch?id=249e41f9-9676-4d51-818b-67ab8e09ee5f&tab=curriculum&view=12d2ab6a-4fa0-4adc-93e7-ca73d8fee3a1
1. Preparation
What did you review or prepare before the activity? Include a date or a small piece of evidence if you have one.
Before theBefore the “Infected” activity, I predicted that the wineventlog sourcetype would help locate antivirus events. I recorded this prediction in my Activity 4.3 notes.
2. Evidence record
Name the tool or device, what you searched or reviewed, and what you observed. Say whether you ran the search yourself or reviewed supplied results.
 My evidence is the supplied Cisco Networking Academy/Splunk views; I did not run the search myself. The walkthrough started with sourcetype=wineventlog, then narrowed to source="WinEventLog:Application" and SourceName="Symantec AntiVirus". The views showed 18 matching events and five host summary rows.

3. Feedback and revision
The walkthrough showed me that naming the wineventlog sourcetype wasn’t enough to explain how the results were narrowed. I revised my notes to include the Application log source and antivirus provider.

Before:  “Use the wineventlog sourcetype to find what is needed.”

After:  “Start with sourcetype=wineventlog, narrow to the Application log source, then select the Symantec AntiVirus provider. The final view groups distinct messages by host.”

Why the revision helps:  This revision gives another analyst a clearer search path and helps prevent interpreting five host rows as five infections.

4. Follow-through and AI use
What improvement did you carry forward? If you used ChatGPT Edu, say how you checked its suggestions.
I followed through by explaining what the grouped results can and cannot show. I also identified a next step: compare the event timestamps and action results with endpoint process logs for the same hosts.
I did use AI. I checked my work with ChatGPT Edu and organized my submission for this assignment with it. ChatGPT helped organize and simplify my record. I checked the details against my saved Activity 4.3 notes. I did not use AI to run or verify a Splunk search.

Feedback: I could not get a peer to review my work.
