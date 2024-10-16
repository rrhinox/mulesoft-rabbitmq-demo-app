# MuleSoft App RabbitMQ-Demo

### **Example of sending JSON data to an AMQP queue with MuleSoft Anypoint Studio** 

![image](https://github.com/user-attachments/assets/f088dca5-9462-478a-9c17-6bfaf2cdf221)   ![image](https://github.com/user-attachments/assets/5d81819f-6771-4d75-abd1-4ac6a37b96b9)   ![image](https://github.com/user-attachments/assets/791e32a9-4f9d-49e7-a992-f6972dd88d76)






---

### **What will we learn in this demo?** ###

1. Using MuleSoft Anypoint Studio
2. Create a project and a Mule App
3. We'll find out how to leverageAnypoint Exchange 
4. How to integrate MuleSoft with RabbitMQ. How?
   1. With Docker Desktop and RabbitMQ
   2. MuleSoft Anypoint Studio with AMQP Connector


### **Prerequisites:**

1. Have an account on **Anypoint Platform** to connect to the exchange  
2. Install **Docker** on your PC [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install/)   
3. Install **MuleSoft Anypoint Studio**, MuleSoft's integrated development environment (IDE). You can do downloads directly from Anypoint Platform (you will be emailed the link).  
   1. ![image](https://github.com/user-attachments/assets/709185b2-b3e1-4c55-b37d-35296de096f7)
 
4. Download a RabbitMQ image to launch a Docker container.   
   1. See below docker run command.  
5. Download HTTP client to perform test POST calls :  
   1. **Insomnia**, **Postman** o **cURL** [Download \- Insomnia](https://insomnia.rest/download)   
6. **AMQP Connector :**  [AMQP Connector](https://github.com/mulesoft/docs-connectors/blob/latest/amqp/0.3.9/modules/ROOT/pages/index.adoc#studio-plugin-1) 

## **RabbitMQ Docker** 

##
      docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management


RabbitMQ Admin console use “guest” default user/pwd only for dev environment  

Go To RabbitMQ console and follow the steps below : 

1. After making sure that RabbitMQ is running, log in to the RabbitMQ web admin console at 
##
      [http://localhost:15672](http://localhost:15672)
2. Go to the **Exchanges** tab and click on **Add a new Exchange** to create an exchange called **sales\_exchange**. You may leave the other feilds as they are and then click on Add exchange.  
3. Now go to the **Queues** tab and click on **Add a new queue** to create a queue called **sales\_queue**. You may leave the other fields as they are and then click on Add queue.  
4. Click on **sales\_exchange** under the **Exchanges** tab and then go to the section titled **Add binding from this exchange**. In the To queue field type in **sales\_queue** and then click on **Bind**.

## **Mule App**

1. Open Anypoint Studio and create **new Mule Project** (Allow permission on folder and connect your Anypoint Platform Account with your login credentials)  
2. Create a **rabbitmq-demo** project  
3. **Open Exchange Icon** under Edit Menu   
   <img width="413" alt="image" src="https://github.com/user-attachments/assets/62eb9ce7-50c7-4ea2-8fdf-ee3c0c95f1d8">
 
4. Search **AMQP Connector** from Exchange and **Import dependencies**   
5. Now **Add one HTTP Listener** define /publish path and use 8081 port   
6. Next **Add AMQP Publish** element and configure it like this   
   <img width="371" alt="image" src="https://github.com/user-attachments/assets/d0d9aacc-0b4b-4ffa-96a6-39d7616909ce">
  
7. Then **add the correct exchange name** binded previously 
<img width="373" alt="image" src="https://github.com/user-attachments/assets/13ba42ac-53e5-4984-b7e0-e6d4987bbf79">
 
8. Next **Add a Logger** connected after Publish element and **add a Message** to log console example \> “Messaggio pubblicato correttamente su RabbitMQ\!\!\!”  
9. At the end Run Mule Application  
10. Wait started message

## **HTTP Client Insomnia**

1. Download and launch Insomnia client and use a ScratchPad without registering an account.  
2. Create new HTTP Request like this and click Send : 

<img width="400" alt="image" src="https://github.com/user-attachments/assets/ad9db930-58eb-42ac-b0b8-ce5c2f3e9514">

3. At the end you should see into the "Console Log" tabs of your IDE, the Logger message configured previously on point 8. and then a queue message on RabbitMQ; From admin console of our RabbitMQ select the Queue **sales\_queue** and go to the **“Get Messages”** section then get the number of messages to get (1 it's ok now!).

<img width="336" alt="image" src="https://github.com/user-attachments/assets/545edcdb-2302-4abf-9a60-e94773ba9d81">


And that's it. It Works\! ✌️ 

Happy Integrations with Mule Runtime App!

![image](https://github.com/user-attachments/assets/f088dca5-9462-478a-9c17-6bfaf2cdf221)   !

---

### **Disclaimer** 

This project is released under the Apache License 2.0. The code and examples provided may be freely used and modified in accordance with the terms of this license.

All images belong to their respective owners and may be subject to restrictions or copyrights.