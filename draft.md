#  mapreduce

## preprocess
Generate random initial input files $\text{input.txt}$

##   mapreduce

###  `split_init_input`
Preprocessing before calculation: divide $\text{input.txt}$ into $m$ (number of map nodes) sub-files $\text{input0.txt},\cdots,\text{input(m-1).txt}$

### `master_node_task`
The master node creates threads that execute map tasks and reduce tasks, and checks whether their respective outputs are complete. If they are incomplete, restart the corresponding tasks.




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTQzNjE4MjQsMjk0ODc3MzgwLDYxMT
A1MjUyMywtMjEyMTA1OTYyMywtMTY0Njg1MDQwLC0xNTAyNzE5
NzUyLC0xMzQzNTA2NTE1LC0yMDg4NzQ2NjEyLC0xNTAzNDEyMD
I5LC04Mzc2NTE3NDYsLTUyNzc5NTQ1NCwtODM4MDMzODkwLC0x
OTIyOTYzMTcwLDEyMzcyOTIxODUsMTc3NjAxMTEwMyw4MzMxOD
E4OTcsMTg1NjgyODI5MV19
-->