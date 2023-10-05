#  mapreduce

## preprocess
Generate random initial input files $\text{input.txt}$ .

##   mapreduce

###  `split_init_input`
Preprocessing before calculation: divide $\text{input.txt}$ into $m$ (number of map nodes) sub-files $\text{input0.txt},\cdots,\text{input(m-1).txt}$ .

### `master_node_task`
The master node creates threads that execute map tasks and reduce tasks, and checks whether their respective outputs are complete. If the output of a task is incomplete, the master node restarts the corresponding task.


## cmp_serial_method

Record the time taken by the ordinary linear scan method.

## check_result
Verify the correctness of mapreduce calculation results.


# RPC

## test_serialization_deserialization
Verify correctness of serialization and deserialization of nested and custom types.

## server & client
The server provides RPC services, and the client requests the corresponding RPC services.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTQyNzM3NzMsMjk0ODc3MzgwLDYxMT
A1MjUyMywtMjEyMTA1OTYyMywtMTY0Njg1MDQwLC0xNTAyNzE5
NzUyLC0xMzQzNTA2NTE1LC0yMDg4NzQ2NjEyLC0xNTAzNDEyMD
I5LC04Mzc2NTE3NDYsLTUyNzc5NTQ1NCwtODM4MDMzODkwLC0x
OTIyOTYzMTcwLDEyMzcyOTIxODUsMTc3NjAxMTEwMyw4MzMxOD
E4OTcsMTg1NjgyODI5MV19
-->