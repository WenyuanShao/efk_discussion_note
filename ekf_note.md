# Discussion note

### JUL 1st
* FPU
	* I have updated my forked composite repo with git rebase, created a pull request within my forked composite repo between ppos and ekf branch to check what to update in my ekf branch.
		* (July 6th) Progress: Rebased all my previous commits into one commit and submitted the pull request to gwusystems/composite ppos branch.
	* I will close my previous pull request to gwsystems/composite, and make a new pull request. 
 		* Question: My ekf branch contains the lib-ekf and related modifications. Do I need to remove the lib related files and only keep the kernel part fpu modifications and unit tests?
		* Solved: I will create a new branch that does include the ekflib relation files.
		* (July 6th) Progress: Built a new branch to keep ekf lib related code, removed all ekf lib related stuff before submit the pull request.
*  Multi-process LINUX server
	* I learned from Wenyuan that UDP will not affect the result a lot comparing with TCP in our simulation environment. I will use int array to keep track the pid-port relation in the UDP server.
		* (July 6th) Solved: @Wenyuan Please correct me if my design below is wrong.
			* 1. Client sent a message to Server use the default port (e.g. 8080). 
			* 2. Server received the message from Client and assign a new port for this Client, e.g. Client A is the 1st client that trying to connect to the Server, Server will assign port number 8081 (= 8080 + 1) only for Client A. 
			* 3. Server fork a new process, whithin that process Server accept data use the new port.
			* 4. Client A received the new port number, and start sending data to Server using the newly assigned port.
### JUL 8th
*  Multi-process LINUX server
	* @Wenyuan challenged the my UDP server design recorded on July 6th.
		* Overhead when the Client trying to communicate with the Server, the Client needs to notice the server by sending a message to server, and wait for the message from the Server side before sending the data.
		* The suggested way to avoid the communication stage at the beginning:
			* 1. Use an int array to track the client port and pid. E.g. Client A use port N to send requests, the server checks whether this port has ever been sending requests before by looking up the pid-port int array. 
				* If pid[N] = 0, then Client A is the first time send request to Server, use fork() and record pid[N] = pid_number. 
				* Otherwise, according to the recorded pid_number in pid[N], put the data from Client A in a queue. 
			* 2. Each client occupies a queue, the corresponding process read the data from the related queue. 
			* 3. @Wenyuan does my understanding correct? 
	* Questions:
		* Does the server use only one parent process to receive requests, instead of using multi-process to receive requests?
		* Checking port number for each request can be considered a overhead?
		* Send the request from parent process to child process will have a big overhead or not?
		* Is there a way to avoid the inter process communication?
			
