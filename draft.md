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

## test_rwlock
Test read-write locks based on timing fairness.




## register_server | register_client | query_client
register_server is the registration center. The RPC server acts as a `register_client` to register the services it provides to the registration center. The RPC client acts as a `query_client` to query the registration center for information about the services it needs.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTI1MTE1MywxMDI3MDQ2MTE5LDI4NT
c4MDEwMSwyOTQ4NzczODAsNjExMDUyNTIzLC0yMTIxMDU5NjIz
LC0xNjQ2ODUwNDAsLTE1MDI3MTk3NTIsLTEzNDM1MDY1MTUsLT
IwODg3NDY2MTIsLTE1MDM0MTIwMjksLTgzNzY1MTc0NiwtNTI3
Nzk1NDU0LC04MzgwMzM4OTAsLTE5MjI5NjMxNzAsMTIzNzI5Mj
E4NSwxNzc2MDExMTAzLDgzMzE4MTg5NywxODU2ODI4MjkxXX0=

-->