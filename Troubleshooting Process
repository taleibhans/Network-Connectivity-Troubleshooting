## Initial Configuration

The workstation was configured with the following IPv4 settings:

- IPv4 address: `172.16.142.132`
- Subnet mask: `255.255.255.0`
- Default gateway: `172.16.142.20`
- DNS server: `192.0.2.1`

The gateway and DNS settings were incorrect, creating two separate network problems.

## Troubleshooting Process

### 1. Reviewed the Network Configuration

I started with:

```powershell
ipconfig /all
````

This allowed me to review the workstation's IP address, subnet mask, default gateway, DNS server, and adapter configuration.

The IP address itself was valid for the local subnet, but the configured gateway and DNS server required further testing.

### 2. Tested the Local TCP/IP Stack

I tested the loopback address:

```powershell
ping 127.0.0.1
```

The test completed successfully with no packet loss.

I then pinged the workstation's own IPv4 address:

```powershell
ping 172.16.142.132
```

This also completed successfully.

These two tests helped confirm that the local TCP/IP stack and network interface were functioning.

### 3. Tested the Default Gateway

Next, I tested the configured gateway:

```powershell
ping 172.16.142.20
```

The request failed with 100% packet loss.

At this point, the issue appeared to be related to the workstation's routing configuration rather than the local network stack.

I corrected the default gateway to the proper VMware NAT gateway:

```text
172.16.142.2
```

### 4. Verified External Connectivity

After correcting the gateway, I tested connectivity to an external IP address:

```powershell
ping 8.8.8.8
```

The test completed successfully with 0% packet loss.

This confirmed that the workstation was now able to reach external networks by IP address.

However, website names still could not be resolved.

### 5. Investigated DNS

I tested DNS resolution with:

```powershell
nslookup microsoft.com
```

The lookup timed out because the workstation was still configured to use:

```text
192.0.2.1
```

as its DNS server.

Since external IP connectivity was working but hostname resolution was not, I was able to isolate the remaining problem to DNS.

I corrected the DNS server to:

```text
172.16.142.2
```

and ran the lookup again.

This time, `microsoft.com` resolved successfully.

### 6. Verified the Network Route

Once basic connectivity and DNS were restored, I used:

```powershell
tracert microsoft.com
```

to inspect the route between the workstation and the destination.

The first hop was the VMware NAT gateway at `172.16.142.2`, followed by additional routers along the path.

Some later hops did not respond to traceroute probes, but the route itself was still functioning.

### 7. Reviewed Active Network Connections

As a final investigation step, I used:

```powershell
netstat -ano
```

to review active TCP and UDP connections.

The output showed several established outbound connections, including traffic using port `443`.

I used the PID shown by `netstat` to identify which local process owned each connection.

For example:

```powershell
Get-Process -Id 11672
```

identified the process as Microsoft Edge.

I repeated the same process for other active connections and identified Windows services and management processes associated with their respective PIDs.

This demonstrated how a network connection can be traced back to the application or process that created it.

## Findings

The workstation had two separate configuration problems:

1. An incorrect default gateway prevented the system from reaching external networks.
2. An incorrect DNS server prevented hostname resolution even after internet connectivity was restored.

The troubleshooting process showed why it is important to test each layer individually instead of treating every connectivity issue as the same problem.

## Resolution

The network configuration was corrected to use:

* Default gateway: `172.16.142.2`
* DNS server: `172.16.142.2`

After making the changes:

* the local TCP/IP stack responded normally
* the workstation could reach its gateway
* external IP connectivity worked
* DNS resolution worked
* routing could be traced successfully
* active outbound network connections could be reviewed and mapped to their owning processes

## What I Learned

This lab helped me understand how different Windows networking tools fit together during troubleshooting.

`ipconfig /all` is useful for reviewing the workstation's configuration.

`ping` helps determine whether a specific system or network layer is reachable.

`nslookup` helps isolate DNS problems.

`tracert` shows the path traffic takes to a destination.

`netstat -ano` provides visibility into active connections, ports, connection states, and process IDs.

The biggest takeaway was learning to troubleshoot connectivity in stages rather than immediately changing several settings at once.

Being able to reach an IP address does not necessarily mean DNS is working, and a functioning network adapter does not necessarily mean the default gateway is configured correctly.

## Skills Demonstrated

* Windows network troubleshooting
* IPv4 configuration
* TCP/IP troubleshooting
* Default gateway analysis
* DNS troubleshooting
* `ipconfig`
* `ping`
* `nslookup`
* `tracert`
* `netstat`
* PID and process correlation
* PowerShell
* VMware networking
* Troubleshooting and verification

````

