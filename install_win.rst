Installation in Windows
=======================

.. |lapsuser| replace:: laps
.. |lapsservice| replace:: laps
.. |lapsdir| replace:: C:\\laps\\

Installation is pretty simple, the only thing you need is to install Java JRE 1.8

#. Create local user "|lapsuser|" – this user will be used to run portal service.
#. Allow user "|lapsuser|" to work as a service::
    
    gpedit.msc -> Local Policy -> User Rights Assignment -> Log on as a service: add user "laps"
    
#. Create directory |lapsdir| and extract distributive.
#. Change the directories owner and set up appropriate access rights: user "|lapsuser|" must have read and write access rights, other users except administrators must not have access to the directory
#. if java.exe is not on %PATH% set correct path to java executable in file C:\\laps\\wrapper\\conf\\wrapper.conf. As file path separator use *"/"*:
    
    wrapper.java.command = path_to_java_exe
    
#. Install LAPS portal service. New service "|lapsservice|" will be created.::

    C:\\laps\\wrapper\\bat\\installService.bat

#. If you have your own license file copy it to C:\\laps\\_conf\\license.txt. Default destribition includes a community license file.
#. Run the service::

    net start laps

#. Open in browser https://host:8443 
