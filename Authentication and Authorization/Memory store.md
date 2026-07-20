
	Browser

		↓

	Cookie (Session ID)

		↓

	Node.js Server

		↓

	Memory (RAM)

		↓

	Session Data
	
	
`example`

	Load Balancer
	
	      │
	 ┌────┴────┐
	 │         │
	Server A  Server B



-  Login happened on Server A.

-  Next request goes to Server B.

-  Server B doesn't have the session.

-  User appears logged out.