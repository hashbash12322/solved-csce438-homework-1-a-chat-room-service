Download Link: https://assignmentchef.com/product/solved-csce438-homework-1-a-chat-room-service
<br>
<h1>1           Overview</h1>

The objective of this assignment is to build a <strong>Chat Rooms Service</strong>. The system can have several Chat rooms, and clients join chat rooms by issuing JOIN commands. Clients can also create, list and delete chat rooms remotely by issuing CREATE, LIST and DELETE commands. All communication between chat rooms and chat clients will be using a socket interface.

<h2>1.1         Chat Room Server</h2>

The program/process implementing the <strong>Chat Room Server </strong>(call it crsd) would do the following steps in a loop, in any order:

<ul>

 <li>Listen on a well-known port to accept CREATE, DELETE, LIST or JOIN requests from Chat clients.</li>

 <li>For a CREATE &lt;chatroom name&gt; request, check whether the given chatroom exists already. If not, create a new master socket (careful about picking the port number!) Create an entry for the new chat room in the local database, and store the name and the port number of the new chat room. Inform the client about the result of the command.</li>

 <li>For a JOIN &lt;chatroom name&gt; request, check whether the chat room exists. If it does, return the port number of the master socket of that chat room and the current number members in the chat room. The client will then connect to the chat room through that port.</li>

 <li>For a LIST request, return the names of all chatrooms.</li>

 <li>For a DELETE &lt;chatroom name&gt; request, check whether the given chatroom exists. If it does, send the warning message “chat room being deleted” to all connected clients before terminating their connections, closing the master socket, and deleting the entry. Inform the client about the result.</li>

 <li>Incoming chat messages are handled on slave sockets that are derived from the chat-room specific master socket. Whenever a chat message comes in, forward that message to all clients that are part of the chat room.</li>

 <li>Clients leave the chat room by (unceremoniously) terminating the connection to the server. It is up to the server to handle this and manage the chat room membership accordingly.</li>

</ul>

<h2>1.2         Chat Room Client</h2>

The program/process implementing the <strong>Chat Room Client </strong>(call it crc) would issue requests to and exchange messages with the chat room server. The client program takes the host name and the port number of the chat room server as first and second command line argument, respectively. The client program provides a simple command line interface of your design, which reads both commands to create, delete, or join chat rooms, and messages to the currently joined chat room.

The chat room client would create, delete, and join chat rooms in the following way:

<ul>

 <li>To create a chat room, connect to the well-known port of the chat server, and send a CREATE &lt;chatroom name&gt; Display the reply and close the connection.</li>

 <li>To delete a chat room, connect to the well-known port of the chat server, and send a DELETE &lt;chatroom name&gt; Display the reply and close the connection.</li>

 <li>To list all chat rooms, connect to the well-known port of the chat server, and send a LIST Display the reply and close the connection.</li>

 <li>To join a chat room, connect to the well-known port of the chat server, and send a JOIN &lt;chatroom name&gt; Read the information with the port number of the chat room and the current number of members. Display the information.</li>

 <li>If the JOIN operation was successful, connect to the port returned by the server, and begin exchanging messages.</li>

 <li>Leave the chat room by terminating the connection.</li>

</ul>

<strong>Note: </strong>There is a little complication, as the client program has to read input both from the command line and from the connection to the chat room. You have to find a solution to handle this. (One way is to use separate threads to handle the two input sources, or you can simply use select() to handle them in a single-thread solution.)

<h1>2           What to Hand In</h1>

The running system will consist of the chat room server (crsd) and the chat room client (crc). As platform, you should be using linux workstations, and develop the program in C/C++.

<h2>2.1         Design</h2>

Before you start hacking away, plot down a design document. The result should be a system level design document, which you hand in along with the source code. Do not get carried away with it, but make sure it convinces the reader that you know how to attack the problem. List and describe the components of the system: Chat Client Program, Chat Room Server Program, and their interaction. In particular, describe how you implement the server program (iterative, multi-threaded using thread, multi-threaded using processes, multi-threaded using select(), others.)

<h2>2.2            Source code</h2>

Hand in the source code, comprising of a:

<ul>

 <li>Makefile</li>

 <li>a file c or crsd.C</li>

 <li>a file c or crc.C</li>

 <li>README file that explains how to compile the program and run it</li>

</ul>

The code should be easy to read (read: well-commented!). The instructor reserves the right to deduct points for code that he/she considers undecipherable.

Points will be give as follows: 5 pts (design document), 5 pts (compilation), 40 pts (5 test cases – details on the exact inputs and outputs will be provided in class)