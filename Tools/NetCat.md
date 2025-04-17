# NetCat

for version recon & enumeration

netcat -v enum_sandbox 22


Let's start by browsing to http://enum-sandbox/shells/.

If a page allows you to create a bind shell on the server or send a reverse shell to our Kali VM. Pick a port that isn't already in use, so we'll type 9999. Create the Bind Shell/The application indicates the bind shell is running. connect to it with Netcat by specifying the host and port. After we connect, then run whoami and hostname to verify our connection.

Bind Shell example


netcat enum-sandbox 9999


whoami


hostname



reverse shell. Before we create the reverse shell, we need to create a listener to receive it. We'll use Netcat on our Kali VM, set -l to start in listener mode, set -v for verbose, and use -p to specify our port.


netcat -vlp 9090



Now that we have our listener running, we can create the reverse shell. We'll type our Kali VM's IP address in the "IP Address" field, 9090 in the "Port" field. The application indicates it sent the reverse shell. Let's check our Netcat listener.


netcat -vlp 9090
whoami
hostname
