# Load balancer

Load balancer will distribute the work-load of your system to multiple individual systems, or group of systems to to reduce the amount of load on an individual system, which in turn increases the reliability, efficiency and availability of your enterprise application or website.

## advantages of load balancing your application:

1. Reduced the work-load on an individual server.
2. Large amount of work done in same time due to concurrency.
3. Increased performance of your application because of faster response.
4. No single point of failure. In a load balanced environment, if a server crashes the application is still up and served by the other servers in the cluster.
5. When appropriate load balancing algorithm is used, it brings optimal and efficient utilization of the resources, as it eliminates the scenario of some server’s resources are getting used than others.
6. Scalability: We can increase or decrease the number of servers on the fly without bringing down the application
7. Load balancing increases the reliability of your enterprise application
8. Increased security as the physical servers and IPs are abstract in certain cases.

## load balancers
which implements different types of scheduling algorithms and routing mechanisms.

1. Software load balancer
2. Hardware load balancer

## Load balancing algorithims
Random: This load balancing method randomly distributes load across the servers available, picking one via random number generation and sending the current connection to it. 

### Round Robin:
Round Robin passes each new connection request to the next server in line, eventually distributing connections evenly across the array of machines being load balanced. 

### Weighted Round Robin (called Ratio on the BIG-IP):
With this method, the number of connections that each machine receives over time is proportionate to a ratio weight you define for each machine.

### Dynamic Round Robin (Called Dynamic Ratio on the BIG-IP):
is similar to Weighted Round Robin, however, weights are based on continuous monitoring of the servers and are therefore continually changing.

### Fastest:
The Fastest method passes a new connection based on the fastest response time of all servers.

### Observed:
The Observed method uses a combination of the logic used in the Least Connections and Fastest algorithms to load balance connections to servers being load-balanced

### Least Connections: 
With this method, the system passes a new connection to the server that has the least number of current connections.

### Predictive:
The Predictive method uses the ranking method used by the Observed method, however, with the Predictive method, the system analyzes the trend of the ranking over time, determining whether a servers performance is currently improving or declining.

# Tasks
0. Double the number of webservers
mandatory
In this first task you need to configure web-02 to be identical to web-01. Fortunately, you built a Bash script during your web server project, and they’ll now come in handy to easily configure web-02. Remember, always try to automate your work!

Since we’re placing our web servers behind a load balancer for this project, we want to add a custom Nginx response header. The goal here is to be able to track which web server is answering our HTTP requests, to understand and track the way a load balancer works. More in the coming tasks.

Requirements:

Configure Nginx so that its HTTP response contains a custom header (on web-01 and web-02)
The name of the custom HTTP header must be X-Served-By
The value of the custom HTTP header must be the hostname of the server Nginx is running on
Write 0-custom_http_response_header so that it configures a brand new Ubuntu machine to the requirements asked in this task
Ignore SC2154 for shellcheck

1. Install your load balancer
mandatory
Install and configure HAproxy on your lb-01 server.

Requirements:

Configure HAproxy so that it send traffic to web-01 and web-02
Distribute requests using a roundrobin algorithm
Make sure that HAproxy can be managed via an init script
Make sure that your servers are configured with the right hostnames: [STUDENT_ID]-web-01 and [STUDENT_ID]-web-02. If not, follow this tutorial.
For your answer file, write a Bash script that configures a new Ubuntu machine to respect above requirements

2. Add a custom HTTP header with Puppet
#advanced
Just as in task #0, we’d like you to automate the task of creating a custom HTTP header response, but with Puppet.

The name of the custom HTTP header must be X-Served-By
The value of the custom HTTP header must be the hostname of the server Nginx is running on
Write 2-puppet_custom_http_response_header.pp so that it configures a brand new Ubuntu machine to the requirements asked in this task
