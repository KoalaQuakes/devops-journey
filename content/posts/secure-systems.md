+++
date = '2026-08-21T16:19:36+02:00'
draft = true
title = 'Secure Systems'
+++

** Secure Foundation **

Security is a wide-ranging, deep and multi-facitied topic. To keep thing very brief I will cover a very reductive but important foundation to secure systems. These are the high-level sections I like to cover to get to standard base line: 

1. Identity and Authentication
2. Logs and Audits
3. Access monitoring and alerting
4. Network configuration and rules
5. Data Encryption
6. Capacity and Resiliance
7. Working environment
8. Work Produced

1. 
Idetity and Authetication is the bedrock, it is so important that everything else is built upon the assumption that authorised individuals control a digital identity that only they, and them alone, use and control.

All identities should be tied to individuals and avoid sharing accounts as much as possible. If it is unavoidable, document a clear procedure to time-bind the access to an invidual. Identities should be connected as much as possible, using SSO.

Authentication needs to be very robust. Today, the minimum is:
Username - often e-mail address
Password - long (15+ characters)
Multi-Factor / 2-Step Verification - Authentication app on phone 

2. 
Logs set up to track access attemps and frequencies, change actions, admin tasks but they need to be relevant only for security indiviualtion.

Audits need to validate and clarify the current state of against it's expected state. Logs are a tool to asssit but it's important there is no conflict of interest so audit functions should be outside of operations and development.

3. 
Access monitoring and alerting. Automated monitoring and alerts for manual review. some examples of automated monitoring include, impossible travel, adaptive profiling, frequency of attempts, 