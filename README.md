# MAC Address Spoofer

This is my first ever project. It’s a Python 3 script that temporarily changes (spoofs) the MAC address of a Linux network interface. 

Instead of just running a working tool, I took an older, broken script and forced myself to debug it so I could actually understand how Python interacts with the Linux operating system.

### Stuff I figured out while building this:
* **Python 3 is picky:** The original code crashed because Python 3 handles terminal output (`subprocess`) as raw bytes, not strings. I had to learn how to `.decode("utf-8")` the output so my Regex search wouldn't panic.
* **Kali fights back:** At first, the script "worked" but the MAC address didn't actually change. I figured out that Kali's `NetworkManager` was instantly stepping in and resetting my interface back to its real VirtualBox MAC. I had to learn how to pause system services to make the spoof stick.
* **Never blindly trust code:** The original script I learned from had backward `if/else` logic that said the hack failed even when it worked. I rewrote the logic flow and fixed the broken syntax.

### How to use it
You need Linux and Python 3. (Tested on Kali Linux).

```bash
# 1. Stop NetworkManager so it doesn't instantly reset your MAC
sudo systemctl stop NetworkManager

# 2. Run the script (change eth0 to your interface and pick a fake MAC)
sudo python3 mac_changer.py -i eth0 -m 00:11:22:33:44:55

# 3. Check if it worked
ip a

# 4. Turn your internet back on when you're done playing
sudo systemctl start NetworkManager
```
### (Note: Built strictly for educational purposes and testing in my local VM lab)
