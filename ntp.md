To sync times between servers
`sudo ntpdate -dvup 8 <ip>`

If syncing fails and output contains strata too high, you have to force updating the time. On your local machine, edit the `/etc/ntp.conf` and `/etc/default/ntpdate` to only contain the server you are syncing to.
After that do:

 * `sudo service ntp stop`
 * `sudo ntpd -q -g -x -n`
 * `sudo service ntp start`
 
Now do
`sudo ntpdate -dvup 8 <ip>`
again, to ensure it worked.



You have to add the ip of the ntp server to the /etc/ntp.conf file, and remove all other ips.
