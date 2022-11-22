# Question 1

> Why do you see a difference in webpage fetch times with small and large router buffers?

|             | average | standard deviation |
|:-----------:| ------- | ------------------ |
| 20 packets  | 0.549   | 0.209              |
| 100 packets | 1.088   | 0.506              |

As we can find from the table above, the average fetch times for 20-packets router buffer is shorter than that of 100-packets router buffer. This is likely due to the size of buffer. Since the buffer can only detect a packet loss when the buffer is filled, and of course it takes more time for a larger size buffer to be filled. Also, less packets in the buffer means less waiting time.

# Question 2

> Bufferbloat can occur in other places such as your network interface card (NIC). Check the output of *ifconfig eth0* on your VirtualBox VM. What is the (maximum) transmit queue length on the network interface reported by ifconfig? For this queue size and a draining rate of 100 Mbps, what is the maximum time a packet might wait in the queue before it leaves the NIC?

The maximum transmit queue length on the network interface reported by ifconfig is 1000. Since MTU is 1500 byte, maximum waiting time is:

(1000 packets x 1500 bytes x 8 bits) / 100Mbps = 0.12s

# Question 3

> How does the RTT reported by ping vary with the queue size? Write a symbolic equation to describe the relation between the two (ignore computation overheads in ping that might affect the final result).

ffw

# Question 4

> Identify and describe two ways to mitigate the bufferbloat problem.

The first way is reducing the queue size, which means having a smaller size router buffer. The second way is .
