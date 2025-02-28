[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Caroline Smith
### Student Id: 21072056
### Email: casmithaa@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

I selected the Phoronix Test Suite tool. For CPU benchmarking, I have chosen to use the Himeno test. This is because unlike other tests (e.g. build-linux-kernel),
 the Himeno test can be run in a reasonable amount of time by each VM (given the four-hour AWS academy server limit). I also chose Himeno because it benchmarks multi-threaded processing. The value of the Himeno benchmark corresponds to how many MFLOPS (million floating point operations per second) it takes the CPU/CPUs to perform a linear solving problem;
 the Phoronix Himeno test returns the average MFLOPS over three different runs.

 For memory performance, I selected the RAMSpeed SMP test (pts/ramspeed). This benchmarking test tests the bandwidth of both cache and memory subsystems through both reading and writing operations. This test measures memory operations in speeds of decimal megabytes per second.
 In Phoronix, you have the option of testing different _types_ of operations:

    Memory Test Configuration
        1: Copy
        2: Scale
        3: Add
        4: Triad
        5: Average
        6: Test All Options

 As well as integer, floating-point or both operations:

        1: Integer
        2: Floating Point
        3: Test All Options


Due to the limited processing power of the VMs, I tested the Copy and Add operations with both Integer and Floating-Point values. This allowed for testing of both read and write capabilities. The final number which I have put in the table below represents the average of the four values (Add-Integer, Add-FP, Copy-Integer, and Copy-FP); each test-datatype value
 is itself an average of three trials.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance / MFLOPS | Memory performance / dec. megabytes per second |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |   3106.6    | 10519.7  |
    | `t2.medium`  |  3069.3    | 19882.9  |
    | `c5d.large` |   2772.5    |  13892.6   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3560  | 0.342  |
    | `m5.large` - `m5.large`   | 4950  | 0.170  |
    | `c5n.large` - `c5n.large` | 4960  | 0.148  |
    | `t3.medium` - `c5n.large` | 2240  | 0.701  |
    | `m5.large` - `c5n.large`  | 4960  | 0.154  |
    | `m5.large` - `t3.medium`  | 2600  | 0.640  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 3270  | 60.588  |
    | N. Virginia - N. Virginia | 4960  | 0.148  |
    | Oregon - Oregon           | 4950  | 0.138  |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
