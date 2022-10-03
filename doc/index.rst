Upstart for ROS Robots
======================

This package aims to assist with creating simple platform-specific jobs
to start your robot's ROS launch files when its PC powers up.

.. toctree::
    :hidden:

    install
    uninstall
    jobs
    providers


Usage
-----

The basic or one-off usage is with the ``install`` script, which can be
as simple as:

.. code-block:: bash

    $ rosrun robot_upstart install myrobot_bringup/launch/base.launch

This will create a job called ``myrobot`` on your machine, which launches
base.launch. It will start automatically when you next start your machine,
or you can bring it up and down manually (command may differ per providers (``upstart`` by default)):

.. code-block:: bash

    When upstart is in use
    $ sudo service myrobot start
    $ sudo service myrobot stop

    When systemd in use
    $ sudo systemctl start myrobot
    $ sudo systemctl stop myrobot

    When supervisor in use
    $ sudo supervisorctl stop myrobot
    $ sudo supervisorctl start myrobot


If the job is crashing on startup, or you otherwise want to see what is
being output to the terminal on startup, check the upstart log:

.. code-block:: bash

    upstart
    $ sudo tail /var/log/upstart/myrobot.log -n 30


    systemd
    $ sudo journalctl -u myrobot

    supervisor
    $ sudo supervisorctl tail -f myrobot stdout

For more details, please see :doc:`install` and :doc:`uninstall`.


Python API
----------

More advanced users or platform maintainers will prefer to script the
job creation as part of a larger installation script which may do other
tasks, such as pick and choose which launchers to install based on a
recipe, interactive wizard, or hardware introspection scheme.

These users will want to work with the Python API, which is detailed 
in :doc:`jobs`.


Extending
---------

If you're interesting in adding support for other init schemes to
robot_upstart, please see :doc:`providers`.


Tips
----

supervisor
==========

You can create a ``roscore`` job along with ``talker_listener.launch``.

.. code-block:: bash

    $ rosrun robot_upstart install --provider supervisor --supervisor-priority 10 --roscore
    $ rosrun robot_upstart install --provider supervisor --supervisor-priority 300 --wait --job talker_listener roscpp_tutorials/launch/talker_listener.launch


Index
-----

* :ref:`genindex`
* :ref:`search`
