# SAAS based Raspberry Pi App deployer

We can provide this product as a service to customers who just need to register their Raspberry Pi clients from any location (different networks - private/public). After registration they can send deploy requests through our app link and check status for the deployment. We can upgrade the server with regular updated code as the customers will not have any control over the servers.

Requirements :
Please run "pip install backports.tempfile" command before running the client code on Pi.



App link:  https://104.196.235.71/  
SSL is enabled on nginx with self signed certificate. So we need to use https in the url.

Architecture Diagram :  

![Architecture-Overview-Diagram](/Architecture-Overview-Diagram.png "Architecture diagram")

To see list of Pi's connected double click client IP filed in UI. 
whenever client code is run on PI, it first registers itself to the rabbit server which in turen creates a queue for the client on which requests are sent. The client continuously listens on its queue for requests.
To find your public repositories click "Find"

![Homepage](/Homepage.png "Home page")

You need to authorize your app on github before you deploy.

![Authorize](/authorize%20app.png "Authorize")

Sending deploy request for the first time creates a webhook on the repository, installs packages under requirements.txt and runs the app.
Whenever commits are made to the repository, webhooks get triggered, and the packages get installed again and the app is run again.

![Webhook](/webhook.png "Webhook")

You can see the request added to the queue on RabbitMQ dashboard when we send request.  
You can also check the status of the request by Client IP by clicking check status or by just refreshing after deploy request.
