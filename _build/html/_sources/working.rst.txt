Working with LAPS Portal
========================

LAPS Passwords access
---------------------

After successfully login you can get password of computer. It is possible to use computer name of IP address. If you use IP address LAPS portal do reverse DNS lookup to determine computer name

.. image::  img/laps_password_access.png
  :align: center

It is possible to mark computer as favorite to save time during next search. LAPS Portal also saves search history (computer names only). 

.. image::  img/laps_favorites.png
  :align: center

Quick launch buttons
--------------------

.. warning::  
    Quick launch buttons uses ActiveX that's why supported only in Internet Explorer

You create command templates in **My Profile -> Commands**. Here you can set command patterns to pass computer name and password to any command which can process it. For example to quick launch DameWare remote admin toll you can use following pattern::

  "c:\program Files\DameWare Mini Remote Control 11.0 x64\dwrcc.exe" -c: -h: -a:1 -m:%pc% -u:Administrator -p:%pwd%

.. image::  img/laps_quick_buttons.png
  :align: center

Templates supports following parameters: 

* %pc% - computer name
* %pwd% - password
* %copypwd% - copy password to clipboard (will be deleted from command template after copy)

After command templates are configured quick launch button will be shown in LAPS passwords viewer.

LAPS security log
----------------------
 

Portal has built in Log viewer where you can look for various events 

.. image::  img/laps_audit_log.png
	:align: center
