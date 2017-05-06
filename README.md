# Camera
RPi Camera

sudo nano  /etc/init.d/ustream

#!/bin/bash
RTMP_URL=rtmp://1.23180756.fme.ustream.tv/ustreamVideo/23180756
STREAM_KEY=mqCAnBEgzAraxS2L6ackVrUQ2HHrQHBc
while :
do
  raspivid -n -vf -hf -t 0 -w 960 -h 540 -fps 25 -b 500000 -o - | ffmpeg -i - -vcodec copy -an -metadata title="Streaming from raspberry pi camera" -f flv $RTMP_URL/$STREAM_KEY
  sleep 2
done 

sudo chmod 755 /etc/init.d/ustream
sudo update-rc.d ustream defaults
sudo reboot
