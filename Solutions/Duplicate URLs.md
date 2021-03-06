### Solution

- Simple Answer: Use HashMap to detect duplicates
  - 10 billion URLS at 100 characters each at 4 bytes each = 4 terabytes of information. Can't save this all in 1 file.
  - Create 4000 1GB files called <x>.txt where <x> is hash(url) % 4000.
    - (Although mostly uniformly distributed, some files may be bigger or smaller than 1GB since it's very unlikely we can create a perfect hash function)
  - Now all URLs with same hash value are in same file
    - (this ensures that 2 of the same key are not in different files, so our next step will successfully remove all duplicates)
  - Do a 2nd pass (through each of the 4000 files) and create a HashMap<URL, Boolean> to detect duplicates
    - This 2nd pass can be done in parallel on 4000 Machines (Pro: Faster, Con: if 1 machine crashes it affects our final result)
