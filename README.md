# CS204-UCP-projectWe implemented Utility Based Partitioning using the following files:
1)ucp.llc_repl
We have created a separate file under replacement folder to implement ucp based
partitioning.First we implemented static partitioning where we divided 16 ways into 2
different core partitions and maintain two variables that kept the count of the present
number of blocks belonging to a particular core and accordingly a victim was selected.
For eg. we used the traces GemsFDTD_716B.trace.xz , gobmk_135B.trace.xz
Functions and methods used inside ucp.llc_repl
ATD class :
Firstly , we initialized a class for Auxiliary Tag Directory , this class contains tag, validbit
value ,lru status and cnt variable.Also we defined a method ATD() to initialize all values
of ATD class to 0 and lru to maximum.
1.a llc_find_victim:
->We maintained 2 counters ctr1 and ctr2 that checked the count of
number of blocks in each core respectively and the victim was selected
according to the quantity of blocks,we chose the one to be evicted.We also
changed the ATD parameters upon finding the victim block.
1.b llc_update_replacement_state
-> If the block available belong to the dynamic sample set of 32
random sets we selected, we wil check whether any set is available
i.e. has valid bit 0 and insert the block in it, otherwise if all the blocks
have valid bit 1 , we would check for a hit or miss by matching tag with
block address and return set%32 so that set belongs in range of dss.
Thus we can verify if replacement is needed (lru=0 if hit and all other
lru values incremented).Moreover we will increment counter values in
ATD parameter for every hit.
