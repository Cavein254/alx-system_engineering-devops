**Title: GraphQL Server Incident Report**
An incident involving one of our GraphQL servers on Sept 10th, 2023, resulted in service disruption to our clients. This post-mortem analysis will provide details regarding the incident, its causes, and mitigations to similar future problems.
**Issue Summary**
At approximately 0614 hrs(EAT), one of our graphic servers experienced an outage, resulting in service disruption for 3 hours. On investigation, it was discovered that the server was not processing incoming requests as it had been crushed. 100 percent of the users were affected by this incident. The root cause was a recent upgrade of the Apollo Server that is responsible for processing GraphQL queries.
**Timeline (all Eastern African Time)**
- 0545 hrs: Server maintenance rolled out involving upgrading of packages specifically Apollo Server 3 to Apollo Server 4 
- 0555 hrs: The outage begins
- 0623 hrs: Log servers send alerts through SMSes
- 0645 hrs: Rollback process initiated
- 0712 hrs: Problem solved and the server restarted
- 0743 hrs: 100% of traffic flowing with no incidents
**Root cause and resolution**
At 0545 hrs our deployment team uploaded a new version of the website with package upgrades. Immediately, resolvers fail as the recent version of Apollo Server 4 has major changes in the way it handles queries and mutation. At 0623 hrs log servers send alerts as the servers are full due to logging gibberish errors. 
At 0625 hrs, one of our engineers responded to the problem by isolating the affected server and completely shutting it down. Rolling-back changes begin at 0635 hrs and last for 7 mins. The rollback ends at 0642 hrs and the server is brought back online. The log servers are cleared of the gibberish data and the persistence of useful logs starts. 0645 hrs everything is working as intended.
Corrective and preventative measures
In the next two days, the team sat down to conduct a thorough analysis investigating what had happened and find ways to prevent future occurrences. The following preventive measures were suggested:
- Implement stricter code review measures to catch errors before they are pushed to deployment.
- Write and implement better testing mechanisms
- Conduct a proper audit of the installation package, especially outlining breaking changes before the upgrade
- Improve the current rollback feature to enable quicker rollback in case of similar incidents occurring in the future.


