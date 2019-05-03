LAPS Portal mobile application
==============================
LAPS Portal has mobile clients which works under Android_ and iOS_ devices. 
Main features of LAPS mobile client:

* secure access to passwords managed by MS LAPS: in addition to TLS encryption all passwords are additionally encrypted with AES algorithm with unique device key per user. This device key is generated during device enrollment process and stored in secure way at mobile device. On iOS key is stored directly in the KeyChain. On Android key itself is encrypted with random 256-bit AES master key which is encrypted with a device-generated RSA (RSA/ECB/PKCS1Padding) from the Android KeyStore. The combination of the encrypted RSA(AES(master key)) and AES(device key) are stored in SharedPreferences.
* PIN protection. If device has fingerprint scanner it will be automatically used by application 
* ability to get LAPS passwords in a convenient and secure way using mobile device
* ability to setup password new expiration date
* login to LAPS Portal with help of confirmation of push notification

LAPS mobile application enrollment
----------------------------------
There are two way how to start use LAPS mobile application

1. Go to **Profile settings -> Mobile**, press "Enroll mobile device" and scan generated QR code at mobile device

.. image::  img/profile_menu.png
	:align: center	

.. image::  img/laps_mobile_enroll_qr.png
	:align: center	

2. Enter External Portal URL configured at **Administration->Communications->Mobile** to mobile device URL field, fill username, password and OTP

.. image::  img/laps_mobile_enrollment.png
	:align: center	

LAPS mobile application usage
-----------------------------
#. Enter PIN or use your fingerprint to login to LAPS Mobile

.. image::  img/laps_mobile_login.png
	:align: center	

#. Enter computer name and press find button

.. image::  img/laps_mobile_app.png
	:align: center	

.. _Android: https://play.google.com/store/apps/details?id=com.ksoft.laps
.. _iOS: https://itunes.apple.com/us/app/laps-mobile/id1461133789