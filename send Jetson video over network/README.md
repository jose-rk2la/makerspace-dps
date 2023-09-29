# Stream Video to a Remote Device #

If you want to stream the video feeds of any models, you can send the feed over a network provided that your host machine is running Ubuntu and both the Jetson and your host machine are on the same network.
See Jose for using it with tailscale if the Jetson and remote machine are not on the same network.

1. first install these dependencies:

```
sudo add-apt-repository universe
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-bad1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev
```  

2. run this gstreamer command on the host machine:

```
gst-launch-1.0 -v udpsrc port=1234  caps = "application/x-rtp, media=(string)video, clock-rate=(int)90000, encoding-name=(string)H264, payload=(int)96" !  rtph264depay ! decodebin ! videoconvert ! autovideosink
```

4. on the Jetson, run the `video-viewer` or `detectnet` command with an attached webcam (usually `/dev/video0` for any USB cameras) with the following command:

```
detectnet /dev/video0 rtp://<remote-ip>:1234 
```

note that you need to replace `<remote-ip>` with the ip address of the remote machine; this should send the video feed to your remote machine
