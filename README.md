# vm-detach-go
vm-detach-go is a helper program for those using VFIO with only one keyboard and mouse while using looking-glass.
The idea is to setup a "Software based KVM switch" by downloading putty and and wants to be able to have this program in the same folder as putty and have a putty session saved named "vm-detach" which is pre-configured with the ssh-key to login to your hosts root account which will autorun a command (because we are using that key), the process for setting it up is described here:<br>
https://github.com/rokups/rokups.github.io/blob/master/pages/full-software-kvm-switch.md<br>
however you can ignore the ddcutil and clickmonitorDDC requirements.


This program is preconfigured to use CTRL+ALT+SPACE, however you can change this inside hotkeys.ini file (which is also in the same directory as putty and the vm-detach.exe file)

hotkeys.ini looks like this
```ini
Modkeys=ctrl+alt
Hotkey=space
```



Valid modkeys are CTRL, ALT, SHIFT and WIN. If you want to use a combination of keys you just chain them with + so to hold ctrl and shift while pressing your hotkey, just write ctrl+shift inside the Modkeys option.<br>
Note: the WIN key is reserved for many functions (also unimplemented ones) making it close to impossible to use it for hotkeys without using multiple modkeys, so you will have to experiment.

The Hotkey is the key you want to press while holding down the Modkeys in order to trigger vm-detach to run putty in the background to tell your host machine that you want to disconnect your physical mouse and keyboard from the Guest OS.
You can find all the valid keys here (just remove **VK_** from the button name so in order to use the spacebar you would type just **space** instead of **vk_space**)<br>
NOTE: all values after the = sign in hotkeys.ini is case-insensitive.




In order to compile the program yourself you need to install golang, once you have golang you must install 2 modules using `go get`
```bash
go get github.com/MakeNowJust/hotkey
go get gopkg.in/ini.v1
```


then clone the repository
```bash
git clone https://github.com/HikariKnight/vm-detach-go.git
cd vm-detach-go
```


Build command for windows using your golang environment (if you want a version with a cmd output window just remove `-ldflags -H=windowsgui`)
```bash
mkdir bin
cd src\
go build -o ..\vm-detach.exe -v -ldflags -H=windowsgui app\vm-detach.go
cp hotkeys.ini ..\bin\
```


Build command for unix systems (for a debug version just replace `release` with `debug`)
```bash
./src/build release
```



You will now have the compiled program inside the bin folder that is made in the beginning of the git repository.
