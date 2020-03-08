Welcome to WebLAPS documentation!
===================================

`LAPS Portal`_ is a web application which helps to secure windows environment with MS LAPS solution implemented. MS LAPS is effective tool to perform automatic password rotation of built-in Administrator password. **In case of compromising one of user account which is used for LAPS passwords access (like account of help desk user) all computers could be compromised!** To eliminate security risks and provide convenient way for LAPS password accessing LAPS Portal was created.

LAPS Portal could be used to implement just-in-time administration (JITA) approach recommended by MS when accounts of system administrators are added to privileged groups for defined period of time and automatically removed after.

LAPS Portal has mobile clients which works under Android_ and iOS_ devices which in a secure way delivers passwords to mobile device. Mobile client also allows to login to LAPS Portal with help of confirmation of authentication request which is delivered by push notification.

LAPS Portal is written in Java, and could be used on any operation systems which support Java 1.8. LAPS Portal includes all necessary components and does not require additional software like web server or database engine. It is possible to join several LAPS Portal to cluster to operatin in a high availability mode in such case you will need a load balancer and an external database engine.

LAPS Portal uses Active Directory user accounts and groups to perform access control. To increase security of passwords managed by LAPS authentication with one time passwords was added to the portal. Currently following 2fa connectors implemented: 

* RADIUS
* LinOTP
* FortiAuthenticator
* Duo
* Built-in TOTP provider which does not require any external system

Security controls implemented in LAPS Portal

* 2FA or OTP only authentication
* password encryption by LAPS.E or AdmPwd.E supported
* customizable capcha for brutforce attacks prevention
* configurable maximum count of requests per seconds to authentications methods
* configurable maximum count of requests per seconds to LAPS passwords accessing to prevent automatic exports of LAPS managed passwords
* access to Active Directory via LDAP over SSL
* all secrets are saved in encrypted form 
* CSRF protection
* user access token is bind to IP address of successful authentication. Access token has a configurable time limit
* ability to schedule LAPS passwords backup in encrypted form in case of AD unavailability
* audit all access to passwords managed by LAPS. It is possible to export LAPS logs in CEF format to external system via syslog 

.. _LAPS Portal: http://weblaps.pro/
.. _Android: https://play.google.com/store/apps/details?id=com.ksoft.laps
.. _iOS: https://itunes.apple.com/us/app/laps-mobile/id1461133789

.. toctree::
   :maxdepth: 3
   :caption: Contents:
   
   working
   mobile
   install_unix
   install_win
   admin
   maintanance   
   
   
