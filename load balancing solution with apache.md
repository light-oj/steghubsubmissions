## Load Balancer Solution with Apache

After completing Devops Tooling Website Solution, we might wonder how a user will be accessing each of the webservers using 3 different IP addresses or 3 different DNS names. We might also wonder what the point of is having 3 different servers doing exactly the same thing.

When we access a website in the Internet we use an URL and we do not really know how many servers are out there serving our requests, this complexity is hidden from a regular user, but in case of websites that are being visited by millions of users per day (like Google or Facebook) it is impossible to serve all the users from a single Web Server (it is also applicable to databases, but for now we will not focus on distributed DBs).

Each URL contains a domain name part, which is translated (resolved) to IP address of a target server that will serve requests when opening a website on the Internet. Translation (resolution) of domain names is performed by DNS servers.

### Load balancing

It refers to efficiently distributing incoming network traffic across a group of backend servers, also known as a server farm or server pool. Modern high‑traffic websites must serve hundreds of thousands, if not millions, of concurrent requests from users or clients and return the correct text, images, video, or application data, all in a fast and reliable manner. To cost‑effectively scale to meet these high volumes, modern computing best practice generally requires adding more servers.

#### A load balancer

Acts as the “traffic cop” sitting in front of your servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximizes speed and capacity utilization and ensures that no one server is overworked, which could degrade performance. If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it.

In this manner, a load balancer performs the following functions:

*   Distributes client requests or network load efficiently across multiple servers
*   Ensures high availability and reliability by sending requests only to servers that are online
*   Provides the flexibility to add or subtract servers as demand dictates

![Load Balancing](https://user-images.githubusercontent.com/117458922/224293449-60d241ca-936c-4bdb-b33f-374f0ceee9bf.png)

### Difference between L4 and L7 Load Balancing

*   L4 load balancing offers traffic management of transactions at the network protocol layer (TCP/UDP). L4 load balancing delivers traffic with limited network information with a load balancing algorithm (i.e. round-robin) and by calculating the best server based on fewest connections and fastest server response times.
*   L7 load balancing works at the highest level of the OSI model. L7 bases its routing decisions on various characteristics of the HTTP/HTTPS header, the content of the message, the URL type, and information in cookies.

## Project Overview

In this project we will enhance our Tooling Website solution by adding a Load Balancer to disctribute traffic between Web Servers and allow users to access our website using a single URL.

![3-tier](https://user-images.githubusercontent.com/117458922/224294190-c89f52ab-f218-400b-91ff-b1901c5aa86c.png)

## Task

We will deploy and configure an Apache Load Balancer for Tooling Website solution on a separate Ubuntu EC2 instance. We will make sure that users can be served by Web servers through the Load Balancer. We can implement this solution with 2 Web Servers for simplicity, the approach will be the same for 3 and more Web Servers.

## Prerequisites

Make sure that we have the following servers installed and configured within Devops Tooling Website Solution:

*   Two RHEL8 Web Servers
*   One MySQL DB Server (based on Ubuntu 20.04)
*   One RHEL8 NFS server

![project print](https://user-images.githubusercontent.com/117458922/224294823-ec4e5fae-b5f0-4d15-b20e-51e589ddfad4.png)

## Configure Apache As A Load Balancer

*   Create an Ubuntu Server EC2 instance and name it "Project-8-Apache-lb".  
    ![](https://lh7-us.googleusercontent.com/docsz/AD_4nXc4ZRp0mkBRfhKE55xCz6SJLJrkmABtXkdxj3DvW93opWhG9hYicfK_zMptrvbNyvG8fbohRPUWi3fvc8TrttodFNE7HJV86dkXfxVphZ4p-BOv73mD16LTe8ty5QDw-YwG_jlnCuNCbNVbFjHiPy0T1mLk?key=B6irPpQmShp_r_W9yTcJ0g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfKyjntnuIV5vLHqonkdehUBA1FUYZb4CuZxUhWN0WwEJQ8ay1gOezfFld4YQJ2J2I3YTewxqvYsIthnrTkSKyn-wx6ohANVzbw2BFmuIrNgVt7SJ0Ec0Hd8iFu1q1ZSbuy-m8tDDcyN-CKjmAx11LYF59E?key=B6irPpQmShp_r_W9yTcJ0g)

*   Open TCP port 80 on Apache-lb by creating an Inbound Rule in Security Group.
*   Install Apache Load Balancer on Project-8-apache-lb server and configure it to point traffic coming to LB to both Web Servers

## Install apache2

`sudo apt update`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdM-vLI52eE_RxQkslTJmDpWKff2SWipoLYibtcoY4AAl3mEphhC1bd5OAy20BkKHgjStOY8RulcihyhE6VvvX6IZXLu7ZV4D1pnaYtwYDy-3OA-eo6D_3eMkKQyz8QDhaiD_Q-rfq0MIzwD1n1uuu2Hx4?key=B6irPpQmShp_r_W9yTcJ0g)  
`sudo apt install apache2 -y`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe8y85X-K9BwNJ5hhtkeBB4O1Jr2j0HYrlhdRBdRyG2E5wkA1zkqe_Bym0pTs_VGqUNuulZTK910xBhX-7croShgzM51BzdjFP9wptURp5aVAn01zxaRgqwvk9Xw5x9IkH84HgaFSo62PjBwL8n7l-Vsgk?key=B6irPpQmShp_r_W9yTcJ0g)  
`sudo apt-get install libxml2-dev`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeBti3s0PdISloIIQx-miymTvEEEFhaFzABEAoypn_jD4Lga5QYGng4kd9l0Krj6d4LQmK1refwbL7lhjjzBVhSWifTihagd2d4BAs31PLeVY6rU0bH7Awdb9cOep5yBBiKQShqQKGMdvaoECxHB9YhmOyN?key=B6irPpQmShp_r_W9yTcJ0g)

## Enable following modules:

`sudo a2enmod rewrite`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdd6Qcqngx0tZ9fZxpnlpUI-2-vMKFgM9fLqS4wXVKize3QI1_3HlAsw1dsvVkpFVUfnld8t6_krtrrm1_riu7u9XasSXfEBXt9MhuMC8w8aMSfZo1rrPCQTtfo6_rLOATIQ9Tmb9RW63W4YRMglXxBpA3w?key=B6irPpQmShp_r_W9yTcJ0g)  
`sudo a2enmod proxy`  
`sudo a2enmod proxy_balancer`  
`sudo a2enmod proxy_http`  
`sudo a2enmod headers`  
`sudo a2enmod lbmethod_bytraffic`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe8Z-E7T1yrqMqh5udRp86f-clV_XRNrNfAimxqcX0EeqPvYMYFHN_Se4L-XRv0ZrsKSkdqJH9rkFtrdJAN6USa2BtMlEjzvzvWE4BLw32Uh_KPM4V4EeESGegcpXjUS37xFYm2qFEbLJL6j3Iz3c8lsQA?key=B6irPpQmShp_r_W9yTcJ0g)

## Restart apache2 service

`sudo systemctl restart apache2`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfF4d-HpzBOVPiW8bM16Dtn7v6nbMeo1XPoRaRUS6j7zbgB1yjruvlyqvOUJRL9xwxMi8IyfmW7LfjRGcg-n_pRai4XFzvptHccxwTWkh7efA4AZUKZnJop1c7owPKw8-GqCV6oLJyVFSQME3bUWJYbo_Ul?key=B6irPpQmShp_r_W9yTcJ0g)

## Configure Load Balancing

`sudo vi /etc/apache2/sites-available/000-default.conf`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfD1EExXs3YRFZxfJIW-As2pr1kzgtDdLnAKon3PNl-1LT2AduDZv00KVcd6cul82QvbFndOZvZdffQgSOSOAHNZlgYk_WyJa-325s8qIgvMJE4TZ8C2XCaSEGyVAdVFS_W2AzHrD84U1tIy4FUQ6BoW4dL?key=B6irPpQmShp_r_W9yTcJ0g)

*   Add this configuration into this section \<VirtualHost \*:80>  

```plaintext
<Proxy "balancer://mycluster">  
              BalancerMember http://<WebServer1-Private-IP-Address>:80 loadfactor=5 timeout=1  
              BalancerMember http://<WebServer2-Private-IP-Address>:80 loadfactor=5 timeout=1  
              ProxySet lbmethod=bytraffic  
              # ProxySet lbmethod=byrequests  
       </Proxy>

       ProxyPreserveHost On  
       ProxyPass  balancer://mycluster/  
       ProxyPassReverse  balancer://mycluster/  
```

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeVH2k4MvixsHnEBr4hht0rSa3ZEmkt4TWSdgITOSmkrPYmQxczSQ5pDmycVlI0yMijN_YED7ig1j5AF77hWGQ0ZOaVaRosFVIxrY0GkVYpW-Kd9Ah5NZjIVTGqOvn09bg-YFz9vtBfA34S9WO2-aOY_GB9?key=B6irPpQmShp_r_W9yTcJ0g)

*   Restart apache server

_bytraffic balancing method will distribute incoming load between your Web Servers according to current traffic load. We can control in what proportion the traffic must be distributed by loadfactor parameter._

*   Verify that our configuration works - try to access your LB’s public IP address or Public DNS name from your browser:

```plaintext
http://<Load-Balancer-Public-IP-Address>/index.php  
```

![image1](https://user-images.githubusercontent.com/117458922/224343812-c15ba5ee-51ac-4e75-b324-550b2bce69bb.png)

![image2](https://user-images.githubusercontent.com/117458922/224343871-f4bbfbe1-2e61-4972-8dd4-935ac3b60f4c.png)

_Note: If in the Devops Tooling Website Solution we mounted /var/log/httpd/ from our Web Servers to the NFS server - unmount them and make sure that each Web Server has its own log directory._

Open two terminal consoles for both Web Servers and run the following command:

```plaintext
sudo tail -f /var/log/httpd/access_log  
```

*   Try to refresh your browser page http://index.php several times and make sure that both servers receive HTTP GET requests from your LB – new records must appear in each server’s log file. The number of requests to each server will be approximately the same since we set loadfactor to the same value for both servers – it means that traffic will be distributed evenly between them.

_If all is properly configured, our users will not even notice that their requests are served by more than one server._

## Optional Step - Configure Local DNS Names Resolution

Sometimes it is tedious to remember and switch between IP addresses, especially if we have a lot of servers under our management. What we can do, is to configure local domain name resolution. The easiest way is to use /etc/hosts file, although this approach is not very scalable, but it is very easy to configure and shows the concept well. So let us configure IP address to domain name mapping for our LB

*   Open this file on our LB server

`sudo vi /etc/hosts`

*   Add 2 records into this file with Local IP address and arbitrary name for both of our Web Servers

`<WebServer1-Private-IP-Address> Web1`  
`<WebServer2-Private-IP-Address> Web2`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcla1ug5UDkqXVVmbM0-QJj9M2I0uhre6Xv2Whd_A4zw6I3PVkE6y2NzDkJa25VgZpYzGf8Gr14uCeXCdtcraI3mF4O-Z2CW117wlzz8abKFOBRfz6gr6RYCv_kj7elix3R3jyI92aBv8x4P-BclmkPxOE?key=B6irPpQmShp_r_W9yTcJ0g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe_YeEatP3ZnqzB25okhqX29CqL9MeZPvvMzpy7wWJQZkTqgbJymMB9RT4H41MgSkxptb7cL1ZdP3CxrIs2QAi058V6lS83Aq1_EwDIVIRYB5EiTYlcd8TME8SZoEaabAc4v7dkkxcRiCG5kdF99KGLoJ_v?key=B6irPpQmShp_r_W9yTcJ0g)

*   Now we can update your LB configuration file with those names instead of IP addresses.

`BalancerMember http://Web1:80 loadfactor=5 timeout=1`  
`BalancerMember http://Web2:80 loadfactor=5 timeout=1`  
![](https://lh7-us.googleusercontent.com/docsz/AD_4nXevLgpO5nhbC-Syhxt9AVC0AvAOjKlKXdWDRHKwXN7lM8HShunwWvgxRs6bfWILOAEOO9GjQqyDFVUZrw8QchEqjw1zp8Qmo7EnAO32vXAExnNAKp7iBtFua_P42iEPPJdMWfAx4bRdVQuo4JFUgTapgqKA?key=B6irPpQmShp_r_W9yTcJ0g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdXip--wYzjI_eu2c9enl_s_8vZ62g_kPN8DbDiwk0U7UttokHkjhOYAenZJUHbe6tNd4fRndIsBWuiiFKKFHmLaxuqADh9vSYW6sj0Zt0pPZ6hD5_yF6TrvOAOHeiX4P70YtaTkJaeBREHbe99zgSbEENL?key=B6irPpQmShp_r_W9yTcJ0g)

*   We can try to curl our Web Servers from LB locally: curl http://Web1 or curl http://Web2 - it will work.
*   Remember, this is only internal configuration, and it is also local to our LB server, these names will neither be ‘resolvable’ from other servers internally nor from the Internet.

_We just finished the Apache Load Balancer on our Ubuntu Server, and the architecture looks like the diagram below._

![Apache LB](https://user-images.githubusercontent.com/117458922/224347492-dc03855b-feab-42a9-bdbe-73a561170681.png)
