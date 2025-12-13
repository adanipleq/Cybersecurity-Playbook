| #  | Question / Issue                                    | Key Answer                                                                                   |
| -- | --------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 1  | Switch forwarding frames but router sees no traffic | **OSI Layer 2 – Data Link;** forwards frames using MAC addresses                             |
| 2  | Subnet 192.168.50.0/26                              | First usable: **192.168.50.1**; Last usable: **192.168.50.62**; Broadcast: **192.168.50.63** |
| 3  | PCs in VLAN 20 can’t talk                           | Commands: **show vlan brief**, **show interfaces trunk**                                     |
| 4  | Static route for 172.16.0.0/24                      | `ip route 172.16.0.0 255.255.255.0 <next-hop>`                                               |
| 5  | Block external ICMP echos                           | `access-list 100 deny icmp any any echo`                                                     |
| 6  | Wi-Fi drops randomly                                | Causes: **RF interference**, **physical obstructions**                                       |
| 7  | Correct T568B order                                 | White/Orange, Orange, White/Green, Blue, White/Blue, Green, White/Brown, Brown               |
| 8  | Can ping gateway but not 8.8.8.8                    | Test **Layer 3** next → routing beyond gateway                                               |
| 9  | Measure bandwidth & performance                     | Protocol: **TCP/UDP**; Tool: **iPerf**                                                       |
| 10 | Final verification                                  | Working **ping test** shown below                                                            |
<img width="706" height="674" alt="image" src="https://github.com/user-attachments/assets/7cd94314-dc11-4ea8-9a1a-ed417a99f665" />
