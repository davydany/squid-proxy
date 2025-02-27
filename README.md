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
curl https://ip.oxylabs.io/location -x http://localhost:3128/ --cacert ./cert/CA.pem
```