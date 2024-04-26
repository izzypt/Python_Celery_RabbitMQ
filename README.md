# Python_Celery_RabbitMQ

Celery and RabbitMQ are two powerful tools often used together in the realm of distributed computing and task queue management, especially within the Python ecosystem.

 > Distributed computing refers to the use of multiple computers or nodes working together in a network to solve a computational problem or perform a task. Instead of relying on a single powerful machine, distributed computing distributes the workload across multiple machines, which can be located in different geographical locations.

> Task queue management involves managing a queue of tasks that need to be executed asynchronously by one or more workers. It provides a mechanism for distributing, prioritizing, and executing tasks in a controlled manner.

### Let's understand (queues/message queueing)

This video explain very well the below:
  - https://www.youtube.com/watch?v=5-Rq4-PZlew

- A queue is a line of things waiting to be handled. Starts at the beggining of the line and is processed in sequential order.
  - Like a queue of people or cars:
  - ![image](https://github.com/izzypt/Python_Celery_RabbitMQ/assets/73948790/9d53f021-3947-4793-a1ef-f0a26d03bbf3)
- A message queue also called a message broker is a queue of messages placed between 2 parts of the system, in order for them to communicate with each other:
  - ![image](https://github.com/izzypt/Python_Celery_RabbitMQ/assets/73948790/d3e667c9-8f87-4441-b73e-8fbf85b5a8ca)
  - A message is the data transported between the sender and receiver.
  - An example of a message could be a party of the system, telling another part of the system to start a task (an image scaling request or logs that should be stored).
  - <img width="1411" alt="image" src="https://github.com/izzypt/Python_Celery_RabbitMQ/assets/73948790/96643edb-4039-44bb-ab62-7125ae5e688e">

### The basic architecture of a message queue

- Producers create messages and  and deliver them to the message queue.
- Consumers connect to the queue and subscribe messages from the queue.
- Messages placed onto the queue are stored until the consumer acknowledge them (i.e, the consumer tells the message broker that the message has been received or handled).

A message queue provides an asynchronous communication protocol, meaning that one system puts a message onto a message queue and does not require an immediate response to  continue processing.


### What is Celery? 
(https://www.youtube.com/watch?v=hFIkEGtW6vE - high level overview)
<img width="1120" alt="image" src="https://github.com/izzypt/Python_Celery_RabbitMQ/assets/73948790/b4377ce3-f102-4c42-9519-eb4c789cf363">


- Celery is a distributed task queue framework for Python, which allows you to run asynchronous tasks in a distributed manner across multiple workers. 
- These tasks can be anything from small data processing operations to complex, long-running computations.
- Some important concepts in celery are:

  - <ins>Tasks</ins>:
    - Tasks are units of work that you want to execute asynchronously.
    - They can be defined as simple Python functions decorated with ```@celery.task``` or as classes implementing the ```celery.Task``` interface.

  - <ins>Workers</ins>:
    - Workers are processes that execute tasks.
    - Celery supports multiple types of workers, including regular workers for executing tasks, beat workers for handling periodic tasks, and more.

  - <ins>Brokers</ins>:
    - Celery requires a message broker to handle the communication between the client and the workers.
    - This is where RabbitMQ comes into play.

  - <ins>Schedulers</ins>:
    - Celery supports periodic tasks, which are managed by a scheduler.
    - The default scheduler in Celery is Celery Beat.
   
  - <img width="1465" alt="image" src="https://github.com/izzypt/Python_Celery_RabbitMQ/assets/73948790/28b5f0b9-2448-45c6-8c0f-187d179f3968">

   
### Why use Celery? 

- Celery simplifies the process of distributing tasks across multiple workers, making it easier to scale your application horizontally.
- It helps in decoupling different parts of your application, allowing for better scalability and fault tolerance.
- Additionally, Celery provides monitoring and management tools to monitor the status of tasks and workers.

### What is RabbitMQ? 

- RabbitMQ is a message broker that implements the Advanced Message Queuing Protocol (AMQP). 
- It acts as a middleman between producers and consumers of messages, allowing them to communicate asynchronously and reliably.
- Some important concepts in RabbitMQ are:

  - <ins>Queues</ins>:
    - Queues are the basic building blocks of RabbitMQ.
    - They store messages that are sent by producers and consumed by consumers.
  - <ins>Exchanges</ins>:
    - Exchanges receive messages from producers and route them to one or more queues based on routing rules defined by the exchange type.
  - <ins>Bindings</ins>:
    - Bindings define the relationship between exchanges and queues, specifying which queues should receive messages from which exchanges.
  - <ins>Consumers</ins>:
    - Consumers are applications that receive and process messages from queues. 
