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

## server | client
The server provides RPC services, and the client requests the corresponding RPC services.

## register_server | register_client

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjg1NzgwMTAxLDI5NDg3NzM4MCw2MTEwNT
I1MjMsLTIxMjEwNTk2MjMsLTE2NDY4NTA0MCwtMTUwMjcxOTc1
MiwtMTM0MzUwNjUxNSwtMjA4ODc0NjYxMiwtMTUwMzQxMjAyOS
wtODM3NjUxNzQ2LC01Mjc3OTU0NTQsLTgzODAzMzg5MCwtMTky
Mjk2MzE3MCwxMjM3MjkyMTg1LDE3NzYwMTExMDMsODMzMTgxOD
k3LDE4NTY4MjgyOTFdfQ==
-->