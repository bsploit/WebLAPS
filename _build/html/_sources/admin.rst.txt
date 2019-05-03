LAPS Portal administration
==========================

Accessing admin console
-----------------------

Right after initial setup LAPS Portal uses port 8443, open LAPS Portal in your browser https://host:8443. Select built-in authorization and login with admin/admin

.. image::  img/laps_login.png
	:align: center	

.. warning::  
    Change default password in profile settings menu

.. image::  img/profile_menu.png
	:align: center	

Active Directory integration
----------------------------

Go to **Administration->Communications->LDAP** and setup following settings:

* bind user account which has access rights to get attributes ms-Mcs-AdmPwd and modify ms-Mcs-AdmPwdExpirationTime
* FQDN name of AD servers (it is allowed to set several servers divided by ";"")

.. warning:: 
	ms-Mcs-AdmPwd is a special attribute which could be accessed via ldap over **SSL** thats why it is impossible to use IP addresses

* Base OU for computers, users and groups searching
* Attribute of a computer which could contains an user or a group (group nesting is not supported) which will allow to get LAPS password of the computer. This mechanism does not connected with access control subsystem based on groups and containers

.. image::  img/laps_ad_setup.png
	:align: center	

You can enable scheduled password rotation for bind user

.. image::  img/ldap_jobs.png
	:align: center	

Certificates
------------

Go to **Administration->Communications->Certificates** and import AD servers certificate and CA certificates (all certificate chain must be imported). 
In case of other integration which uses ssl/tls protocol like LinOTP HTTP API, FortiAuthenticator and others please do not forget import theirs certificates as well. LAPS Portal supports X.509 DER encoded certificates.

After fresh install LAPS Portal generates self-signed certificate which has alias “jetty”. To replace self-signed certificate:

#. **Administration -> Communications ->Certificates** press "Generate CSR" button, enter DNS name of host where LAPS Portal is located and save generated certificated signing request file.
#. Generate certificated signed by externals CA using generated CSR file
#. Import CA's certificate
#. Import certificate signed by CA, set as alias DNS name of server
#. add string parameter "jetty_cert_alias" at engine.conf file with value of certificate alias
#. restart LAPS Portal

.. warning:: 
	After certificates import do not forget to restart LAPS Portal

Access rights management
------------------------
Go to **Administration->Security->Groups** and setup user group to OU mappings. You must use distinguished names of groups and OUs. Members of group will be able to get LAPS passwords of computers in the OU and sub OUs.

.. image::  img/laps_groups.png
	:align: center

It is possible to import CSV file with groups and OUs mapping, file must be in following portal::

	name of element;group DN;OU DN
	forexample:
	Boston;CN=LAPS_Boston,OU=Groups,DC=domain,DC=com;OU=Boston,OU=Computers,DC=domain,DC=com

Import the file 

.. image::  img/import_laps_mapping.png
	:align: center	

Authentication setup
--------------------

Go to **Administration->Security->Authentication** and setup authentication parameters:

* Require or not password check for internal LAPS Portal users. **If you switch off this requirement then you must enable one time passwords (OTP) validation for this type of users!**
* Require or not password check for Active Directory users. Such approach could be recommended in case you will allow to use LAPS Portal from untrusted environment to eliminate risk of password stealing. **If you switch off this requirement then you must enable one time passwords (OTP) validation for this type of users!**
* Require or not OTP validation for AD users
* Require or not OTP validation for users stored in LAPS Portal
* Type of OTP provider:	
	* linotp provider is used for integration with LinOTP via http API. You must setup LinOTP valudation URL

	.. image::  img/laps_linotp.png
		:align: center	

	* radius provider. You must configure address, shared secret and authentication type: chap, mschap, pap, peap, eap-md5, eap-tls, eap-mschap

	.. image::  img/laps_radius.png
		:align: center	

	* fortiauth provider for integration with FortiAuthenticator

	.. image::  img/laps_fortiauthenticator.png
		:align: center	

	* totp provider which is built in to LAPS Portal. You can use this provider in case you do not have in your environment OTP system to enable two factor authentication for LAPS Portal. If you use this type of TOTP provider you will need to use mobile application like FreeOTP, Google Authenticator, etc.

* Capcha generation requirements: capcha alphabet, unsuccessfull login attempts after capcha will be required 
* Account lockout policy: Account lockout threshold (number of unsuccessfull login attempts) after user will unable to login during defined period of time

.. image::  img/laps_authentication.png
	:align: center


LAPS passwords expiration
-------------------------

Go to **Administration->Security->Extra** and configure automatic LAPS password rotation. After access to ms-Mcs-AdmPwd by any user LAPS portal will modify ms-Mcs-AdmPwdExpirationTime attribute. You can also configure maximum allowed time difference between current time and value which LAPS Portal user can setup in expire field.
If you have more than one domain controller you can force modifing of ms-Mcs-AdmPwdExpirationTime attribute on all configured domain controllers.
Optinally you can add timeout between attempts to get passwords. This timeout will prevent from retriving passwords in fast way. This timeout is not used for API access via tokens described below.

.. image::  img/laps_extra.png
	:align: center

LAPS Portal API and tokens
--------------------------

If you have external systems like Endpoint Detection and Response which require access to passwords managed by LAPS you can use API provided by LAPS portal. To provide access LAPS Portal API you must configure access token. Each access token could be bind to specific IP address and additionally restricted by OU

.. image::  img/laps_api.png
	:align: center

To get LAPS password with help of API you should use GET request to /passwordbytoken/{pc} and pass token in X-Auth cookie ::

	GET /passwordbytoken/computer123
	Content-Type: application/json
	Cookie: X-Auth=APITOKEN

LAPS Portal and SIEM integration
--------------------------------
Go to **Administration->Communications->Syslog** and set IP of syslog receiver. LAPS Portal send logs in CEF format via UDP.

.. image::  img/laps_syslog_cef.png
	:align: center

LAPS Portal mobile app settings
--------------------------------
LAPS Portal has mobile client which works on Android and iOS devices. With help of mobile application it is possible to get passwords and login to LAPS Portal with help of confirmation at mobile device of authentication request which is delivered by push notification.
Go to **Administration->Communications->Mobile** and perform configuration:

* Enable or disable mobile features of LAPS Portal
* Sync URL for mobile app - is URL which LAPS Portal uses to deliver authentication requests via push notifications. Contact to contact@weblaps.pro to get working URL
* External Portal URL - is an URL which will be used by mobile clients to work with LAPS Portal. The only endpoint which is required for mobile device is /api/mobile/fromdevice. In case if you do not plan to publish mobile API to Internet you can use following URL: https://domain.com/api/mobile and mobile application will automatically transform it to https://domain.com/api/mobile/fromdevice. If you plan to expose mobile API to Internet it is recommended  to use reverse proxy with rewrite URL capabilities which will transform all requests in following way:  https://example.org/8fe6392f5994f2ac193627c3001029e4863d10ea => https://domain.com/api/mobile. You can additionally allow only POST and OPTIONS methods
* Organization name and password is used by cloud service to deliver authentication requests via push notifications

.. image::  img/laps_mobile_settings.png
	:align: center

LAPS Portal high availability mode
----------------------------------
High availability mode allows you to join several nodes of LAPS Portal to single cluster and place them behind load balancer or reverse proxy. Please check requirements before using LAPS Portal in cluster mode:

* all nodes must use external database engine
* all nodes must have same private key at keystore with alias "jetty"
* all nodes must use theirs own certificates generated by CA and certificate of CA must be imported to keystore
* load balancer must inject X-Forwarded-For header with valid source IP address

.. image::  img/laps_cluster.png
	:align: center


Extra settings
---------------------
Go **Administration->Communications->Extra** and configure:

* User access token duration (maximum time of users inactivity)
	
.. image::  img/laps_session.png
	:align: center 

* Some sensitive API are protected by internal DoS filter. You can restrict maximum number of requests per second to this sensitive API related to authentication, password accessing

* Forwarded customizer is used to extract source IP address from X-Forwarded-For header which contains information of client IP address if LAPS Portal located behind a reverse proxy or a load balancer.

.. image::  img/laps_network.png
	:align: center 

Backup passwords managed by LAPS

At **Administration->System->Laps Backup** you can configure automatic backup of passwords managed by LAPS. You can use saved passwords in case of AD unavailability. You can configure:

* сron exporession
* password which will be used to encrypt ZIP archive with computers passwords
* base DN of computers
* maximum count of archive files

.. image::  img/laps_passwords_backup.png
	:align: center 
