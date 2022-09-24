The [Unit] section is common to unit configuration files of all types. It is used to configure general information about the unit and any dependencies that help systemd determine the start up order. In my template I'm adding a description for the service, and I also specify that I want my application to start after the networking subsystem is initialized, since it is a web application.

The [Service] section is where the details specific to your application are included. I'm using the most common options to define the user under which to run the service, the starting directory and the execution command. The Restart option tells systemd that in addition to starting the service when the system boots, I want the application to be restarted if it exits. This takes care of crashes or other unexpected problems that may force the process to end.

Finally, the [Install] section configures how and when the unit should be enabled. By adding the WantedBy=multi-user.target line I'm telling systemd to activate this unit whenever the system is running in multi-user mode, the normal mode a Unix server starts when operational. See a discussion on Unix runlevels if you want to know more details about the multi-user mode.

Unit configuration files are added in the /etc/systemd/system directory to be seen by systemd. Each time you add or modify a unit file you must tell systemd to refresh its configuration:

