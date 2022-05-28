## cylau0's notes

### Contact Details
- email: cylau0@gmail.com

### Technical Notes
	
#### Software Installation for utilizing ffmpeg with Intell Quick Sync Video
```
  pacman -Syu intel-media-sdk intel-media-driver pacman -Syu intel-gpu-tools libva-utils vdpauinfo
  git clone https://aur.archlinux.org/rtsp-simple-server.git
  cd rtsp-simple-server
  makepkg -si
  systemctl enable rtsp-simple-server
  systemctl start rtsp-simple-server
  systemctl status rtsp-simple-server
```
#### Using ffmpeg to transcode from a webcam, with webcam video device = /dev/video0 and alsa hw:1,0
```
  ffmpeg -init_hw_device qsv=hw -filter_hw_device hw -f v4l2 -video_size 1280x720 -input_format mjpeg -c:v mjpeg_qsv -i /dev/video0 -f alsa -channels 1 -i hw:1,0 -c:v h264_qsv -load_plugin hevc_hw -f rtsp -rtsp_transport tcp rtsp://127.0.0.1:8554/webcam -vf hwupload=extra_hw_frames=64,format=qsv -c:v h264_qsv
```
