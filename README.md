# Questions

## Question 1

> Why do you see a difference in webpage fetch times with small and large router buffers?

|             | average | standard deviation |
|:-----------:| ------- | ------------------ |
| 20 packets  | 0.585   | 0.202              |
| 100 packets | 1.180   | 0.647              |

As we can find from the table above, the average fetch times for 20-packets router buffer is shorter than that of 100-packets router buffer. This is likely due to the size of buffer. Due to the large size of buffer, it might continue to store as much as possible packets if the network continues to be busy, and thus packets in a larger buffer will have a longer waiting duration. 

Also, we know that in order to detecting the capacity of network, hosts will continuously increase the transmission rate until it finds a packet getting lost in the network. Larger buffer means the packets will not be immediately lost or rejected, they are stored in the buffer for later resending, and hosts will detect any problem later than using smaller buffer.  Thus, when the host find some lost of packets and begin to decrease its transmission rate, there are already lots of packets in the buffer and might cause the network unusable for a period of time.

## Question 2

> Bufferbloat can occur in other places such as your network interface card (NIC). Check the output of *ifconfig eth0* on your VirtualBox VM. What is the (maximum) transmit queue length on the network interface reported by ifconfig? For this queue size and a draining rate of 100 Mbps, what is the maximum time a packet might wait in the queue before it leaves the NIC?

The maximum transmit queue length on the network interface reported by ifconfig is 1000. Since MTU is 1500 byte, maximum waiting time is:

(1000 packets x 1500 bytes x 8 bits) / 100Mbps = 0.12s

## Question 3

> How does the RTT reported by ping vary with the queue size? Write a symbolic equation to describe the relation between the two (ignore computation overheads in ping that might affect the final result).

In this exercise we use ping process to find the RTT. Compared the graph of `rtt.png` for buffer size 20 and buffer size 100, we can see that as the buffer size increases, the RTT will also increase. Also, when using 100 buffer size, the ping times become more variable, this is likely due to the bufferbloat problem. When buffer occupancy is reduced, there is a rapid fall in RTT. However, it is still longer than 20 buffer size.

All in all, the relationship between RTT and queue size is linear.

## Question 4

> Identify and describe two ways to mitigate the bufferbloat problem.

The first way is reducing the queue size, which means having a smaller size router buffer. It is apparent that this can help to reduce the negative impact of bufferbloat. The second way is sending a message back to host when the packet is being resending by buffer. As mentioned before, larger buffer size will prevent the host getting prompt information and continuously sending too many packets. If a message is sending back to inform the host, it can reduce the transmission rate before the buffer gets overwhelmed. Obviously it might increase the overload of network but it can mitigate the bufferbloat problem to some extent.
