# Squid Forward Proxy

The goal of this project is to quickly test out instances where you need a forward proxy,
with custom SSL Certificates.

## Prerequisites
* Docker
* Docker Compose
* ~500MB of free disk space for caching
* Open ports 3128 and 4128 (if running locally)


## How to Run Proxy Server

* Clone this repository in your working directory.

```bash
git clone git@github.com:davydany/squid-proxy.git $PROJECT_HOME/squid-proxy
```

* Change directory to `$PROJECT_HOME/squid-proxy`:

```bash
$PROJECT_HOME/squid-proxy
```

* Run the Project

```bash
docker compose up 
```

## How to Use Proxy Server

This is how you'd normally do `curl`:

```bash
curl https://ip.oxylabs.io/location
```

Here is how you'd do it by using this proxy server:

```bash
curl https://ip.oxylabs.io/location -x http://localhost:4128/ --cacert ./cert/CA.pem
```

### Configure All Outbound Traffic to use Proxy Server

```bash
iptables -t nat -A OUTPUT -p tcp --dport 80 -j DNAT --to-destination 127.0.0.1:4128
iptables -t nat -A OUTPUT -p tcp --dport 443 -j DNAT --to-destination 127.0.0.1:4128
```

**RESET:** If you need to reset the commands above, do this:

```bash
iptables -t nat -D OUTPUT -p tcp --dport 80 -j DNAT --to-destination 127.0.0.1:4128
iptables -t nat -D OUTPUT -p tcp --dport 443 -j DNAT --to-destination 127.0.0.1:4128
```

Now, reset `iptables`:

```bash
iptables -t nat -F

# really reset things (if the above commands don't work)
iptables -F
iptables -t nat -F
iptables -X

# verify
iptables -t nat -L --line-numbers -v

```

