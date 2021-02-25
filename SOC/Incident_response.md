Purpose
-------

This document describes <Your Company>'s overall plan for preparing and responding to any business or technical incidents. It defines the roles and responsibilities of participants, characterization of incidents, relationships to other policies and procedures, and reporting requirements. The goal of this Incident Response Plan is to prepare for, detect, and respond to incidents. It provides a framework by which the Incident Response Team shall determine the scope and risk of an incident, respond appropriately to that incident, communicate the results and risks to all stakeholders, and reduce the likelihood of an incident from occurring or reoccurring.

Scope
-----

This plan applies to the physical location, the information systems, and networks of <Your Company> and any person or device that gains access to these systems or data.

Maintaining Currency
--------------------

It is the responsibility of the Security Manager to maintain and revise this policy to ensure that it is always in a ready state.

Definitions
-----------

### Event

An event is an exception to the normal operation of infrastructure, systems, or services. Not all events\
become incidents.

### Incident

An incident is an event that, as assessed by the staff, violates the policies of <Your Company> as related to Information Security, Physical Security, or Acceptable Use; other policies, standards, or codes of conduct; or threatens the confidentiality, integrity, or availability of information systems.

Incidents will be prioritized according to their potential for the exposure of protected data or the criticality of the resource, using a four (4) level system consisting of:

-   0 -- Critical

-   1 -- High

-   2 -- Low

-   3 -- None.

Incidents can include:

-   Malware/viruses/Trojans.

-   Ransomware.

-   Phishing.

-   Unauthorized electronic access.

-   Breach of information.

-   Unusual, unexplained or repeated loss of connectivity.

-   Unauthorized physical access.

-   Loss or destruction of physical files, etc.

### Evidence Preservation

The goal of any incident response is to reduce and contain the impact of an incident and ensure that information security related assets are returned to service in the timeliest manner possible. The need for a rapid response is balanced by the need to collect and preserve evidence in a manner consistent with state and federal laws, and to abide by legal and administrative requirements for documentation and chain-of-custody.

### Incident Response

The Incident Response Life Cycle consists of a series of phases: distinct sets of activities that will assist in the handling of an incident, from start to finish.

### Preparation

Preparation includes those activities that enable <Your Company> to respond to an incident. These include a variety of policies, procedures, tools, as well as governance and communications plans. <Your Company> utilizes several mechanisms to prevent, and prepare to respond to, an incident.

-   Security Awareness Training: All personnel are required to take compliant Security Awareness Training. This training must be updated at a minimum of every year. This training covers additional ongoing threats to systems such as malware, phishing, social engineering, ransomware, and other threats as they become known.

-   Malware/Antivirus/Spyware Protections: All information system terminals, as well as key information flow points on the network are protected by continuous defense against malware/antivirus/spyware and other known malicious attacks. These defense mechanisms are kept up to date without the need for end user intervention, and end users are restricted from accessing, modifying, disabling, or making other changes to the defense mechanisms.

-   Firewalls and Intrusion Prevention Devices (IPD): Multiple firewalls and IPD are in place within the network to provide the necessary depth of defense. DevOps and Security departments keep all firewalls and IPD up to date with the latest security patches and other relevant upgrades, as well as maintain an active backup of the latest security configuration.

-   Personnel Security Measures: All <Your Company> personnel with access to where data is accessed, stored, modified, transmitted, or maintained have been cleared to the required Personnel Security standards set forth in SOC compliance documents.

-   Event Logs: Event logging is maintained at all applicable levels, capturing all the required events and content specified for SOC compliance, retained for the specified period, and reviewed weekly.

-   Patching/Updating: Systems shall be patched and updated as new security patches and hot fixes are released. Any software or hardware product that reaches the end of the manufacturers service and support life for patching will be deemed out-of-compliance and replaced.

### Staffing

<Your Company> will strive to maintain adequate staff levels and third-party support to investigate each incident to completion and communicate its status to other parties while it continues to monitor the tools that detect new events.

### Training

No incident response capability can be effectively maintained over time without proper and ongoing training. The continuous improvement of incident handling processes implies that those processes are periodically reviewed, tested, and translated into recommendations for enhancements. All <Your Company> staff will be trained on a periodic basis in security awareness, procedures for reporting and handling incidents to ensure a consistent and appropriate response to an incident, and that postincident findings are incorporated into policy and procedure.

Detection and Analysis
----------------------

### Detection

Detection is the discovery of an event with security tools or through notification by an inside or outside party about a suspected incident. The detection of an incident requires the immediate activation of the Incident Response Team as listed in Appendix A. The determination of an incident can arise from one or several circumstances simultaneously. Means by which detection can occur include:

-   Trained personnel reviewing collected event data for evidence of compromise.

-   Software applications analyzing events, trends, and patterns of behavior.

-   Intrusion Protection/Intrusion Detection devices alerting to unusual network or port traffic.

-   The observation of suspicious or anomalous activity within any <Your Company> facility or on a\
    computer system.

It is critical in this phase:

-   To detect whether a incident has occurred.

-   To determine the method of attack.

-   To determine the impact of the incident to the mission, systems, and personnel involved in the\
    incident.

-   To obtain or create intelligence products regarding attack modes and methods.

### Analysis

Analysis of the incident indicators will be performed in a manner consistent with the type of incident. For any technical incident, <Your Company> will utilize on call developers to perform static and dynamic analysis of malicious code, a review of information system boundary protections, determination of source code if applicable, the depth and breadth of the attack, if the attack has migrated to other systems on or off the network, and any other tasks appropriate to the type of incident experienced. These analyses can be performed either manually or utilizing automated tools dependent upon the situation, timeliness, and availability of resources.

### Incident Categories

An incident will be categorized as one of four severity levels. These severity levels are based on the impact to <Your Company> and can be expressed in terms of financial impact, impact to services and/or performance of our mission functions, or impact to SOC compliance, etc. The below table provides a listing of the severity levels and a definition of each severity level.

### Severity Level Description

|

**Severity Level**

 |

**Description**

 |
|

3 (Low)

 |

Incident where the impact is minimal. Examples may be e-mail SPAM, isolated virus infections, etc.

 |
|

2 (Medium)

 |

Incident where the impact is significant. Examples may be a delayed or limited ability to provide services, delayed delivery of critical electronic mail or data transfers, etc.

 |
|

1 (High)

 |

Incident where the impact is severe. Examples may be a disruption to the services and/or performance of our mission functions. <Your Company>'s proprietary or confidential information has been compromised, a virus or worm has become wide spread and is affecting over 1 percent of employees, etc.

 |
|

0 (Critical)

 |

Incident where the impact is catastrophic. Examples may be a shutdown of all <Your Company>'s network services. <Your Company>'s proprietary or confidential information has been compromised and published in/on a public venue or site.

 |

Containment, Eradication, and Recovery
--------------------------------------

### Containment

Incident Manager is responsible for containment and will document all containment activities during an incident.

Containment activities for incidents involve decision-making and the application of strategies to help control attacks and damage, cease attack activities, or reduce the impact or damage caused by the incident. This requires intelligence gathered by the detection and analysis phases of the incident -- for example, identification of affected hosts, identification of attacking hosts or attackers, identification of malware and its capabilities, and identification and monitoring of attacker communication channels. In most cases, it is important to introduce containment solutions all at once, as attackers may escalate their attack activity if deployment of the strategy is delayed.

### Eradication

Incident Manager is responsible for eradication and will document all eradication activities during an incident.

Eradication efforts for an incident involve removal of latent threats from systems (such as malware on the system and user accounts that may have been created), identifying and mitigating potential vulnerabilities or misconfigurations that may have been exploited, and identification of other hosts that may have been affected within the organization.

### Recovery

Incident Manager is responsible for recovery and will document all recovery\
activities during an incident.

Recovery efforts for incidents will involve the restoration of affected systems to normal operation. This is dependent upon the type of incident experienced but may include actions such as restoring systems from backups, rebuilding systems from an agency approved baseline, replacing compromised files with clean versions, installing patches, changing passwords, and increasing network perimeter and host-based security.

### Post-Incident Activity

Incident Manager is responsible for documenting and communicating postincident activity.

Post-incident activities will occur after the detection, analysis, containment, eradication, and recovery from an incident. One of the most important phases of incident response, post-incident activities involve the reflection, compilation, and analysis of the activities that occurred leading to the incident, and the actions taken by those involved in the incident, including the incident response team. Important items to be reviewed and considered for documentation are:

-   Exactly what happened, and at what times?

-   How well did staff and management perform in dealing with the incident?

-   What information was needed sooner?

-   Were any steps or actions taken that might have inhibited the recovery?

-   What should be done differently the next time a similar incident occurs?

-   How could information sharing with other organizations have been improved?

-   What corrective actions can prevent similar actions in the future?

-   What precursors or indicators should be watched for in the future to detect similar incidents?

-   What additional tools or resources are needed to detect, analyze, and mitigate future incidents?

Post-incident activities will be incorporated into future training opportunities for all parties involved in the incident, from victims, to system administration personnel, to incident responders.

Escalation
----------

The escalation process will be initiated to involve other appropriate resources as the incident increases in scope and impact. Incidents should be handled at the lowest escalation level that can respond to the incident with as few resources as possible in order to reduce the total impact and maintain limits on cyber-incident knowledge. The table below defines the escalation levels with the associated team members involvement.

|

Severity Level

 |

Response Team Member Involvement

 |

Description

 |
|

Priority 3 (P3)

 |

-   Support Engineer

-   PST Stakeholder (Optional)

-   SST Stakeholder (Optional)

 |

Normal operations. Does not affect major parts of the system.

 |
|

Priority 2 (P2)

 |

-   Support Engineer

-   PST Stakeholder (Optional)

-   SST Stakeholder (Optional)

 |

Issue reported and is impacting a part of the application, but normal operations are still available.

 |
|

Priority 1 (P1)

 |

-   Incident Manager

-   Support Engineer

-   PST Stakeholder (Optional)

-   SST Stakeholder (Optional)

-   Executive Stakeholder (Optional)

 |

Issue reported and is affecting customers or internal employees; workflow is partially or entirely blocked. Partial site outage or minor payments issues.

 |
|

Priority 0 (P0)

 |

-   Incident Manager

-   Support Engineer

-   PST Stakeholder

-   SST Stakeholder

-   Executive Stakeholder

 |

Issue reported and is impactful system-wide; site outages and major payments errors

 |

The Incident Response Team will consider several characteristics of the incident before escalating the response to a higher level. They are:

-   How wide spread is the incident?

-   What is the impact to business operations?

-   How difficult is it to contain the incident?

-   How fast is the incident propagating?

-   What is the estimated financial impact to [Municipality or county name]?

-   Will this negatively affect [Municipality or county name]'s image?

Appendix A: Incident Response Team
----------------------------------

|

**Role**

 |

**Assignee**

 |

**Contact Information**

 |
|

Incident Manager

 |

Secondary developer on call

 |  |
|

Support Engineer

 |

Primary developer on call

 |  |
|

PST Stakeholder

 |

Sonal

 |  |
|

SST Stakeholder

 |

Starr

 |  |
|

Executive Stakeholder

 |

Tyler, Sonal, David, A.T.

 |  |

Appendix B: Incident Response Process Tree
------------------------------------------

This document discusses the steps taken during an incident response plan. To create the plan, the steps\
in the following example should be replaced with contact information and specific courses of action\
for your organization.

1.  The person who discovers the incident will escalate to the appropriate stakeholder. List possible sources of those who may discover the incident. The known sources should be provided with a contact procedure and contact list. Sources requiring contact information may be:

    1.  Helpdesk

    2.  Engineering Manager

    3.  Other relevant stakeholders

    4.  List all sources and check off whether they have contact information and procedures. Usually each source would contact one 24/7 reachable entity such as a developer on call. Those in the engineering department may have different contact procedures than those outside of the department.

2.  If the person discovering the incident is a member of the Engineering department or affected department, they will proceed to step four (4).

3.  The Helpdesk/Engineering Staff will refer to the development on call contact list or effected department contact list and call the designated numbers in order on the list. The Helpdesk will log:

    1.  The name of the caller.

    2.  Time of the call.

    3.  Contact information about the caller.

    4.  The nature of the incident.

    5.  When the event was first noticed, supporting the idea that the incident occurred.

4.  The IT staff member or affected department staff member who receives the call (or discovered the incident) will refer to their contact list for both management personnel to be contacted and incident response members to be contacted. The staff member will call those designated on the list. The staff member will contact the incident response manager using both email and phone messages. The staff member will log the information received in the same format as the grounds security office in the previous step. The staff member could possibly add the following:

    1.  Is the system affected business critical?

    2.  What is the severity of the potential impact?

    3.  Name of system being targeted, along with operating system, Internet Protocol (IP) address, and location.

    4.  IP address and any information about the origin of the attack.

5.  Contacted members of the response team will meet or discuss the situation over the telephone\
    and determine a response strategy.

    1.  Is the incident real or perceived?

    2.  Is the incident still in progress?

    3.  What data or property is threatened and how critical is it?

    4.  What is the impact on the business should the attack succeed? Minimal, serious, or critical?

    5.  What system or systems are targeted, where are they located physically and on the network?

    6.  Is the incident inside the trusted network?

    7.  Is the response urgent?

    8.  Can the incident be quickly contained?

    9.  Will the response alert the attacker and do we care?

    10. What type of incident is this? Example: virus, worm, intrusion, abuse, damage.

6.  An incident ticket will be created. The incident will be categorized into the highest applicable\
    level of one of the following categories:

    1.  Priority 0 - A company wide impacting event.

    2.  Priority 1 - A threat to sensitive data.

    3.  Priority 2 - A threat to computer systems.

    4.  Priority 3 - A disruption of services.

7.  Team members will establish and follow one of the following procedures basing their response\
    on the incident assessment:

    1.  Worm response procedure.

    2.  Virus response procedure.

    3.  System failure procedure.

    4.  Active intrusion response procedure - Is critical or sensitive data (Personally Identifiable Information (PII), etc.) at risk?

    5.  Inactive Intrusion response procedure.

    6.  System abuse procedure.

    7.  Property theft response procedure.

    8.  Website denial of service response procedure.

    9.  Database or file denial of service response procedure.

    10. Spyware response procedure.

    11. The team may create additional procedures which are not foreseen in this document. If there is no applicable procedure in place, the team must document what was done and later establish a procedure for the incident.

8.  Team members will use forensic techniques, including reviewing system logs, looking for gaps in logs, reviewing intrusion detection logs, and interviewing witnesses and the incident victim to determine how the incident was caused. Only authorized personnel should be performing interviews or examining evidence, and the authorized personnel may vary by situation and the organization.

9.  Team members will recommend changes to prevent the occurrence from happening again or infecting other systems.

10. Upon management approval, the changes will be implemented.

11. Team members will restore the affected system(s) to the uninfected state. They may do any or more of the following:

    1.  Reinstall the affected system(s) from scratch and restore data from backups if necessary. Preserve evidence before doing this.

    2.  Make users change passwords if passwords may have been sniffed.

    3.  Be sure the system has been hardened by turning off or uninstalling unused services.

    4.  Be sure the system is fully patched.

    5.  Be sure real time virus protection and intrusion detection is running.

    6.  Be sure the system is logging the correct events and to the proper level.

12. Documentation: the following shall be documented:

    1.  How the incident was discovered.

    2.  The category of the incident.

    3.  How the incident occurred, whether through email, firewall, etc.

    4.  Where the attack came from, such as IP addresses and other related information about the attacker.

    5.  What the response plan was.

    6.  What was done in response?

    7.  Whether the response was effective.

13. Evidence Preservation: make copies of logs, email, and other communication. Keep lists of witnesses. Keep evidence as long as necessary to complete prosecution and beyond, in case of an appeal.

14. Notify proper external agencies: notify the police and other appropriate agencies if prosecution of the intruder is possible. List the agencies and contact numbers here.

15. Assess damage and cost: assess the damage to the organization and estimate both the damage\
    cost and the cost of the containment efforts.

16. Review response and update policies: plan and take preventative steps so the intrusion can't\
    happen again.

    1.  Consider whether an additional policy could have prevented the intrusion.

    2.  Consider whether a procedure or policy was not followed which allowed the intrusion,\
        and then consider what could be changed to ensure that the procedure or policy is\
        followed in the future.

    3.  Was the incident response appropriate? How could it be improved?

    4.  Was every appropriate party informed in a timely manner?

    5.  Were the incident response procedures detailed, and did they cover the entire\
        situation? How can they be improved?

    6.  Have changes been made to prevent a reinfection? Have all systems been patched,\
        systems locked down, passwords changed, antivirus updated, email policies set, etc.?

    7.  Have changes been made to prevent a new and similar infection?

    8.  Should any security policies be updated?

    9.  What lessons have been learned from this experience?

Policy Information
------------------
| Category | Description |
| ----------- | ----------- |
| Effective Date | Date |
| Policy Owner | Person |
| Policy Administrator | Person |