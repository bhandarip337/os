<div align="center">

[**_``Go Back``_**](../README.md)

# Deadlock

</div>

## Introduction
A process in operating system uses resources in the following way. 

- Requests a resource 
- Use the resource 
- Releases the resource 

``Deadlock`` is a situation where a set of processes are blocked because each process is holding a resource and waiting for another resource acquired by some other process.

Consider an example when two trains are coming toward each other on the same track and there is only one track, none of the trains can move once they are in front of each other. A similar situation occurs in operating systems when there are two or more processes that hold some resources and wait for resources held by other(s). For example, in the below diagram, ``Process 1`` is holding ``Resource 1`` and waiting for ``Resource 2`` which is acquired by ``Process 2``, and ``Process 2`` is waiting for ``Resource 1``

<div align="center">

!["Deadlock"](pic/deadlock.png)

</div>

``Deadlock`` can arise if the following four conditions hold simultaneously (Necessary Conditions) 

- ``Mutual Exclusion:`` Two or more resources are non-shareable (Only one process can use at a time) 
- ``Hold and Wait:`` A process is holding at least one resource and waiting for resources. 
- ``No Preemption:`` A resource cannot be taken from a process unless the process releases the resource. 
- ``Circular Wait:`` A set of processes are waiting for each other in circular form. 

## System Model

- For the purposes of deadlock discussion, a system can be modeled as a collection of limited resources that can be divided into different categories and allocated to a variety of processes, each with different requirements.
- Memory, printers, CPUs, open files, tape drives, CD-ROMs, and other resources are examples of resource categories.e
- By definition, all resources within a category are equivalent, and any of the resources within that category can equally satisfy a request from that category. If this is not the case (i.e. if there is some difference between the resources within a category), then that category must be subdivided further. For example, the term “printers” may need to be subdivided into “laser printers” and “color inkjet printers.”
- Some categories may only have one resource.
- The kernel keeps track of which resources are free and which are allocated, to which process they are allocated, and a queue of processes waiting for this resource to become available for all kernel-managed resources. Mutexes or ``wait()`` and ``signal()`` calls can be used to control application-managed resources (i.e. binary or counting semaphores. )
- When every process in a set is waiting for a resource that is currently assigned to another process in the set, the set is said to be deadlocked.
>todo

## System Resources : Preemptable and Non-Preemptable

Deadlocks can occur when processes have been granted exclusive access to devices, files and so forth. To make the discussion of deadlocks as general as possible, we will refer to the objects granted as resources. 

>The resource is the object granted to a process.

Resources come in two types: 

- ``Preemptable:`` A preemptable resource is one that can be taken away from the process owning it with no ill effects. Memory is an example of a preemptable resource. 

- ``Non-Preemptable:``A non-preemptable resource is one that cannot be taken away. An example is a printer.

## Condition for Resource Deadlock 

The condition for resource deadlock are:

- ``Mutual Exclusion``
- ``Hold and Wait``
- ``No preemption``
- ``Circular Wait`` 


### ``Mutual Exclusion:`` 
A resource can be held by only one process at a time. In other words, if a process ``P1`` is using some resource ``R`` at a particular instant of time, then some other process ``P2`` can't hold or use the same resource ``R`` at that particular instant of time. The process ``P2`` can make a request for that resource ``R`` but it can't use that resource simultaneously with process ``P1``.

### ``Hold and Wait:`` 
A process can hold a number of resources at a time and at the same time, it can request for other resources that are being held by some other process. For example, a process ``P1`` can hold two resources ``R1`` and ``R2`` and at the same time, it can request some resource ``R3`` that is currently held by process ``P2``.

### ``No preemption:`` 
A resource can't be preempted from the process by another process, forcefully. For example, if a process ``P1`` is using some resource ``R``, then some other process ``P2`` can't forcefully take that resource. If it is so, then what's the need for various scheduling algorithm. The process ``P2`` can request for the resource ``R`` and can wait for that resource to be freed by the process ``P1``.

### ``Circular Wait:`` 
Circular wait is a condition when the first process is waiting for the resource held by the second process, the second process is waiting for the resource held by the third process, and so on. At last, the last process is waiting for the resource held by the first process. So, every process is waiting for each other to release the resource and no one is releasing their own resource. Everyone is waiting here for getting the resource. This is called a circular wait.

## Deadlock Modeling

>todo

## The OSTRICH Algorithm

There is a very interesting algorithm in Computer Science named as ``Ostrich Algorithm`` in which all of us should be an expert.

Before reading further about this algorithm, first let me tell you about a common (but false) legend about Ostriches that when a danger comes ostriches bury their heads in the sand and pretend there is no danger at all.

Now, I assume you would have understood whats this ``Ostrich Algorithm``.

In Computer Science, the strategy of ignoring potential problems on the basis that they will occur very rarely, is called as ``Ostrich Algorithm``. Many times, to trade-off between high priority tasks and very rarely occurring known errors, we as developers take this strategy. 

Though this ``Ostrich Algorithm`` sounds funny, this is one of the popular solutions to handle deadlocks in many popular operating systems. Checking for and avoiding deadlock is too expensive. Given that they happen very rarely, the engineers decided to choose Reboot if there is a deadlock.

## Method of Handeling Deadlock

There are three approaches to deal with deadlocks.

- ``Deadlock Prevention``
- ``Deadlock avoidance``
- ``Deadlock detection and Recovery``

### ``Deadlock Prevention``
This is done by restraining the ways a request can be made. Since deadlock occurs when all the above four conditions are met, we try to prevent any one of them, thus preventing a deadlock.

### ``Deadlock avoidance``
This approach allows the three necessary conditions of deadlock but makes judicious choices to assure that deadlock point is never reached. It allows more concurrency than avoidance detection A decision is made dynamically whether the current resource allocation request will, if granted, potentially lead to deadlock. It requires the knowledge of future process requests. Two techniques to avoid deadlock :

- Process initiation denial
- Resource allocation denial

Advantages of deadlock avoidance techniques :

- Not necessary to pre-empt and rollback processes
- Less restrictive than deadlock prevention

Disadvantages :

- Future resource requirements must be known in advance
- Processes can be blocked for long periods
- Exists fixed number of resources for allocation

### ``Deadlock detection and Recovery``

We let the system fall into a deadlock and if it happens, we detect it using a detection algorithm and try to recover.

Some ways of recovery are as follows.

- Aborting all the deadlocked processes.
- Abort one process at a time until the system recovers from the deadlock.
- ``Resource Preemption:`` Resources are taken one by one from a process and assigned to higher priority processes until the deadlock is resolved.

## Deadlock Prevention

>todo

## Deadlock Avoidance:  Bankers Algorithm

>todo

## Deadlock Detection: Resource Allocation Graph

>todo

## Recovery from Deadlock

When a Deadlock Detection Algorithm determines that a deadlock has occurred in the system, the system must recover from that deadlock. There are two approaches of breaking a Deadlock: 

- ``Process Termination``
- ``Resource Preemption``

### ``Process Termination`` 
To eliminate the deadlock, we can simply kill one or more processes. For this, we use two methods: 

#### **Abort all the Deadlocked Processes** 
Aborting all the processes will certainly break the deadlock, but with a great expense. The deadlocked processes may have computed for a long time and the result of those partial computations must be discarded and there is a probability to recalculate them later. 
 
#### **Abort one process at a time until deadlock is eliminated** 
Abort one deadlocked process at a time, until deadlock cycle is eliminated from the system. Due to this method, there may be considerable overhead, because after aborting each process, we have to run deadlock detection algorithm to check whether any processes are still deadlocked. 
 
### ``Resource Preemption`` 
To eliminate deadlocks using resource preemption, we preempt some resources from processes and give those resources to other processes. This method will raise three issues – 

#### **Selecting a victim** 
We must determine which resources and which processes are to be preempted and also the order to minimize the cost. 
 
#### **Rollback** 
We must determine what should be done with the process from which resources are preempted. One simple idea is total rollback. That means abort the process and restart it. 
 
#### **Starvation** 
In a system, it may happen that same process is always picked as a victim. As a result, that process will never complete its designated task. This situation is called Starvation and must be avoided. One solution is that a process must be picked as a victim only a finite number of times. 



