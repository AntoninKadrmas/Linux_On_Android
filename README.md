#### Download apps :
- Anduoinx
- Termux
- RVNC Viewer
#### Install linux:
1. Open Androinx 
2. Go to "Linux Distribution"
3. Select "Debian"
4. Select "CLI Only"
5. Open Termux
6. Copy "Recopy Command" from Androinx 
7. Paste and run command in Termux
8. Go through installation
!! Now you have installed linux.
#### Type to exit ubuntu:
```
exit
```
#### Type to enter ubuntu:
```
./start-debian.sh
```

#### Install LXDE:
1. update debian apt
```bash
sudo apt update
```
2. Install desktop environment LXDE
```bash
sudo apt install lxde task-lxde-desktop -y
```
3. Choose keyboard layout (I choose English)
#### Create new user:
1. Create user
```bash
useradd -m user_name -s /bin/bash
```
2.  Add user into sudoers file with same privileges as root
```bash
sudo nano /etc/sudoers
```
3. This insert into sudoers file
```
user_name   ALL=(ALL:ALL) ALL
```
4. Switch to newly created user
```bash
su - user_name
```
#### Install Tightvnc:
1. Install
```bash
sudo apt install tightvncserver
```
2. Enter vnc password (it will be used when connecting by RVNC)
```
vncserver
```
3. Stop the vncserver :x ... on port 590x
```
vncserver -kill :1
```
4. Backup xstartup file
```bash
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
```
4. Open file in some editor (if you don't have any install nano editor)
```bash
apt install nano
```
5. Open xstartup file
```bash
nano ~/.vnc/xstartup
```
6. Insert into xstartup file and save it (Ctr+x ... y)
```bash
#!/bin /bash
xrdb $HOME/.Xresources
exec startlxde &
```
7. My xstartup file looks like this
```bash
#!/bin/sh
xrdb $HOME/.Xresources
xsetroot -solid grey
#x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
#x-window-manager &
# Fix to make GNOME work
export XKL_XMODMAP_DISABLE=1
/etc/X11/Xsession
exec startlxde & # this is the line I added into file all other lines were already there
```
8. Rerun the vncserver
```
vncserver -localhost
```
#### Connect to vnc:
1. Open Real vnc
2. Create new session
3. Address: localhost:1
4. Click on connect
5. Enter password

!! You should be now in.

Error:
1. Process completed signal 9 error (could happened after some time when vnc server running)
- Enter into developer mode and allow usb debugging (on android)
- Connect device into computer
- Install android debugging bridge (android developer SDK platform tools)
- Extract download folder 
- Add path to extracted folder into environment variable
- Open command prompt
- To check if device is connected successfully (you should see device number with it's status)
```
adb devices
```
- To enter device shell
```
adb shell
```
- On android 12L, 13 enter ... I used this and it works pretty well
```
settings put global settings_enable_monitor_phantom_procs false
```
- On android 12 enter
```
/system/bin/device_config set_sync_disabled_for_tests persistent; /system/bin/device_config put activity_manager max_phantom_processes 2147483647
```


Used sites:
- https://www.fosslinux.com/64968/how-to-install-lxde-gui-in-debian-11-bullseye.htm
- https://lowendspirit.com/discussion/874/install-lxde-with-vnc-in-debian-server
- https://youtu.be/26GI3z6tI3E?si=COMnazaped-Jx80F
	- https://developer.android.com/tools/releases/platform-tools
- https://youtu.be/IlBeGznxXH8?si=nCtPDD-AVaFj47mV
