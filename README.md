pdupes - A multithreaded duplicate file checker in Python

My very first program in Python. Alas, using multiple threads for directory
scanning and hashing of chunks bring only a limited speed benefit. Most likely
due to the Python Global Interpreter Lock (GIL). The speedup comes from having
multiple threads waiting for their I/O completion.

The program works like this:
 - Scan all directories and subdirectories given
 - Put all regular files size and dev:inode pairs in a dict
 - Repeat until no more files:
   - Remove all filesizes that have only dev:inode pair
   - Hash a chunk from the other filesizes
   - Count the number of hashes for each filesize
   - Remove files that have a unique hash chunk

