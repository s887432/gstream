# gstreamer

Tested under Ubuntu 20.04 64bits.

## environment setup

$ sudo apt-get update
$ sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gtk-doc-tools

## compile sample code

$ gcc gstreamer_basic_01.c -o gstreamer_basic_01 \`pkg-config --cflags --libs gstreamer-1.0\`

## Example

#### test pattern
$ gst-launch-1.0 videotestsrc pattern=XXXX ! video/x-raw, width=800, height=480 ! autovideosink <br>

#### show test pattern on framebuffer
$ gst-launch-1.0 videotestsrc pattern=XXXX ! video/x-raw, width=800, height=480 ! fbdevsink <br>

 <br>
where pattern is <br>
smpte (0) – SMPTE 100%% color bars <br>
snow (1) – Random (television snow) <br>
black (2) – 100%% Black <br>
white (3) – 100%% White <br>
red (4) – Red <br>
green (5) – Green <br>
blue (6) – Blue <br>
checkers-1 (7) – Checkers 1px <br>
checkers-2 (8) – Checkers 2px <br>
checkers-4 (9) – Checkers 4px <br>
checkers-8 (10) – Checkers 8px <br>
circular (11) – Circular <br>
blink (12) – Blink <br>
smpte75 (13) – SMPTE 75%% color bars <br>
zone-plate (14) – Zone plate <br>
gamut (15) – Gamut checkers <br>
chroma-zone-plate (16) – Chroma zone plate <br>
solid-color (17) – Solid color <br>
ball (18) – Moving ball <br>
smpte100 (19) – SMPTE 100%% color bars <br>
bar (20) – Bar <br>
pinwheel (21) – Pinwheel <br>
spokes (22) – Spokes <br>
gradient (23) – Gradient <br>
colors (24) – Colors <br>

#### play streaming demo video
$ gst-launch-1.0 playbin uri=https://www.freedesktop.org/software/gstreamer-sdk/data/media/sintel_trailer-480p.webm

#### with subtitle
$ gst-launch-1.0 playbin uri=https://www.freedesktop.org/software/gstreamer-sdk/data/media/sintel_trailer-480p.webm suburi=https://www.freedesktop.org/software/gstreamer-sdk/data/media/sintel_trailer_gr.srt

#### display camera
$ gst-launch-1.0 v4l2src device=/dev/video0 ! video/x-raw, format=YUY2,width=640,height=480,frame=30/1 ! videoconvert ! autovideosink <br>

where <br>
device=/dev/video0 can be ignored if only one camera available <br>
autovideosink can be xvimagesink <br>
 
#### 16:9 
$ gst-launch-1.0 v4l2src device=/dev/video0 ! video/x-raw, format=YUY2,width=640,height=480,frame=30/1 ! aspectratiocrop aspect-ratio=16/9 ! videoconvert ! autovideosink <br>
$ gst-launch-1.0 v4l2src device=/dev/video0 ! video/x-raw, format=YUY2,width=640,height=480,frame=30/1 ! aspectratiocrop aspect-ratio=16/9 ! videoconvert ! videoscale ! video/x-raw,width=800,height=480 ! autovideosink <br>

#### display on LCD
$ gst-launch-1.0 v4l2src device=/dev/video0 ! video/x-raw, format=YUY2,width=640,height=480,frame=30/1 ! videoconvert ! autovideosink <br>
<br>
$ gst-launch-1.0 v4l2src device=/dev/video0 ! video/x-raw, format=YUY2,width=640,height=480,frame=30/1 ! videoconvert ! videoscale ! video/x-raw,width=800,height=480 ! autovideosink <br>

## RTSP Server under ubuntu 2020.04

##### enviromnent setup

$ sudo apt-get install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gtk-doc-tools

###### get source code and compile
$ git clone git://anongit.freedesktop.org/gstreamer/gst-rtsp-server <br>
$ cd gst-rtsp-server <br>
$ 
$ ./autogen.sh <br>

$ make <br>

##### Launch RTSP Server
$ cd example <br>
$ ./test-launch "( videotestsrc ! x264enc ! rtph264pay name=pay0 pt=96 )" <br>

##### Client command
$ gst-launch-1.0 playbin uri=rtsp://127.0.0.1:8554/test <br>

# Patrick Lin @ Taipei
