The setup should have one central NTP server, and the other servers should only use this server.

To achieve this, you have to edit the files `/etc/ntp.conf` and `/etc/default/ntpdate`, if they exist.

* For the NTP server, just keep the entries, you don't have to change anything.
* For the clients, remove all other servers from the files and only add the ip of the one server on the local network.

Now, the servers should synchronize themselves within minutes after system startup.

You can check how good the synchronization is by running `sudo ntpdate -dvup 8 <ip>`. If the command fails, the main server is not yet synced.
