# Distributed Merge Sorting System

## System Structure
* Master only conducts operation of slaves. All meaningful sorting processes occur in each slave.
* Slaves can directly exchange data with each other without master once bootstrap is complete.
* Detailed information at [Implementation Details](impl.md).


## Procedure 
1. Run master with slave informations.

2. Run slaves with master information. Slaves automatically establish connection to master.

3. Master command slaves sampling.

4. Slaves sample data accordingly and reply with mean.
> Slaves process data locally, and then reply with mean. Sample data could not be sent through gRPC as HTTP/2 do not handle large data transfer gracefully on which protocol buffer is based.

5. Master labels each slave with estimated value range order and broadcast complete slave informations(Addresses and labels).

6. Slaves start merge sort locally.

7. After local sort, slaves partition data and send to corresponding slaves if required. Slaves notifie master when all partitions are complete.

8. Master permits slaves to proceed to final merge process.

9. Slaves merge local and received data and then report resulting files. Slave program finishes.

10. Master outputs collected report. Master program finishes.



