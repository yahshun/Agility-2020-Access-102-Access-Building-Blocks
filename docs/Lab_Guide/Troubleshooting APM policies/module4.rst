Lab 4: Troubleshooting
======================

Welcome to the troubleshooting APM Policies lab.  This lab is optional.
The lab exercises will provide guidance on how to configure and troubleshoot
common Access Policy Manager (APM) issues as experienced by field engineers,
support engineers, and customers.  This guide is intended to complement 
lecture material provided during the course as well as reference guide for 
students after the class as a basis for troubleshooting APM within your
own environment.  The following troubleshooting techniques will be covered
in this lab:

#.  Message Boxes
#.  Logs
#.  SAML Tracer
#.  F5 tcpdump and Wireshark


Task 1 - Jump Host
----------------------

#. Establish an RDP connection to your Jump Host as well as login to the GUI
of the bigip1.f5lab.local BIG-IP system.

Task 2: General Troubleshooting
------------------------
 
In this lab exercise, you will learn where to look and what to look at when an Access Policy 
is not successfully allowing access or not performing as intended.

#. Questions to ask yourself?

#. Do we have proper Network Connectivity?

#. Are there any Upstream/Downstream Firewall Rules preventing APM to be reachable or to reach destination
targets it requires to access?

#. Do we have DNS setup properly?

#. Do we have NTP setup properly?

#. Are we receiving any Warnings or Error messages when we logon?

#. Are there any missing dependencies?

#. Time to check on our Sessions under Manage Session Menu



    #. What can we see from the Manage Session Menu?
    #. If we click the Session ID link what more information is available?
    #. Is Authentication Successful or is it Failing?
    #. Is the user receiving the proper ENDING ALLOW from the Policy?
	
# Time to Review the Reports information for the Session in question

    #. What information is available from the ALL SESSIONS REPORT?
    #. Can we review the Session Variables for the user’s session from the ALL SESSION REPORT? If YES then Why however If NO then WHY?

# Can the BIG-IP TMOS Resolve the AAA server by Hostname and by Hostname.Domain?

    #. Is the AAA reachable over the network, no Firewalls blocking communication from BIGIP Self-IP?

#. Manage Sessions within the Access Policy Manager menu

#. We use the Manage Sessions menu to view general status of currently logged in sessions,
view their progress through a policy, and to kill sessions when needed.

#. Open a USER session to APM through a new browser window by navigating to your first Virtual
Server IP Address created in LAB I 

#. Did you receive an error message? If so, take note of the Session Reference Number

#. In the browser window, you are using to manage the BIG-IP, navigate to Access  Overview > Active Sessions menu.

#. Review the Manage Sessions screen, is there an Active Session? If not then why?


Task 2 - Message Box 
----------------------

#.  You can log BIG-IP APM session variables by configuring a message box action to display the sessionid variable.

#.  The sessionid is one of the session variables that can be displayed using a message box event.   To do so
perform the following procedure:

#.  Log into the BIG-IP Configuration utility

#.  Navigate to Access Profiles

#.  Edit an Access Profiles

#.  At the point in the Access Policy where you want to insert the message box, click the plus sign (+) to add
an action.

#.  Select the Message Box action

#.  Click Add Item

#.  In the Name box type a name for the action.  For example:   Display session ID

#.  In the Language menu, select language or leave it set to the default language

#.  In the Message box, enter a message to display the session variables.
For example:

	Your session ID is %{session.user.sessionid}
	Your user name is %{session.logon.last.username}
	

Task 2 - APM Logging 
----------------------
	
#. Checking APM Logs

APM Logs by default show the same information you can get from the Manage Sessions menu, as well as APM module-specific information.
Access Policy Manager uses syslog-ng to log events. The syslog-ng utility is an enhanced version of the standard logging utility syslog.
The type of event messages available on the APM are:


Event Messages					File location					Description
Access Policy Events			/var/log/access					Access Policy event messages include logs pertinent to access policy
																SSO, network access, and web applications.   To view access policy events
																on the navigation pane, expand system menu and click logs.
																
																
Audit Logging					/var/log/audit					Audit event messages are log messages that APM logs as a result of configuration changes.



When setting up logging you can customize the logs by designating the minimum severity level or log level,
that you want the system to report when a type of event occurs. The minimum log level indicates the minimum
severity level at which the system logs that type of event.  Note:  Files are rotated daily if their file size exceeds 10MB.
Additionally, weekly rotations are enforced if the rotated log file is a week old, regardless whether or not the file exceeds the 10MB threshold.
The default log level for the BIG-IP APM access policy log is Notice, which does *not* log Session Vari- ables. Setting the access policy log
level to Informational or Debug will cause the BIG-IP APM system to log Session Variables, but it will also add additional system overhead.
If you need to log Session Variables on a production system, F5 recommends setting the access policy log level to Informational temporarily
while performing troubleshooting or debugging


Task 3 - SAML Tracer
----------------------

Overview

SAML Tracer is a browser plugin debugger for viewing SAML messages and can be leveraged
for viewing SAML and WS-Federation messages sent through a browser durng Single Sign-On and logout.
It is an essential tool for SAML debuging and is used extensively by SAML developers when analyzing
Authentication Requests and Responses during a SAML login process.   SAML Tracer is a browser Add-On 
and is supported on Google Chrome and Firefox.    For this lab the SAML Tracer has already been 
enabled within Google Chrome and students will launch SAML Tracer while simultaneously logging into 
the server3.acme.com SAML enabled application.    


#.  Establish an RDP connection to your Jump Host

#.  Lauch Google Chrome

#.  On the top right menu bar click on the SAML Tracer object which will launch SAML Tracer

#.  Within Chrome type in https://sp.acme.com

#.  It may help to minize Chrome and move the SAML Tracer utility to the right side of Chrome
	in order to view the SAML request/response actions
	
#.  Log in to https://sp.acme.com as as user1/user1 

#.  Within the SAML Tracer utility you should see a number of GET and POST responses

#.  Click on one of the GET requests within SAML Tracer and displayed below will be the
	details of the request. In general GET calls will display the request an application 
	is sending to the IdP.   A POST call is often useful to display details such as whether 
	or not an X509 certificate is correct, but can be useful to display any number of variables
	depending on whether the call is SP-Initiated or IdP-Initiated.
	

Task 4 - F5 tcpdump and Wireshark
----------------------

#.  This lab will cover the following topics:

	#. tcpdump switches and filters
	#. F5 specific tcpdump commands
	#. F5 Wireshark plugin
	#. Using the F5 Wireshark plugin
	#. SSL decrypt packet capture
	
#.  Establish an RDP connection to your Jump Host

#	Establish an WebSSH 




































