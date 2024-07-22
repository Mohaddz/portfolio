---
title: "Dynamic vs Normal Round Robin Scheduling Comparison"
date: 2022-11-15T10:00:00+03:00
draft: false
toc: true
images:
  - "https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/DRRpost.png"
tags:
  - Operating Systems
  - Java
  - Scheduling Algorithms
  - Round Robin
  - Dynamic Round Robin
  - CPU Scheduling
---
<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/DRRpost.png" width=3000 height=500>

<br>

[Github Repo](https://github.com/Mohaddz/Dynamic-Round-Robin)
<img style="float: left;margin-right: 20px;" src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/github-mark-white.svg" width="30" height="30"/> 

## 1. Introduction

CPU scheduling is a crucial aspect of operating systems, allowing efficient utilization of CPU and I/O resources. This project implements and compares two variations of the Round Robin (RR) algorithm: Normal Round Robin and Dynamic Round Robin. The Round Robin algorithm is designed for time-sharing systems, allowing processes to use the CPU for a fixed time quantum before switching to the next process.

### 1.1 Understanding CPU Scheduling

Before diving into the specifics of Round Robin algorithms, it's essential to understand what CPU scheduling is:

CPU scheduling is the process by which the operating system decides which process or thread should run on the CPU at any given time. The main goals of CPU scheduling are to:
1. Maximize CPU utilization
2. Ensure fair allocation of CPU time among processes
3. Minimize response time for interactive users
4. Maximize throughput (number of processes completed per unit time)

Different scheduling algorithms aim to achieve these goals in various ways, each with its own strengths and trade-offs.

### 1.2 Dynamic Round Robin vs Normal Round Robin

Both Dynamic and Normal Round Robin are variants of the basic Round Robin algorithm, which allocates a fixed time slice (quantum) to each process in a circular order. However, they differ in how they determine and use this time quantum:

1. **Normal Round Robin (NRR)**:
   - Uses a fixed time quantum for all processes
   - Simple to implement and understand
   - Can lead to longer waiting times for processes with varying CPU burst times

2. **Dynamic Round Robin (DRR)**:
   - Adjusts the time quantum based on the current mix of processes in the ready queue
   - Typically calculates the quantum as the average burst time of processes in the ready queue
   - More adaptive to varying process requirements
   - Generally results in better overall system performance, especially with a mix of short and long processes

Key Differences:
- *Quantum Calculation*: NRR uses a predetermined fixed quantum, while DRR calculates it dynamically.
- *Adaptability*: DRR adapts to the current workload, whereas NRR maintains the same quantum regardless of process characteristics.
- *Performance*: DRR often shows improved average waiting time and turnaround time compared to NRR, especially in heterogeneous workloads.

This project aims to implement and compare these two approaches, demonstrating the potential benefits of a more adaptive scheduling algorithm in modern computing environments.


## 2. Project Structure

The project consists of four main classes:

1. **DRR (Main class)**: Handles the main program flow, input reading, and scheduling simulation.
2. **Process2**: Represents a process with its attributes and scheduling methods.
3. **Config**: Manages the system configuration (memory, devices).
4. **Comp**: A comparator class for priority queue sorting.

### 2.1 DRR (Main Class)

- Reads input from a file
- Allows user to choose between Dynamic and Normal Round Robin
- Manages queues: SubmitQ, ReadyQ, HoldQ1p (priority queue), HoldQ2
- Executes the chosen scheduling algorithm
- Displays the results in a table format

### 2.2 Process2 Class

- Represents individual processes
- Contains attributes like arrival time, job number, memory units, devices, burst time, and priority
- Implements methods for moving processes between queues and executing Round Robin algorithms

### 2.3 Config Class

- Manages system resources (memory and devices)
- Tracks available and used resources

### 2.4 Comp Class

- Implements a comparator for sorting processes in the priority queue based on memory requirements

## 3. Implementation Highlights

### Dynamic Round Robin

```java
public void RoundRobin(Queue<Process2> ReadyQ, PriorityQueue<Process2> HoldQ1p, Queue<Process2> HoldQ2,
        ArrayList<Config> PC, int quantum, StringBuffer str) {
    quantum = getTotalBurstTime() / ReadyQ.size();
    // ... (rest of the method)
}
```

### Normal Round Robin

```java
public void RoundRobinNormal(Queue<Process2> ReadyQ, PriorityQueue<Process2> HoldQ1p, Queue<Process2> HoldQ2,
        ArrayList<Config> PC, int quantum, StringBuffer str) {
    quantum = 10;
    // ... (rest of the method)
}
```

## 4. Sample Input
Raw.txt
```
C 9 M=45 S=12
A 10 J=1 M=5 S=4 R=8 P=1
A 13 J=2 M=49 S=2 R=13 P=2
A 15 J=3 M=13 S=5 R=5 P=1
A 19 J=4 M=6 S=1 R=7 P=2
A 21 J=5 M=1 S=3 R=4 P=2
A 28 J=6 M=3 S=4 R=8 P=1
A 34 J=7 M=41 S=5 R=12 P=2
A 35 J=8 M=27 S=3 R=8 P=1
D 36
```
| Time | Type | Job | Memory | Devices | Burst Time | Priority |
|------|:----:|-----|--------|---------|------------|----------|
| 9    |  C   | -   | 45     | 12      | -          | -        |
| 10   |  A   | 1   | 5      | 4       | 8          | 1        |
| 13   |  A   | 2   | 49     | 2       | 13         | 2        |
| 15   |  A   | 3   | 13     | 5       | 5          | 1        |
| 19   |  A   | 4   | 6      | 1       | 7          | 2        |
| 21   |  A   | 5   | 1      | 3       | 4          | 2        |
| 28   |  A   | 6   | 3      | 4       | 8          | 1        |
| 34   |  A   | 7   | 41     | 5       | 12         | 2        |
| 35   |  A   | 8   | 27     | 3       | 8          | 1        |
| 36   |  D   | -   | -      | -       | -          | -        |




This input file defines the system configuration and processes to be scheduled.

## 5. Results and Comparison

### Performance Metrics

#### Average Waiting Time Comparison
<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/DRR11.jpg" width=700 height=300>

#### Average Turnaround Time Comparison
<img src="https://raw.githubusercontent.com/Mohaddz/portfolio/master/static/images/DRR22.jpg" width=700 height=300>

### Output

#### Dynamic Round Robin
| Process | Burst Time | Arrival Time | Completion Time | Turnaround Time | Waiting Time |
|---------|------------|--------------|-----------------|-----------------|--------------|
| 1       | 8          | 10           | 18              | 8               | 0            |
| 3       | 5          | 15           | 23              | 8               | 3            |
| 5       | 4          | 21           | 32              | 11              | 7            |
| 4       | 7          | 19           | 34              | 15              | 8            |
| 6       | 8          | 28           | 42              | 14              | 6            |
| 7       | 12         | 34           | 54              | 20              | 8            |
| 8       | 8          | 35           | 62              | 27              | 19           |

#### Normal Round Robin
| Process | Burst Time | Arrival Time | Completion Time | Turnaround Time | Waiting Time |
|---------|------------|--------------|-----------------|-----------------|--------------|
| 1       | 8          | 10           | 18              | 8               | 0            |
| 3       | 5          | 15           | 33              | 18              | 13           |
| 4       | 7          | 19           | 40              | 21              | 14           |
| 5       | 4          | 21           | 44              | 23              | 19           |
| 6       | 8          | 28           | 52              | 24              | 16           |
| 8       | 8          | 35           | 70              | 35              | 27           |
| 2       | 13         | 13           | 73              | 60              | 47           |
| 7       | 12         | 34           | 75              | 41              | 29           |

Key findings:
- Dynamic Round Robin showed better average Waiting Time and Turnaround Time compared to Normal Round Robin.
- Normal Round Robin's fixed quantum led to longer waiting times for processes.
- Dynamic Round Robin's flexible quantum, based on the average of jobs in the ready queue, resulted in more efficient processing.

## 6. Challenges and Solutions

1. **Challenge**: Implementing priority-based queuing for processes.

   **Solution**: Used a PriorityQueue with a custom Comparator to sort processes based on memory requirements.

2. **Challenge**: Managing system resources efficiently.

   **Solution**: Implemented the Config class to keep track of available and used resources.

3. **Challenge**: Calculating dynamic quantum for the Dynamic Round Robin.

   **Solution**: Used the average burst time of processes in the ready queue to determine the quantum.

## 7. Enhancement Suggestions

To optimize Normal Round Robin:
- Select an appropriate time quantum in relation to the process's burst time in the ready queue.
- Balance between short and long time quantums to avoid excessive context switching or process starvation.

## 8. Conclusion

While Normal Round Robin didn't outperform Dynamic Round Robin, it remains well-suited for timesharing systems. The Dynamic Round Robin algorithm demonstrated superior performance in terms of average Waiting Time and Turnaround Time. This project showcases the importance of adaptive scheduling techniques in optimizing CPU utilization and process management.

## 9. Future Work

- Implement more scheduling algorithms for comparison (e.g., Shortest Job First, Priority Scheduling)
- Add GUI for real-time visualization of the scheduling process
- Incorporate more complex process behaviors (I/O bursts, priority changes)
- Explore further optimizations for the Normal Round Robin algorithm