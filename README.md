# rpinode

Docker images that helps with easy deployment of bitcoin full node on a Raspberry Pi.

## Requirements

### Hardware
* A Raspberry Pi 3/Raspberry Pi 3. (Model 4 B, 4GB model Recommended).
* 16/32GB microSD card.
* Portable SSD/HDD (500GB+) to store the bitcoin blockchain.

### Software
* Git
* Docker

# Setup

- Install Raspbian on your Raspberry Pi. ([Instructions](https://www.google.com))
- Updates and Upgrade System
    ```sh
    sudo apt-get update
    sudo apt-get upgrade -y
    ```
- Install Build Essentials and Git.
    ```sh
    sudo apt-get install -y build-essential git
    ```
- Install Docker
    ```sh
    curl -sSL https://get.docker.com/ | sh
    ```
- Plug in your Portable SDD/HDD and make sure it is mounted at /mnt/usb.
  ```sh
    sudo mount /dev/sda1 /mnt/usb
  ```
  (Please refer to detailed instruction [Here](https://www.raspberrypi.org/documentation/configuration/external-storage.md))
- Reboot and Login as Pi.

# Quick Start

## Clone repository
Now that we have the hardware and software setup done. lets proceed to clone this repository
```bash
cd /home/pi
git clone https://github.com/prakashr1984/rpinode.git
cd rpinode/bitcoind
sudo chmod +x entrypoint.sh # Give execute permission for entrypoint.sh
```

## Initialize the bitcoin data directory
Now, we need to setup the directory to store the blockchain data.
```bash
#Assuming we have the harddisk mounted at /mnt/usb, run the following command
#This step will create /mnt/usb/bitcoin_data directory and copy in the bitcoin.conf file.
make init
```

## Building the image
Run the following command to build the docker image.
```bash
make build
```

## Running the image
Run the following command to run the container
```bash
#Run the docker image in background.
make run
#To view the console output run the following command
make logs  
#Or use the docker logs command directly.
docker logs -f bitcoind --tail 100
```
Or run the docker command directly
```bash
docker run -it -v /mnt/usb/bitcoin_data:/home/bitcoin/.bitcoin prakashr1984/bitcoind 
```