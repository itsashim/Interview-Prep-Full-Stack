# Streams

Used to process (read and write) data piece by piece (chunks), without completing the whole read or write operation, and therefore without keeping all the data in memory
eg:- netflix /youtube

- perfect for handling large volumes of data for eg vide
- more efficient dataprocessing in terms of memory (no need to keep all data in memory) and time (we don't have to wait until all the data is available)

# there are four fundamental types of stream
- readable stream
- writable stream
- duplex stream
- transform stream