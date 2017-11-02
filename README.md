# Meta

This tool is to be used to simulate EC2 metadata API on local, I use this all the time to
test my `chef` provisioning in vagrant before actually deploy it as base auto scale/instantiaton AMI

## Building

When running on a testing vagrant VM, clone, then build and run the repo with:

```bash
go get github.com/julienschmidt/httprouter
go build
./go-dummy-metadata
```

## Usage

This package does not show the API commands, but will display data when a valid endpoint is accessed.

First, route all packets poriginating from localhost with the destination of 169.254.169.254 back to 127.0.0.1.

**DO NOT DO THIS IN PRODUCTION - THIS IS ONLY FOR TESTING**

```bash
iptables -t nat -A OUTPUT -d 169.254.169.254 -j DNAT --to-destination 127.0.0.1
```

Then, simply execute GET requests against the normal EC2 metadata endpoint as you normally would on an EC2 instance:

```bash
$> curl http://169.254.169.254/latest/meta-data/ami-id

ami-5cdummy
```