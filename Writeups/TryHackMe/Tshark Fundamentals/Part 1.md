# TShark Fundamentals - Part I

TShark is a network protocol analyzer that allows users to capture and interactively browse the contents of network traffic. It is the command-line version of Wireshark, providing similar functionality without the graphical interface. TShark is useful for capturing data packets in real-time and analyzing them for troubleshooting, network analysis, and educational purposes.

### Hints for Command-Line Packet analysis
Since this tool is CLI-based, it is suitable for data carving, in-depth packet analysis and automation with scripts. Here is a list of the most common tools used in packet analysis.

| Tool    | Purpose                                                                 |
|---------|-------------------------------------------------------------------------|
| capinfos| Provides information about capture files                                |
| grep    | Searches for specific patterns within packet data                       |
| cut     | Removes sections from each line of packets                              |
| uniq    | Filters out repeated lines in packet data                               |
| nl      | Numbers lines in packet data                                            |
| sed     | Edits packet data based on a script                                     |
| awk     | Processes and analyzes packet data                                      |

### Command-Line Interface and Parametres
We must have in consideration that since TShark is text-based, obtaining the results is easy. It is paramount to learn the essentials. The most common parameres are explained in the following table:

| Parameter | Purpose                                                                 |
|-----------|-------------------------------------------------------------------------|
| -h        | Displays help information and exits                                     |
| -v        | Displays the version information and exits                              |
| -D        | Lists all available network interfaces                                  |
| -i        | Specifies the network interface to use for capturing packets            |
| (none)    | Runs TShark with default settings, capturing packets on the first available interface |

Now let's show other parameters to have in consideration:

| Parameter | Purpose                                                                 |
|-----------|-------------------------------------------------------------------------|
| -r        | Reads packets from a specified capture file instead of capturing live data |
| -c        | Specifies the number of packets to capture                              |
| -w        | Writes the captured packets to a specified file                         |
| -V        | Displays detailed information about each packet                         |
| -q        | Runs TShark in "quiet" mode, minimizing output                          |
| -x        | Displays each packet in a hex and ASCII format                          |

Now practicing a little bit here are the results:

Checking out the version of the tool.

![Figure 1 - TShark Version](/Writeups/TryHackMe/Tshark%20Fundamentals/Pictures/Tshark1-version.png)

#### **Sniffing** 
Be aware that a computer can have multiple network interfaces allowing the host to communicate and sniff the traffic throughout the network. Therefore, it is importante to specify interfaces with particular jobs. Viewing the available interfaces in this VM.

![Figure 2 - TShark Available Interfaces](/Writeups/TryHackMe/Tshark%20Fundamentals/Pictures/Tshark2-interfaces.png)

Sniffing can be done without selecting an interfaces. No interfaces means an anlias for `-i 1`. Setting a different sniffing interface is done using the `-i` parametres. TShark always echoes the used interface name at the beginning of the sniffing.

![Figure 3 - TShark Sniffing](/Writeups/TryHackMe/Tshark%20Fundamentals/Pictures/Tshark3-sniffing.png)
