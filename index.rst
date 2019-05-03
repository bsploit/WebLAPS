Welcome to WebLAPS documentation!
===================================

`LAPS Portal`_ is a web application which helps to secure windows environment with MS LAPS solution implemented. MS LAPS is effective mechanism to perform automatic password rotation of built-in Administrator password. **In case of compromising one of user account which is used for LAPS passwords access (like account of help desk user) all computers could be compromised!** To eliminate security risks and provide convenient way for LAPS password accessing LAPS Portal was created.

LAPS Portal has mobile clients which works under Android_ and iOS_ devices which in a secure way delivers passwords to mobile device. Mobile client also allows to login to LAPS Portal with help of confirmation of authentication request which is delivered by push notification.

LAPS Portal is written in Java, and could be used on any operation systems which support Java 1.8. LAPS Portal includes all necessary components and does not require additional software like web server or database engine. It is possible to join several LAPS Portal to cluster to operatin in a high availability mode in such case you will need a load balancer and an external database engine.

LAPS Portal uses Active Directory user accounts and groups to perform access control. To increase security of passwords managed by LAPS authentication with one time passwords was added to the portal. Currently following 2fa connectors implemented: 

* RADIUS
* LinOTP
* FortiAuthenticator
* Built-in TOTP provider which does not require any external system

Security controls implemented in LAPS Portal

* 2FA or OTP only authentication
* Customizable capcha for brutforce attacks prevention
* Configurable maximum count of requests per seconds to authentications methods
* Configurable maximum count of requests per seconds to LAPS passwords accessing to prevent automatic exports of LAPS managed passwords
* Access to Active Directory via LDAP over SSL
* All secrets are saved in encrypted form 
* CSRF protection
* User access token is bind to IP address of successful authentication. Access token has a configurable time limit
* Ability to schedule LAPS passwords backup in encrypted form in case of AD unavailability
* Audit all access to passwords managed by LAPS. It is possible to export LAPS logs in CEF format to external system via syslog 

.. _LAPS Portal: http://weblaps.pro/
.. _Android: https://play.google.com/store/apps/details?id=com.ksoft.laps
.. _iOS: https://itunes.apple.com/us/app/laps-mobile/id1461133789

.. toctree::
   :maxdepth: 3
   :caption: Contents:
   
   working
   install_unix
   install_win
   admin
   maintanance   
   mobile
   
