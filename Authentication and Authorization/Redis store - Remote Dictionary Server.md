
- ***Redis is an in-memory data store that stores frequently accessed data in RAM for very fast access.
  
  - ***By default, Redis stores data in RAM. If persistence is not enabled, data is lost after a restart. Redis can also be configured to persist data to disk.***
  
  - ***Redis stores data as key-value pairs instead of storing data in relational tables like SQL databases.***

 `example`:
 
	  Key              Value
	----------------------------
	user:101         Goushik
	session:abc123   {userId:101}
	otp:987654       123456

 `Flow`:

	Browser

		↓

	Session ID

		↓

	Node.js

		↓

	Redis

		↓

	Session Data
	


==**Every server accesses the same Redis.**


         Load Balancer

              │

        ┌────────┴────────┐

     Node.js A        Node.js B

        │              │

        └──────┬───────┘

               │

             Redis


  -  ***Now it doesn't matter which server handles the request.***

  -  ***All servers use Redis.***



