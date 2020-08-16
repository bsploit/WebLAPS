Installation Prerequisites
==========================

.. |lapsuser| replace:: laps
.. |lapsservice| replace:: laps
.. |lapsdir| replace:: /opt/laps

Prior to installing the WebLAPS, the following requirements must be met:

#. Install Java JRE or JDK version 1.8
#. Check that java executable is on your system PATH. Following command must return no errors
    
	java -version
	
if any error occurred please fix your Java installation https://www.java.com/en/download/help/path.xml

#. Make sure that network connection is open to port 636 (LDAPS) from weblaps host to domain controllers

#. Make sure that your LDAPS is configured at your domain controllers. LAPS stores passwords in special confidential attribute which is accessible only via secured connection. https://social.technet.microsoft.com/wiki/contents/articles/2980.ldap-over-ssl-ldaps-certificate.aspx

#. Prepare service user in AD and grant it permissions to read and reset passwords.

#. Export certificate of CA which signed certificate for LDAPS

#. import CA certificate at mobile devices if you want to use LAPS mobile app and you use your own CA to issue certificate for WebLAPS server.