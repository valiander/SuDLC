Overview
--------

The level and content of security monitoring, alerting and reporting needs to be set during the requirements and design stage of projects, and should be proportionate to the information security risks. This can then be used to define what should be logged.

There is no one size fits all solution, and a blind checklist approach can lead to unnecessary "alarm fog" that means real problems go undetected.

Technical Standards
-------------------

For Node.js, log4js will be the log framework used.

Standards
---------

Where possible, always log:

-   Input validation failures e.g. protocol violations, unacceptable encodings, invalid parameter names and values

-   Output validation failures e.g. database record set mismatch, invalid data encoding

-   Authentication successes and failures

-   Authorization (access control) failures

-   Session management failures e.g. cookie session identification value modification

-   Application errors and system events e.g. syntax and runtime errors, connectivity problems, performance issues, third party service error messages, file system errors, file upload virus detection, configuration changes

-   Application and related systems start-ups and shut-downs, and logging initialization (starting, stopping or pausing)

-   Use of higher-risk functionality e.g. network connections, addition or deletion of users, changes to privileges, assigning users to tokens, adding or deleting tokens, use of systems administrative privileges, access by application administrators, all actions by users with administrative privileges, access to payment cardholder data, use of data encrypting keys, key changes, creation and deletion of system-level objects, data import and export including screen-based reports, submission of user-generated content - especially file uploads

-   Legal and other opt-ins e.g. permissions for mobile phone capabilities, terms of use, terms & conditions, personal data usage consent, permission to receive marketing communications

Optionally consider if the following events can be logged and whether it is desirable information:

-   Sequencing failure

-   Excessive use

-   Data changes

-   Fraud and other criminal activities

-   Suspicious, unacceptable or unexpected behavior

-   Modifications to configuration

-   Application code file and/or memory changes

### Event attributes

Each log entry needs to include sufficient information for the intended subsequent monitoring and analysis. It could be full content data, but is more likely to be an extract or just summary properties.

The application logs must record "when, where, who and what" for each event.

The properties for these will be different depending on the architecture, class of application and host system/device, but often include the following:

-   When

    -   Log date and time (international format)

    -   Event date and time - the event timestamp may be different to the time of logging e.g. server logging where the client application is hosted on remote device that is only periodically or intermittently online

    -   Interaction identifier Note A

-   Where

    -   Application identifier e.g. name and version

    -   Application address e.g. cluster/hostname or server IPv4 or IPv6 address and port number, workstation identity, local device identifier

    -   Service e.g. name and protocol

    -   Geolocation

    -   Window/form/page e.g. entry point URL and HTTP method for a web application, dialogue box name

    -   Code location e.g. script name, module name

-   Who (human or machine user)

    -   Source address e.g. user's device/machine identifier, user's IP address, cell/RF tower ID, mobile telephone number

    -   User identity (if authenticated or otherwise known) e.g. user database table primary key value, user name, license number

-   What

    -   Type of event Note B

    -   Severity of event Note B e.g. {fatal, error, warning, info, debug, trace}

    -   Security relevant event flag (if the logs contain non-security event data too)

    -   Description

Additionally consider recording:

-   Secondary time source (e.g. GPS) event date and time

-   Action - original intended purpose of the request e.g. Log in, Refresh session ID, Log out, Update profile

-   Object e.g. the affected component or other object (user account, data resource, file) e.g. URL, Session ID, User account, File

-   Result status - whether the ACTION aimed at the OBJECT was successful e.g. Success, Fail, Defer

-   Reason - why the status above occurred e.g. User not authenticated in database check ..., Incorrect credentials

-   HTTP Status Code (web applications only) - the status code returned to the user (often 200 or 301)

-   Request HTTP headers or HTTP User Agent (web applications only)

-   User type classification e.g. public, authenticated user, CMS user, search engine, authorized penetration tester, uptime monitor (see "Data to exclude" below)

-   Analytical confidence in the event detection Note B e.g. low, medium, high or a numeric value

-   Responses seen by the user and/or taken by the application e.g. status code, custom text messages, session termination, administrator alerts

-   Extended details e.g. stack trace, system error messages, debug information, HTTP request body, HTTP response headers and body

-   Internal classifications e.g. responsibility, compliance references

-   External classifications e.g. NIST Security Content Automation Protocol (SCAP), Mitre Common Attack Pattern Enumeration and Classification (CAPEC)

**Note A:** The "Interaction identifier" is a method of linking all (relevant) events for a single user interaction (e.g. desktop application form submission, web page request, mobile app button click, web service call). The application knows all these events relate to the same interaction, and this should be recorded instead of losing the information and forcing subsequent correlation techniques to re-construct the separate events. For example a single SOAP request may have multiple input validation failures and they may span a small range of times. As another example, an output validation failure may occur much later than the input submission for a long-running "saga request" submitted by the application to a database server.

**Note B:** Each organization should ensure it has a consistent, and documented, approach to classification of events (type, confidence, severity), the syntax of descriptions, and field lengths & data types including the format used for dates/times.

### Data to exclude

Never log data unless it is legally sanctioned. For example intercepting some communications, monitoring employees, and collecting some data without consent may all be illegal.

Never exclude any events from "known" users such as other internal systems, "trusted" third parties, search engine robots, uptime/process and other remote monitoring systems, pen testers, auditors. However, you may want to include a classification flag for each of these in the recorded data.

The following should not usually be recorded directly in the logs, but instead should be removed, masked, sanitized, hashed or encrypted:

-   Application source code

-   Session identification values (consider replacing with a hashed value if needed to track session specific events)

-   Access tokens

-   Sensitive personal data and some forms of personally identifiable information (PII) e.g. health, government identifiers, vulnerable people

-   Authentication passwords

-   Database connection strings

-   Encryption keys and other master secrets

-   Bank account or payment card holder data

-   Data of a higher security classification than the logging system is allowed to store

-   Commercially-sensitive information

-   Information it is illegal to collect in the relevant jurisdictions

-   Information a user has opted out of collection, or not consented to e.g. use of do not track, or where consent to collect has expired

Sometimes the following data can also exist, and whilst useful for subsequent investigation, it may also need to be treated in some special manner before the event is recorded:

-   File paths

-   Database connection strings

-   Internal network names and addresses

-   Non sensitive personal data (e.g. personal names, telephone numbers, email addresses)

Consider using personal data de-identification techniques such as deletion, scrambling or pseudonymization of direct and indirect identifiers where the individual's identity is not required, or the risk is considered too great.

In some systems, sanitization can be undertaken post log collection, and prior to log display.