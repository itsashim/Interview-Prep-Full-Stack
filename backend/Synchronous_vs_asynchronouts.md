Blocking Vs Nonblocking

=> Synchronous basically means each statements is basically processed line by line and each line basically waits for the result of the prevous line. So it is also called as blocking code 

This can become a problem with slow operations


=> Asnchronous is no blocking code, the heavy work is is processed at the background and when the result is ready with the help of callback function is called to handle the result. and while doing this rest of the code can still be executed without blocking.

=> Node js is single thread, that means every user in your node application uses that thread so if it was not async
for one user heavy task every other user have to wait. 