# Week-01 [OWASP Rating Methodology](https://www.owasp.org/index.php/OWASP_Risk_Rating_Methodology)
## Explain The Two Sets of Factors: __Threat Agents__ and __Vulnerability__
### * Threat Agents:
A __Theat Agent__ is the source of your security concerns. The "Attackers" if you will
These can be anything from a group of malicious hackers to a well-meaning employee.
OWASP quantifies the level of a __Threat Agent__ with a number of options, each with likelihood rating of 0 to 9:

* Skill Level (1, 3, 5, 6 ,9): How technically skilled the TA is.
	* no technical skills (1)
	* some technical skills (3)
	* advanced computer user (5)
	* network and programming skills (6)
	* security penetration skills (9)
* Motive (1, 4, 9): How motivated is the threat agent to find and exploit a vuln?
	* low or no reward (1)
	* possible reward (4)
	* high reward (9)
* Oppertunity (0, 4, 7, 9): What resources and oppertunites are required for the threat agent to find and exploit a vuln?
	* full access or expensive resources required (0)
	* special access or resources required (4)
	* some access or resources required (7)
	* no access or resources required (9)
* Size (2, 2, 4, 5, 6, 9): How large is the group of threat agents?
	* internal devs (2)
	* internal sys-admin (2)
	* intranet users (4)
	* partners (5)
	* authenticated users (6)
	* anonymous internet users (9)

### * Vulnerability:
The goal here is to estimate the particular vuln involved being discovered or 
exploited assuming the __Threat Agent__ selected above.
		
Under OWASP, each __Vulnerability__ has 4 options with a likelyhood rating associated with them:
* Ease of discovery (1, 3, 7, 9): how easy is it for the __Threat Agent__ to disover this __Vulnerability__?
	* practically impossible (1)
	* difficult (3)
	* easy (7)
	* automated tools available (9)
* Ease of exploit (1, 3, 5, 9): how easy is it for the __Threat Agent__ to exploit this __Vulnerability__?
	* theoretical (1)
	* difficult (3)
	* easy (5)
	* automated tools available (9)
* Awareness (1, 4, 6, 9): How well known is this __Vulnerability__ to the __Threat Agent__?
	* unknown (1)
	* hidden (4)
	* obvious (6)
	* public knowledge (9)
* Intrusion detection (1, 3, 8, 9): How likely is an exploit to be detected?
	* active detection in app (1)
	* logged and reviewed (3)
	* logged without review (8)
	* not logged (9)

## Give examples of how you could change those parameters - for example for MySQL servers
1. Enabling and regularly reviewing logs would improve __Intrusion detection__, lowering the score from a 8 or 9 to a 3.
2. Making a __Vulnerability__ harder to exploit or lowering the possible effect of it on the rest of the system could lower the __Ease of exploit__ rating from a 5 to a 3 or 1. This could be done, for example, by increasing security tightness around your server, disabling remote root access, having secure user-groups etc.

## Explain how security risks are rated in OWASP
A security risk is rated using 2 factors: __Technical Impact__ and __Business Impact__.
The __Technical Impact__ is the traditional security areas of concern: confidentiality, integrity, availability and accountability.

### * __Technical Impact__: 
The goal is to estimate how heavily the system would be impacted.

* Loss of confidentiality (2, 6, 6, 7, 9): How much data could be disclosed and how sensitive is it?
	* minimal non-sensitive data disclosed (2)
	* minimal critical data disclosed (6)
	* extensive non-sensitive data disclosed (6)
	* extensive critical data disclosed (7)
	* all data disclosed (9)
* Loss of integrity (1, 3, 5, 7, 9): How much data could be corrupted and how damaged is it?
	* minimal slightly corrupt data (1)
	* minimal seriously corrupt data (3)
	* extensive slightly corrupt data (5)
	* extensive seriously corrupt data (7)
	* all data totally corrupt (9)
* Loss of availability (1, 5, 5, 7, 9): How much service could be lost and how v ital is it?
	* minimal secondary services interrupted (1)
	* minimal primary services interrupted (5)
	* extensive secondry services interrupted (5)
	* extensive primary services interrupted (7)
	* all services completely lost (9)
* Loss of accountability (1, 7, 9): Are the __Threat Agents__' actions tracable to an individual?
	* fully tracable (1)
	* possibly tracable (7)
	* completely anonymous (9)

### * __Business Impact__: The business impact stems from the technical impact, but requires a deep understanding of what is important to the company.
These options and ratings quantify how much damage the business would take in case of a technical breach.

* Financial damage (1, 3, 7, 9): How much financial damage will result from the exploit:
	* less than the cost to fix the __Vulnerability__ (1)
	* minor effect on annual profit (3)
	* significant effect on annual profit (7)
	* bankruptcy (9)
* Reputation damage (1, 4, 5, 9): Would an exploit result in reputational damage with harm to the business?
	* minimal damage (1)
	* loss of major accounts (4)
	* loss of goodwill (5)
	* brand damage (9)
* non-compliance (2, 5, 7): How much exposure does non-compliance introduce?
	* minor violation (2)
	* clear violation (5)
	* high profile violation (7)
* Privacy violation (3, 5, 7, 9): How much personally identifiable info would be disclosed?
	* one individual (3)
	* hundreds of people (5)
	* thousands of people (7)
	* millions of people (9)

## Argue whether OWASP gives a complete picture of security risks on an application:
I don't think it does; it is too general.
While it might help greatly in giving an overview of what could be lost or how serious a possible attack would be, it wont deal with the specifics of the given companies problem, or with unforseeable events. 
For example, the OWASP rating has no way of quantifying an exploit or threat agent that is not known the the company already. 
As such, there might be exploits or threat agents that don't factor in to their final rating.
		
