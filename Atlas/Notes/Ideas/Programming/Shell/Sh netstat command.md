- It used for examining network connections on your computer.
- It acts like a network traffic inspector, giving you insights into how your device is communicating with other devices or servers over the internet.
### What can do
- **Show Active Connections:** Netstat's primary function is to display a list of active network connections, including:

	- Local and remote IP addresses and ports involved in the connection.
	- Protocol being used (TCP, UDP, etc.).
	- Connection state (listening, established, closing, etc.).

- **Identify Listening Ports:** It can reveal which programs on your computer are actively listening for incoming connections on specific ports. This helps you understand what programs are potentially communicating externally.

- **Monitor Network Activity:** By running Netstat periodically, you can monitor changes in network connections and identify suspicious activity.

- **Gather Network Statistics:** Netstat can also provide general network statistics like the total number of packets sent and received.
### Flags
- `-a`: Show all connections, including listening and non-listening sockets.
- `-t`: Show TCP connections only.
- `-u`: Show UDP connections only.
- `-l`: Show listening sockets only.
- `-p`: Show the process ID (PID) of the program using the connection.
- `-n`: Show process names in numerical form (often used with `-p`).
- `-i`: Display a short list in a format for all network interfaces ^0d9c81

### Output 
The output of Netstat can vary depending on your operating system, but it typically includes columns with information like:

- **Proto:** The protocol used (TCP, UDP).
- **Recv-Q:** The number of bytes in the receive queue.
- **Send-Q:** The number of bytes in the send queue.
- **Local Address:** The IP address and port of your computer.
- **Foreign Address:** The IP address and port of the remote computer.
- **State:** The state of the connection (LISTEN, ESTABLISHED, etc.).

By using the appropriate flags and interpreting the output, Netstat becomes a valuable tool for network troubleshooting, security analysis, and general network monitoring.