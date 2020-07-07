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
		* (July 6th) Solved: 
			* 1. Client sent a message to Server use the default port (e.g. 8080). 
			* 2. Server received the message from Client and assign a new port for this Client, e.g. Client A is the 1st client that trying to connect to the Server, Server will assign port number 8081 (= 8080 + 1) only for Client A. 
			* 3. Server fork a new process, whithin that process Server accept data use the new port.
			* 4. Client A received the new port number, and start sending data to Server using the newly assigned port.
