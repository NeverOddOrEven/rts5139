# Overview #

This is a temporary fix for RTS5129/RTS5139 USB MMC/SD CARD card reader on Linux 3.16+ kernels. On my 
Lenovo Ideapad Yoga 13 Model 20175 running Mint Cinnamon with a ```4.13.0-37-generic``` kernel I get the following errors. 

```
Jan 27 22:27:53 ideapad-yoga-13 kernel: [   48.108682] mmc0: tuning execution failed
Jan 27 22:27:53 ideapad-yoga-13 kernel: [   48.108699] mmc0: error -22 whilst initialising SD card
```

This ocurred during a transition from ```3.15``` to ```3.16``` kernel, as a result of the ```staging/rts5139``` driver (which worked with the RTS5129/RTS5139) being replaced by the newer ```rtsx``` driver (which does not work with the RTS5129/RTS5139). This project reverts back to the old drivers as a temporary measure to get things up and running again.

# Compilation instructions #

Firstly, make sure you have kernel headers and the ```build-essential``` package installed.

Checkout, build and install the replacement driver.

```
cd /tmp
git clone https://github.com/asymingt/rts5139.git
cd rts5139
make
sudo make install
```

Then, make sure you disable module autoloading (and also in the initial RAM filesystem)

```
sudo depmod -a
sudo update-initramfs -u
```

Reboot, and check to see if the card reader works.





