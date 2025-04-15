---
title: Injection
date: 2025-04-12
categories: [dockerlabs, pentesting]
tags: [kali-linux, very-easy]
---
The first machine we're going to solve is called **Injection**, and it's categorized as **very easy**. 
## Initial Setup of the Target Machine
We need to download the machine through the DockerLabs website, which will led us to a Mega download page.

This step applies to all machines.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411171104.png)

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411171231.png)

Once we have the archive downloaded, we need to unzip it. This will result in two files: **auto_deploy.sh** and **injection.tar**.

To initialize the machine, we must use the following command in the terminal, in the same directory where we unzipped the archive:

```bash
sudo bash auto_deploy.sh injection.tar
```

Since it's the first time, Docker will be installed automatically; we just need to wait.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411171449.png)
## Scanning and Enumeration

Once the installation is finished, it will show us the **IP address** of the machine. In this case, it's **172.17.0.2**. 

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411171610.png)

The first thing we should do, is scan the IP address of the machine. We're looking for **open ports**.

We will use the following command:

```bash
 nmap -p- --open -sT --min-rate 4500 -vvv -n -Pn 172.17.0.2
```

This nmap command performs a fast and aggressive TCP scan of **all ports**.

- **-p-**: Tells nmap to scan al 65,535 ports.
- **--open**: Only shows ports that are open.
- **-sT**: Performs a TCP connect scan.
- **--min-rate 4500**: Sets the **minimum packet sending rate** to 4500 packets per second.
- **-vvv**: Enables very verbose output.
- **-n**: Disables DNS resolution.
- **-Pn**: Skips the host discovery phase.

As we can see, there are two open ports: **80** and **22**.

- **Port 80**: Used for HTTP, the protocol that serves websites over the web.
- **Port 22**: Used for SSH, which allows remote command-line access to the machine.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411172749.png)

If we enter the machine's IP address of the machine in a web browser, we are presented with a login page.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411173020.png)
## Exploitation
Since this machine is called **Injection**, we might asume that it requires **SQL Injection** to exploit. 

We'll try to exploit the machine using the following command.

```sql
admin' or 1=1-- -
```

This command is a classic **SQL Injection** payload.

- **admin'**: Closes the original string in the SQL query.
- **or 1=1**: Always evaluates to *true*, so it bypasses authentication.
- **-- -**: Comments out the rest of the SQL query to avoid syntax errors.

Since this payload tricks the application into logging in **without a valid password**, we can use whatever password we like.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411172952.png)

There you go! Now we know a **username** and **password**.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411173412.png)

Now we can access the machine via SSH using the following command:

```bash
ssh dylan@172.17.0.2
```

And we're in!

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411173541.png)
## Post Exploitation

In order to gain root access, I'm going to search for root-owned binaries using the next command:

```bash
find / -perm -4000 -user root 2</dev/null
```

This command is used to search for **SUID (Set User ID) binaries** owned by root.

- **find /**: Starts searching from the root directory (*/*).
- **-perm -4000**: Looks for files with the SUID permission set.
- **-user root**: Limits the results to files owned by the root user.
- **2</dev/null**: Redirects error messages to */dev/null* so the output is cleaner.

As we can see, we get a list of different binaries owned by root.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411173957.png)

Here, the important one is the **/usr/bin/env** binary. The main reason is that this binary can be used to **invoke programs** with custom environment variables, which may allow for privilege escalation or bypassing security mechanisms.

So, if we use these command we, could get a **shell** with root privileges.

```bash
/usr/bin/env /bin/sh -p
```

What this command does:

- **/usr/bin/env**: Runs a program in a modified environment.
- **/bin/sh**: The shell program that will be executed.
- **-p**: It tells the shell to **preserve the effective user ID**, which in this case is root, because the binary has the SUID bit set.

Once we execute the command and we get the shell, we can confirm that we are in fact the user root by typing **whoami**.

![](../assets/pictures/2025-04-12/Pasted%20image%2020250411175058.png)

We successfully escalated privileges - we're now root!