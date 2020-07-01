# Discussion note

### JUL 1st
* FPU
	* I have updated my forked composite repo with git rebase, created a pull request within my forked composite repo between ppos and ekf branch to check what to update in my ekf branch.
	* I will close my previous pull request to gwsystems/composite, and make a new pull request. 
 		* Question: My ekf branch contains the lib-ekf and related modifications. Do I need to remove the lib related files and only keep the kernel part fpu modifications and unit tests?
*  Multi-process LINUX server
	* I learned from Wenyuan that UDP will not affect the result a lot comparing with TCP in our simulation environment. I will use int array to keep track the pid-port relation in the UDP server.
