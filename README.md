Set up a DNS server using the `4km3/dnsmasq` Docker image to resolve domains to custom IPs and log DNS queries.

Step 1:

```
docker pull 4km3/dnsmasq:latest
```

Step 2: Edit dnsmasq.conf

```
address=/example.com/<your-ip>
address=/example.org/<your-ip>
log-queries
```

Step 3: Run docker container

```
docker run --name my-dnsmasq --rm -it -p 0.0.0.0:53:53/udp -v <path-to-dnsmasq.conf-on-pc>:/etc/dnsmasq.conf --cap-add=NET_ADMIN 4km3/dnsmasq:latest -k
```

Replace <path-to-dnsmasq.conf-on-pc> with the actual path to your dnsmasq.conf file.

### Mobile Device Configuration (Android)

1. Install `rethink.apk` from `https://github.com/celzero/rethink-app` on your phone.

2. Configure the DNS settings in the rethink app:

   - Navigate to Configure > DNS > Other DNS > DNS 53 > Add DNS Proxy
   - Set Proxy Name to your DNS server's IP address
   - Set Port to 53

3. Start the DNS proxy in the rethink app.

4. Check whether DNS Spoofing is working or not by going to Chrome and visit `chrome://net-internals` and enter the target IP address to check if DNS spoofing is working correctly.
