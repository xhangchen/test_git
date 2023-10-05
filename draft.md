#  mapreduce

## preprocess
Generate random initial input files $\text{input.txt}$

##   mapreduce

###  `split_init_input`
Preprocessing before calculation: divide $\text{input.txt}$ into $m$ (number of map nodes) sub-files $\text{input0.txt},\cdots,\text{input(m-1).txt}$

### `master_node_task`
The master node creates threads that execute map tasks and reduce tasks, and checks whether their respective outputs are complete. If the output of a task is incomplete, restart the corresponding task.




<!--stackedit_data:
eyJoaXN0b3J5IjpbNTc1NDUwOCwyOTQ4NzczODAsNjExMDUyNT
IzLC0yMTIxMDU5NjIzLC0xNjQ2ODUwNDAsLTE1MDI3MTk3NTIs
LTEzNDM1MDY1MTUsLTIwODg3NDY2MTIsLTE1MDM0MTIwMjksLT
gzNzY1MTc0NiwtNTI3Nzk1NDU0LC04MzgwMzM4OTAsLTE5MjI5
NjMxNzAsMTIzNzI5MjE4NSwxNzc2MDExMTAzLDgzMzE4MTg5Ny
wxODU2ODI4MjkxXX0=
-->