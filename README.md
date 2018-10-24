# Codepath-assignment-8

Blue site:
Exploit 1: Session Hijacking
The blue site uses a single PHP session id parameter to verify the user's session. 
If a hacker has that session ID, they can inject it into the parameter 
and get into the site's staff section even if they didn't log on with a user name and password.
Here, we attempt to get into the site first simply by going to the staff index's HTML address.
This fails, yielding a redirect to login. 
However, we send this failed request to the repeater in Burp.
There, we inject a session ID from a user logged in in another browser.
The resulting response gets us into the staff menu.

Exploit 2:



Questions:
Which attacks were easiest to execute? Which were the most difficult?
SQL injection and cross site scripting were relatively easy -- 
they can be done right on the page or in the address bar.
CSRF and session hijacking were more difficult, or at least more time-consuming,
as they require some leg work away from the page itself.

What is a good rule of thumb which would prevent accidentally username enumeration vulnerabilities 
like the one created here?

Don't have the page display something different for different kinds of failed logins!

Since you should be somewhat familiar with the CMS and how it was coded, 
can you think of another resource which could be made vulnerable to an 
Insecure Direct Object Reference? What code could be removed which would expose it? 
(Hint: It was also the answer to the first bonus objective to the Weekly Assignment for week 3.)

Yes, login could also be made vulnerable to IDOR if the POST request for login relies on 
tokens that are simply encoded versions of the user name.

Many SQL Injections use OR as part of the injected code. 
(For example: ' OR 1=1 --'.) Could AND work just as well in place of OR? 
(For example: ' AND 1=1 --'.) Why or why not?

No. The idea is that a logical OR returns all the records where either of the query parameters are true.
OR 1=1 is useful because 1=1 is always true, and a query with it will therefore return _all the records_.
AND 1=1 checks to ensure both 1=1 and the original query are true, and will therefore likely only 
return one record.

A stored XSS attack requires patience because it could be stored for months before being triggered. 
Because of this, what important ingredient would an attacker most likely include in a stored XSS attack script?

Code that adjusts any parameters that rely on a timer, i.e. if there were any CSRF components those would need
to be adjusted

Imagine that one of your classmates is an authorized admin for the site's CMS and you are not. 
How would you get them to visit the self-submitting, hidden form page you created in Objective #5 (CSRF)?

A convincing email that appears to be a warning of an attack requiring immediate action: Go to 
this page to resolve the security issue.

Compare session hijacking and session fixation. 
Which attack do you think is easier for an attacker to execute? 
Why? One of them is much easier to defend against than the other. 
Which one and why?

Session hijacking steals an existing session cookie, session fixation injects a cookie that the victim then uses.
The latter is harder to execute because it relies on having access to the target's browser.
However, it's also harder to protect against, because session timeout won't necessarily stop it
