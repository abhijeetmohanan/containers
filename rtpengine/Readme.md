# RTP ENGINE

An RTP Proxy.

## Load Kernel Module on Server

This step is optional and is primarily done to enable packet forwarding at the kernel level.  
If you do not need this feature, proceed with the following adjustments:  

- Remove the `-F` flag from the CLI.
- Set `no-fallback = false` in the `rtpengine.conf` file.

## Compile Kernel Module Locally on the Server  

```bash
# For Debian-based systems

apt-get update && apt-get install build-essential -y 

git clone https://github.com/sipwise/rtpengine.git rtpengine

cd rtpengine/kernel-module 

# Build the kernel module
make && make install 

# Enable the module to auto-load on reboot 
echo "xt_RTPENGINE" | sudo tee /etc/modules-load.d/rtpengine.conf

# Reboot the server
reboot 

# List the currently active modules. If the module is loaded, "xt_RTPENGINE" will appear in the output.
lsmod | grep xt_RTPENGINE

# In case of module corruption, rebuild and reinstall the module:
make clean && make && make install 
```


<b>Starting RTP Engine </b>

```bash 
docker-compose up -d # To start 
docker-compose up -d --build # To rebuild
```

## Documents 

- [Github](https://github.com/sipwise/rtpengine)
- [rtpengine manual](https://rtpengine.readthedocs.io/en/latest/rtpengine.html)
- [opensips and rtpengine](https://opensips.org/docs/modules/3.4.x/rtpengine.html)
