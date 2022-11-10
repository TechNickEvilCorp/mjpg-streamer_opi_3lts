# mjpg-streamer_opi_3lts
manual how instal mjpg-streamer

## A. Setup mjpg-streamer

## Install necessary packages for mjpg-streamer

```bash
sudo apt-get update
sudo apt-get install build-essential libjpeg8-dev imagemagick libv4l-dev git cmake uvcdynctrl
```

```bash
git clone https://github.com/jacksonliam/mjpg-streamer.git
cd /mjpg-streamer/mjpg-streamer-experimental
make
sudo make install
```

## B. Run mjpg-streamer for test
```bash
sudo mjpg_streamer -i "input_uvc.so -d /dev/video1 -r 640x480 -f 14" -o "output_http.so"
```
Tou have seen steam on
```bash
yourip/webcam/?action=stream
```

## C. if all ok then activate him in systemd

```bash
sudo nano /lib/systemd/system/mjpg-streamer.service
```
insert a
```
[Unit]
Description=A server for streaming Motion-JPEG from a video capture device
After=network.target

[Service]
User=root
ExecStart=sudo mjpg_streamer -i 'input_uvc.so -d /dev/video1 -r 640x480 -f 14' -o 'output_http.so'

[Install]
WantedBy=multi-user.target
```
## d. Enable service
```bash
sudo systemctl start mjpg-streamer.service
```

## Start service
```bash
sudo systemctl enable mjpg-streamer.service
```
