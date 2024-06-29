# 9th Session

- ## Debugging your network connection to another machine *[ There was some stuff before this section but I was late :D ]*
    - Check hardware connection
    - Ping from Machine A to Machine B
> `nmap -sP 192.168.1.0/24` to scan for ip addresses connected on your local network
    - `sudo tcpdump` to listen for all packets with `sudo tcpdump -w [filename.pcap]` to save the packets into a file that we can open with wireshark on our host machine if the remote machine does not have a gui to open `wireshark` [Each packet on wireshark shows how many layers is used and how many bytes it has]
> Some discussion on ports but nothing new in it
---
- ## Extras
    - Check the photo in the vault or the group for monitoring and debugging commands --> [Click here for the image](https://www.google.com/url?sa=i&url=https%3A%2F%2Fm.facebook.com%2FTecMint%2Fphotos%2Flinux-performance-monitoring-tools-httpswwwtecmintcomcommand-line-tools-to-monit%2F2260304577321323%2F&psig=AOvVaw2G1AWzdvblfUhyzxaUVWm5&ust=1719739579210000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCMDesKi_gIcDFQAAAAAdAAAAABAE)
---