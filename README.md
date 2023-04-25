# CS-3053-Project-3-File-system-interface-multiprogramming-support-and-memory-management-

Task 1: Implement the file system calls (creat, open, read, write, close, and unlink)

I started by implementing system calls in the UserProcess file. The handleCreate method
was implemented by checking for a valid address input, assigning the file a name, checking if the
file name is valid, and finding a place to input the new file in the file list. The handleOpen
method uses the same logic as the create method. The handleRead method checks for valid input,
then assigns a temporary variable to the file item, then writes bytes to the memory until all of the
bytes in the file are read. handleWrite uses the same logic as read, but it acquires a lock before
and after each byte is written. handleClose was implemented by checking for valid input, then
returns 0 if the file was successfully closed. handleUnlink returns 0 if the file was successfully
unlinked.

Then, I implemented system calls in the UserKernel. The createFile method inserts the
file name into the file manager if the file name is not already in use. openFile creates a new file if
the file name is not in the file manager, otherwise it restores the machine status. closeFile
removes the file name from the file system and the file manager if the file is unlinked and its
byte count is 0. unlinkFile removes the file name from the file system and file manager is the
file’s byte count is 0.

Task 2: Implement support for multiprogramming

For this task I had to make efficient use of memory by implementing
writeVirtualMemory, translate, and modify loadSections within the UserProcess. There are
multiple writeVirtualMemory metods but the one I implemented takes an int, byte[], int, and int
as the input. I set the length of the data, then gave each page a physical address, and finally
returned the number of bytes transferred. Translate allocates the machine’s physical memory by
validating the input then returning the size translated into bytes. I modified loadSections by
acquiring a lock from the UserKernel, checking for a valid page number, then inserting pages
into the page table before loading sections.

Task 3: Implement the system calls (execute, join, and exit)

This task was completely implemented within UserProcess. handleExec checks that each
input is valid, reads bytes into the virtual memory, then converts the bytes into an int then to a
string, then runs a child process. handleJoin runs a child process, then acquires the exit status,
then writes to the virtual memory. handleExit interrupts the machine and runs a parent process,
then terminates the kernel when the process is over.
