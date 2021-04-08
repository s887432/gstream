# gstreamer

Tested under Ubuntu 20.04 64bits.

## environment setup

$ sudo apt-get update
$ sudo apt install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gtk-doc-tools

## compile sample code

$ gcc gstreamer_basic_01.c -o gstreamer_basic_01 \`pkg-config --cflags --libs gstreamer-1.0\`

## RTSP Server under ubunto 2020.04

##### enviromnent setup

$ libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gtk-doc-tools

###### get source code and compile
$ git clone git://anongit.freedesktop.org/gstreamer/gst-rtsp-server
$ cd gst-rtsp-server
$ ./autogen.sh

$ make

##### Launch RTSP Server
$ cd example
$ ./test-launch "( videotestsrc ! x264enc ! rtph264pay name=pay0 pt=96 )"

##### client command
$ gst-launch-1.0 playbin uri=rtsp://127.0.0.1:8554/test

Patrick Lin
