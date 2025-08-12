
# 🌱 Culture of Innovation: ACT Active Customer 360 Meeting

Date: Aug 4, 2022
Time: 08:32
Attendees: Jacob D. Lynda L. Ryan R. __Rob Th.__ __Kartik P__

---

# Goals / agenda
1. How is my customer doing?
2. 

# Discussion notes
- Every org in business is responsible for customer health
- With ACT, combo of customer health and customer sentiment
	- gives report card for every customer
		1. config. scorecard
			1. based on 90-day data
		2. near realtime data
		3. multi dimensional
		4. one click health report
		5. customer sentiment 
	- MA score and Customer Sentiment score [can be same or vary]

## Architecture
- Uses Google Cloud Platform 
- Limited usage
	- still being tesed: not formally released

- single sign-on
- backend: Nodejs
	- big query
	- JIRA Cloud
	- Salesforce
	- Cloud datastore
- facade: Angular
- Manhattan Azure AD Identity Protection

- No more excuses about "I didn't know"

- great information for developers to know and put things into context
- This will allow people to pinpoint the customer's issues quicker with more detail
	- Previously, when you get the email too later that "Customer is in a ditch"
	- and you just start digging to try to find the issue
- weighted performance scores
	- get a big picture from different perspectives
# Questions:
1. Are outages weighted based on Proximity to the Planned go-live or specific Project Phase? For example - an outage of a VPT during their volume testing could be almost as bad as when they are in production.
	1. Ryan Rizzo, Great question. For live customer outage becomes higher priority where non live client VPT and other implementation factor is considered, it still WIP.


2. I can definitely see a problem with opening the whole dashboard to too many people. Will there be a mechanism where we could let a person see the subset of projects with which they are engaged?
	1. Agreed David Cauffiel - this need to be sorted out before release


3.Also are we strictly looking at outages or outages + degradations?
	Both


# Looking Ahead
- [ ] Optimizing Scorecard
- [ ] Holistic Parameters
- [ ] Looking at all Dimensions