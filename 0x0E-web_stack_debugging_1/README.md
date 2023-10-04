# Web stack debugging #1

Test and verify your assumptions
The idea is to ask a set of questions until you find the issue. For example, if you installed a web server and it isn’t serving a page when browsing the IP, here are some questions you can ask yourself to start debugging:

Is the web server started? - You can check using the service manager, also double check by checking process list.
On what port should it listen? - Check your web server configuration
Is it actually listening on this port? - netstat -lpdn - run as root or sudo so that you can see the process for each listening port
It is listening on the correct server IP? - netstat is also your friend here
Is there a firewall enabled?
Have you looked at logs? - usually in /var/log and tail -f is your friend
Can I connect to the HTTP port from the location I am browsing from? - curl is your friend
There is a good chance that at this point you will already have found part of the issue.

###Get a quick overview of the machine state
When you connect to a server/machine/computer/container you want to understand what’s happened recently and what’s happening now, and you can do this with 5 commands in a minute or less:

### w
1. shows server uptime which is the time during which the server has been continuously running
shows which users are connected to the server
load average will give you a good sense of the server health - (read more about load here and here)


### history
1. shows which commands were previously run by the user you are currently connected to
2. you can learn a lot about what type of work was previously performed on the machine, and what could have gone wrong with it
3. where you might want to start your debugging work


### top
1. shows what is currently running on this server
2. order results by CPU, memory utilization and catch the ones that are resource intensive


### df
1. shows disk utilization

### netstat
1. what port and IP your server is listening on
2. what processes are using sockets
3. try netstat -lpn on a Ubuntu machine


## Machine

Debugging is pretty much about verifying assumptions, in a perfect world the software or system we are working on would be working perfectly, the server is in perfect shape and everybody is happy. But actually, it NEVER goes this way, things ALWAYS fail (it’s tremendous!).

For the machine level, you want to ask yourself these questions:

	1. Does the server have free disk space? - df
	2. Is the server able to keep up with CPU load? - w, top, ps
	3. Does the server have available memory? free
	4. Are the server disk(s) able to keep up with read/write IO? - htop

If the answer is no for any of these questions, then that might be the reason why things are not going as expected. There are often 3 ways of solving the issue:

	1. free up resources (stop process(es) or reduce their resource consumption)
	2. increase the machine resources (adding memory, CPU, disk space…)
	3. distributing the resource usage to other machines


## Network issue
For the machine level, you want to ask yourself these questions:

1. Does the server have the expected network interfaces and IPs up and running? ifconfig
2. Does the server listen on the sockets that it is supposed to? netstat (netstat -lpd or netstat -lpn)
2. Can you connect from the location you want to connect from, to the socket you want to connect to? telnet to the IP + PORT (telnet 8.8.8.8 80)
4. Does the server have the correct firewall rules? iptables, ufw:
	1. iptables -L
	2. sudo ufw status


## Process issue
If a piece of Software isn’t behaving as expected, it can obviously be because of above reasons… but the good news is that there is more to look into (there is ALWAYS more to look into actually).

1. Is the software started? init, init.d:
	1. service NAME_OF_THE_SERVICE status
	2. /etc/init.d/NAME_OF_THE_SERVICE status
2. Is the software process running? pgrep, ps:
	1. pgrep -lf NAME_OF_THE_PROCESS
	2. ps auxf
3. Is there anything interesting in the logs? look for log files in /var/log/ and tail -f is your friend
## Debugging is fun
Debugging can be frustrating, but it will definitely be part of your job, it requires experience and methodology to become good at it. The good news is that bugs are never going away, and the more experienced you become, trickier bugs will be assigned to you! Good luck :)



# Tasks

0. Nginx likes port 80
mandatory
Using your debugging skills, find out what’s keeping your Ubuntu container’s Nginx installation from listening on port 80. Feel free to install whatever tool you need, start and destroy as many containers as you need to debug the issue. Then, write a Bash script with the minimum number of commands to automate your fix.

Requirements:

Nginx must be running, and listening on port 80 of all the server’s active IPv4 IPs
Write a Bash script that configures a server to the above requirements

1. Make it sweet and short
#advanced
Using what you did for task #0, make your fix short and sweet.

Requirements:

Your Bash script must be 5 lines long or less
There must be a new line at the end of the file
You must respect usual Bash script requirements
You cannot use ;
You cannot use &&
You cannot use wget
You cannot execute your previous answer file (Do not include the name of the previous script in this one)
service (init) must say that nginx is not running ← for real
