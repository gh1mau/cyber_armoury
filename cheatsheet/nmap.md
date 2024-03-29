## NMAP Cheatsheet

**Scanning Type**

| Scanning Type                       | Command                                      | Description                                            |
| ----------------------------------- | -------------------------------------------- | ------------------------------------------------------ |
| TCP SYN port scan (default)         | `nmap -sS <target>`                          | Scans for open ports using TCP SYN packets             |
| TCP connected port scan             | `nmap -sT <target>`                          | Scans for open ports using full TCP connections        |
| UDP port scan                       | `nmap -sU <target>`                          | Scans for open ports using UDP packets                 |
| Ping scan                           | `nmap -sP <target>`                          | Scans for hosts that respond to ping requests          |

<br>

**Version Detection**

| Option        | Command                                        | Description                                                                                                                                                                       |
| ------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-sV`         | `nmap -sV <target>`                            | Basic command for finding the version of the service                                                                                                                              |
| `--version-intensity 6` | `nmap -sV --version-intensity 6 <target>` | Set the intensity level (0-9) for version detection                                                                                                                         |
| `-A`          | `nmap -A <target>`                             | Aggressive scan option that includes OS detection, version detection, script scanning, and traceroute. Can create noise. Requests may be caught by the firewall if they have one. |
| `-O`          | `nmap -O <target>`                             | Remote OS detection option                                                                                                                                                       |

<br>

**Ports Specific**

| Option        | Command                                            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------- | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-p <port>`   | `nmap -p 23 <target>`                              | Scan for a specific port                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `-p <range>`  | `nmap -p 23-100 <target>`                          | Scan for a range of ports                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `-pU:110,T:23-25` | `nmap -pU:110,T:23-25 <target>`                  | Scan for different types of ports (UDP and TCP)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `-p-`         | `nmap -p- <target>`                                | Scan all ports (65535 ports by default, but may take longer and create more noise). However, sometimes clever administrators may hide important information on less common ports.                                                                                                                                                                                                                                                                                                                                                                                                |
| `-smtp,https` | `nmap -smtp,https <target>`                        | Scan for specific protocols. In this example, the command would scan for SMTP and HTTPS services.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

<br>

**Time Options**

| Option       | Command                                           | Description                                                                                                                                                                    |
| ------------ | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-T0`        | `nmap -T0 <target>`                              | Slow scan option that sends packets less frequently than the default. Useful for scanning networks where a lot of traffic is already present.                                        |
| `-T1`        | `nmap -T1 <target>`                              | Faster scan option than the default. Sends packets more frequently than the slow scan option, but still designed to be stealthy.                                             |
| `-T2`        | `nmap -T2 <target>`                              | Timely scan option that balances speed and stealth. Sends packets more frequently than the default, but still designed to be stealthy.                                           |
| `-T3`        | `nmap -T3 <target>`                              | Aggressive scan option that sends packets even more frequently than the timely scan option. May create more noise and be detected by firewalls or intrusion detection systems. |
| `-T4`        | `nmap -T4 <target>`                              | Very aggressive scan option that sends packets extremely frequently. May create a lot of noise and may be detected by firewalls or intrusion detection systems.             |


<br>

**Scripts**

| Option                                  | Command                                             | Description                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--scripts vulners`                     | `nmap --scripts vulners <target>`                  | Executes the `vulners` script, which checks for known vulnerabilities on the target host. The script can be found on GitHub at https://github.com/vulnersCom/nmap-vulners.                                                                                                                                                                                                                                   |
| `--script vulners,ftp-anon`             | `nmap --script vulners,ftp-anon <target>`          | Executes multiple scripts (in this case, the `vulners` and `ftp-anon` scripts) on the target host. Multiple scripts can be specified by separating them with a comma.                                                                                                                                                                       |
| `-p 21 --script "ftp-*"`                | `nmap -p 21 --script "ftp-*" <target>`             | Executes all scripts that match the pattern `ftp-*` for the FTP service running on port 21. This allows for comprehensive scanning of the FTP service, and can be adapted for other services by changing the pattern. Additional scripts can be specified by separating them with a comma.                                              |
| `-sV -sC`                               | `nmap -sV -sC <target>`                           | Executes the default scripts for version detection and basic script scanning on the target host. The `-sV` option enables version detection, while `-sC` runs the default set of scripts.                                                                                                                                              |
| `--script-help http-waf-detect.nse`     | `nmap --script-help http-waf-detect.nse`          | Displays help information for the `http-waf-detect.nse` script. This option can be used to obtain documentation on any script included with Nmap.                                                                                                                                                                                           |
| `nmap --script-updatedb`                | `nmap --script-updatedb`                           | Updates the Nmap script database to include the latest scripts from the Nmap community. This can improve scanning performance and accuracy, as well as ensure that the latest security vulnerabilities are being scanned for. Note that this command may require root privileges. |
| `ls -al /usr/share/nmap/scripts/` (CLI) | `ls -al /usr/share/nmap/scripts/`                  | Lists all the default scripts included with Nmap. This command can be executed in a terminal to view the available scripts, and can be used as a reference when specifying scripts to run during scanning.                                                                                                                              |

<br>

**Miscellaneous**

| Option                            | Command                                           | Description                                                                                                                                                                                                                                                                   |
| --------------------------------- | ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-A -T4`                          | `nmap -A -T4 <target>`                            | Executes an aggressive scan with a timing template of T4, which increases the speed of the scan at the cost of accuracy. The `-A` option enables OS detection, version detection, script scanning, and traceroute.                                                                   |
| `-sV -sS -vv`                     | `nmap -sV -sS -vv <target>`                       | Executes a scan with the default scripts for version detection and a TCP SYN scan for port scanning. The `-vv` option enables verbose output for more detailed scan results.                                                                                                     |
| `-A -F`                           | `nmap -A -F <target>`                             | Executes an aggressive scan with fast scan options enabled. The `-F` option enables a scan of only the most common 100 ports, while the `-A` option enables OS detection, version detection, script scanning, and traceroute.                                                        |




