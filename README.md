# OWASP Notes

top 10 security risks

1. injection
2. broken authentication
3. sensitive data exposure
4. xml external entities
5. broken access control
6. security misconfiguration
7. cross site scripting xss
8. insecure deserialization
9. using compnents with known vulnerablities
10. insuffiecient logging and monitoring

## injection
+ attackers break out of a variable and what they types into that variable gets ran as code instead of read as a variable
- sql injection;  ORMS and RDM are most common venues of attack
    - may try to add and "or 1==true" type statement to get all data instead of merely data they are allowed to access
- javascript can also be injected though



## Broken Authentication
 - only need one admin credential to get access to private data to other users
 - weak passwords are vulnerability
 - poor validation and management of session ids and auth tokens
 - lack of password rotation; if attackers can get one password they can try to use those credentials to get into the users other accounts
    - many people reuse passwords so getting one may allow attackers access to other websites with that users credentials
 - exposure of session
    - poor session security can allow attackers to get session data
    - automated
 - failure for session to timeout can lead to problems when people forget to log out on shared computers
  - credential stuffing = injection of breached usernames/password pairs into different websites until a match is found
    - automated
 
## sensitive data exposure
- certain data needs to be protected more because it is sensitive
    - health records, SSN, secrets, etc
- is data transmitted in clear text
- weak cryptology/encryption
- caching sensitive data risks exposure
- this category basically means all of the other threats but in relation to more sensitive data
- hackers may be able to break encryption - cracking by GPUs
    - (movie hacking)

## xml external entities
- uploading malicious files via xml
- or xml based injection attacks
- source codse analysis tools
    - Static Application Security Testing (SAST); more hepful against xml external entities attacks but hard to set up and can be up limited use against other security issues
    - Dynamic Application Security Testing (DAST) 

## broken access control
- user access roles need to work so that basic users dont have admin rights
- broken access controls can allow users to access other users data
    - old example would be simply changing the profile name in the url once logged in and gettign access to another users account or info
- source codse analysis tools can identify if access controls exist but often not if they work
- attacker may alter metadata cia json or headers, etc
    - access control needs to happen on server side where it cannot be altered by attackers (if other owasp standards met)
    - jwt should be invalidated after logout (see broken auth section)
    - logging helps devs notice issues

## security misconfiguration
- attacks may take advancage of security flaws (this is a very broad categroy that technically covers all of the others)
- notable examples include 
    - error messages that give too much info like stack traces or user info; this can reveal vulnerabilities or even credentials and sensitive info
    - unneccesary features that are not secured; such as sharing private data to a cloud on accident
    - dev or admin options like an admin console that allow access but arent properly secured (delete the hardcoded paswords before production please)

## cross site scripting xss
- 2nd most prevalent issue
- 3 types
    1. reflected XSS
        - escaped user input on application or api allows attacker to execute html and JavaScript in users browser
        - generally requures user to interact with a malicious link
    2. Stored XSS
        - stored input is viewed later...
    3. DOM XSS
        - Javascript applications or frameworks that can change the page based on user input may provide attackers opportunities to manipulate the DOM.
        - may involve session stealing, acount takeover, fake login and node replacement, attacks agaisnt browser and other client side attacks
- avoid giving users access to inputing escapable data - especially if that data manipulates the DOM
- many cheap options for attackers means relatively easy to get started making these attacks


## insecure deserialization
- attackers look for vulnerabilities with deserialization. 
    + they may be able to get malicious code into an api in the form of a serialized object that executes malicious code when deserialized
    + they may be able to manipulate their own access if they figure out how to mimic serialized objects with more access priviledges


## using compnents with known vulnerablities
- update your dependencies and version when possible so that you do not have old vulnerable components
- old versions are often old because they have known vulnerabilities - get the latest version (even if its 6.8 versus 6.7 instead of 7.1)
- it is vital to monitor dependncies and components; stay alert for new alerts and security bulletins
+ have a plan to patch


## insuffiecient logging and monitoring
- if no one is watching they may not see attempts to breach the system
- a quick response may prevent hacking, or identify threats before they get in
- high value transactions and logins should be logged 
- warnings should be specific on the developer end but not on the user end
    - you want your devs to know what the sqlException msg was, not attackers
- store logs locally
- real time reaction; logs should be able to sent alerts
    - also, should be manually checked frequently
- loggin does not stop when the log file fills up
