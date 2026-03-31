[Video](https://www.youtube.com/watch?v=bwt09KXDH94&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=1)

System Design is basically the process of planning and structuring how a software system works at scale how different parts (servers, databases, APIs, etc.) interact to handle users, data, and traffic efficiently.

Types of storage:
- HDD/SDD - lasts until broken (physically)
- RAM - Temporary 
Wanna keep data, use HDD

When it comes to storing data, you would not use an application servers for data storage
- no one should host data on a VM in form of some regular files 
- too much going on with the OS, resource management
- bad for requests from multiple clients
- no separation of concern between data storage and app server 
- cannot scale

Clients requests to the application servers are a typical bottle neck, so if you add on some data handling to it, it will suck even more

We use a Data Base (DB) → Dedicated Computer for storage → stores all the needed data for the application (but one DB is not enough for fault tolerance and other problems that we will face at scale)

→ Reason for this whole video series