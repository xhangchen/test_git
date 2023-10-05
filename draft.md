#  mapreduce

## preprocess
Generate random initial input files $\text{input.txt}$ .

##   mapreduce

###  `split_init_input`
Preprocessing before calculation: divide $\text{input.txt}$ into $m$ (number of map nodes) sub-files $\text{input0.txt},\cdots,\text{input(m-1).txt}$ .

### `master_node_task`
The master node creates threads that execute map tasks and reduce tasks, and checks whether their respective outputs are complete. If the output of a task is incomplete, the master node restarts the corresponding task.


## cmp_serial_method

Record the time taken by the ordinary linear scan method
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1NzM3MzAyNiwyOTQ4NzczODAsNjExMD
UyNTIzLC0yMTIxMDU5NjIzLC0xNjQ2ODUwNDAsLTE1MDI3MTk3
NTIsLTEzNDM1MDY1MTUsLTIwODg3NDY2MTIsLTE1MDM0MTIwMj
ksLTgzNzY1MTc0NiwtNTI3Nzk1NDU0LC04MzgwMzM4OTAsLTE5
MjI5NjMxNzAsMTIzNzI5MjE4NSwxNzc2MDExMTAzLDgzMzE4MT
g5NywxODU2ODI4MjkxXX0=
-->