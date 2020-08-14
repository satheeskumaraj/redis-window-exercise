# redis-window-exercise

3. Linux problem solving

Problem statement: Redis service not started. 

Issue identification:

I tired to restart the redis service by using the following command “systemctl restart redis” but it throws the below error.
“Job for redis-server.service failed because the control process exited with error code. See "systemctl status redis-server.service" and "journalctl -xe" for details.”
So i tried to debug nore on this and the following command “journalctl -xe”. It show like some error there in redis.conf file, the error look like bellow.

“redis-server[96196]: Reading the configuration file, at line 108
redis-server[96196]: >>> 'logfile /var/log/redis-server.log'
redis-server[96196]: Can't open the log file: Read-only file system”

Basically this issue will raised either because of permission issue on that particular file or mentioned wrong file pat. While i checked in /lib/systemd/system/redis-server.service file the log will be looking in “ReadWriteDirectories=-/var/log/redis” folder. But in redis.conf which mentioned as “/var/log/redis-server.log”.

Solution:
I changed the logfile from “/var/log/redis-server.log” to “/var/log/redis/redis-server.log” in redis.conf. And restarted the redis it’s worked.


4. Windows problem solving

Problem statement: We have an issue with the web application installed. When browsing to http://localhost/ we get a 503 exception.

Issue identification: 

While checking that issue, i came to know that , DefaultAppPool is in stopped status in IIS Manger. So i tried to start the default one. But it’s again went down. After dig that issue. I came to know that, the Identity was mentioned “AppPoolServiceUser”, But is should be the “ApplicationPoolIdentity”.

Solution:
After changed Identity from “AppPoolServiceUser”  to  “ApplicationPoolIdentity”. And restarted, it’s working fine.


For more information please refer the document.
