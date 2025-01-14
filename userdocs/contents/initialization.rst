=======================
Warewulf Initialization
=======================

System Services
===============

Once Warewulf has been installed and configured, it is ready to be initialized and have the associated system services started. To do this, start by configuring the system services that Warewulf depends on for operation. To do that, run the following command:

.. code-block:: bash

   sudo wwctl configure --all

This command will configure the system for Warewulf to run properly. Here are the things it will do:

* **dhcp**: (re)Write the DHCP configuration and restart the service from the configured template in ``/etc/warewulf/dhcp/`` and enable the system service.
* **hostfile**: Update the system's /etc/hosts file based on the template ``/etc/warewulf/hosts.tmpl``.
* **nfs**: Configure the NFS server on the control node as well as the ``/etc/fstab`` in the system overlay based on the configuration in ``/etc/warewulf/warewulf.conf`` and enable the system service.
* **ssh**: Create the appropriate host keys (stored in ``/etc/warewulf/keys/``) and user keys for passwordless ``ssh`` into the nodes.
* **tftp**: Write the appropriate binary PXE/iPXE blobs to the TFTP root directory and enable the system service.

This command will quickly setup the system services per the Warewulf configuration. Watch this output carefully for errors and resolve them in the configuration portion of this manual.

Warewulf Service
================

The Warewulf installation attempts to register the Warewulf service with Systemd, so it should be as easy to start/stop/check as any other Systemd service:

.. code-block:: bash

   sudo systemctl enable --now warewulfd

You can also check and control the Warewulf service using the `wwctl` command line program as follows:

.. code-block:: bash

   sudo wwctl server status

.. note::
   If the Warewulf service is running via Systemd, restarting stopping, and starting it from the ``wwctl`` command may result in unexpected results.

Logs
----

The Warewulf server logs are by default written to ``/var/log/warewulfd.log``.