# Distributed Merge Sorting System

## System Structure
* Master only conducts operation of slaves. All meaningful sorting processes occur in each slave.
* Slaves can directly exchange data with each other without master once bootstrap is complete.
* Detailed information at [Implementation Details](impl.md).


## Procedure 

|Master                     |                      Slave   |
|---------------------------|------------------------------|
|Run with number of slaves  |                              |
|                           |Run with master information   |
|                           |Connect to master             |
|                           |Sample data and send to master|
|                           |Keep requesting complete slave informations to master |
|Collect sampled data and slave informations |    |
|Label each slave with estimated value range order |   |
|Reply with complet slave informations (`Address`, `label`) | |
|                           |Save neighbor informations |
|                           |Sort local data |
|                           |Partition data and send to corresponding slaves |
|                           |Notify master once data transfer is completed |
|                           |Keep requesting permit to proceed toward final merge |
|Reply with permit once all slave notified data transfer completion| |
|                           |Merge final partitions|
|                           |Report resulting filenames|
|Collect filenames          |  |    
|Report sorting result      |   |


