# Output showing the 3-tier deployment of website

## You can start the server in two ways:
1.	By using the IP address of the app01 server. And the default port number 8080 for the apache-tomcat service.
![app01(Tomcat-server)](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/app01.png)
2.	By using the IP address of the NGINX server which helps in load balancing with the default port number of 80.
![web01(Nginx-server)](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/web01.png)

## Login with admin credentials 
> **Username - vp_admin**


> **Password - vp_admin**

## To check whether Rabbitmq server is running
### click on RabbitMQ tab to see the result:
![RabbitMQ](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/RabbitMQ.png)
### RabbitMQ validation
![RabbitMQ-result](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/RabbitMQ-result.png)
## To check whether Memcached server is running
### click on All Users tab to see the result:
![Memcache-1](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Memcache-1.png)
### Now to check whether caching works fine, click on any random user name.
![Memcache-2](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Memcache-2.png)
### Upon First request, the data is retrieved from the MySQL Database, and then inserted in cache memory.
![Memcache-3](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Memcache-3.png)
### After that click on same user name again, the response time will be less this time, since the data is retrieved from cache memory.
![Memcache-4](https://github.com/Kizhakkekkara-Vishnu-Vijayan/Sample/blob/master/images/Memcache-4.png)
**Note: _This happens because when the request is initiated for the first time by the user, the data is fetched from MySQL database. But when the same request is initiated by the user for the second time, the request is fetched from Memcache server and not from the database, since the response gets stored in the cached memory of Memcache server when the data is requested for the first time. This helps in reducing the load of the database._**
