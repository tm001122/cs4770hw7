# Assignment 7
## Introduction
Your task is to utilize Wireshark to snoop on a tcp connection between the provided executable and a remote server.
- You can initiate the tcp connection by executing the provided file with your Ohio ID as a command line argument. 

- The response will be a 64x64 greyscale image encoded as a png. Each 8 byte chunk of the data stream is further encoded by being x'ored with your OU id.

- Each byte of the response is read and then immediately discarded by the client. 

- I compiled the client with the same hardware as assignment 6 but I used rust and compiled in release mode which enables optimizations. You can use a VM, WSL, or the lab machines to run the executable if you only have access to windows.

- If you provide an invalid id the server will write 404 null (00000000) bytes (every valid image many more bytes than 404).

- A unique image has been uploaded for each student.

## Deliverables
- Submit your unique image as a png. (60%)
- Submit a link to a short youtube video showing you running wireshark and viewing the bytes and then explaining the process. (40%)

## Block encoding
- For each of the 8-byte blocks
-  z  k  2  5  0  6  1  8 -> convert to ascii 
- 7A 6B 32 35 30 36 31 38 xor'ed with
- 01 af 00 ad 0d 11 12 99 equals
- 7b c4 32 98 3d 27 23 a1
-  0  1  2  3  4  5  6  7 (byte indices)

- The last block may be less than 8 bytes, however the encoding pattern remains the same (byte n of the is xor'ed with byte n of your OU id.)

- To retrieve the original image repeat the xor operation for each block.
- You should receive a png file that is able to be opened by a regular image viewer.
