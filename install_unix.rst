Installation in Unix
=======================

.. |lapsuser| replace:: laps
.. |lapsservice| replace:: laps
.. |lapsdir| replace:: /opt/laps

Installation is pretty simple, the only thing you need is to install Java JRE 1.8

#. Install Java JRE or JDK version 1.8
#. Create local user "|lapsuser|" – this user will be used to run portal service::

	useradd laps --shell /sbin/nologin --no-create-home

#. Create working directory for LAPS WebPortal and extract distributive::

	mkdir /opt/laps
	unzip /tmp/laps.zip /opt/laps

#. Change an owner of the directory and set correct access rights::

	chown -R laps:laps /opt/laps
	chmod –R u=rwx,g=rx,o-rwx /opt/laps

#. If java executable is not on PATH set correct path to java executable in /opt/laps/wrapper/conf/wrapper.conf::

	wrapper.java.command = путь_до_иполняемого_файла_java

#. Install LAPS portal service. New service "|lapsservice|" will be created.::

	/opt/laps/wrapper/sh/installDaemon.sh

#. Run the service::

	service laps start

#. Open in browser https://host:8443 