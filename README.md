# RaspiCam-gstreamer
Live Web Streaming on the Raspberry Pi using gstreamer

# What is Gstreamer
gstreamer allows you to stream video with very low latency – a problem with VLC currently.  The catch is that you need need gstreamer on the client used to view the stream.  gstreamer is a development framework not a media player and there isn't a way to stream so that common players such as VLC can display the stream (without users having to install complex plugins).  So, gstreamer can provide an excellent low latency video link, which is great if you are techy enough to set it up at both ends, but its no good if you want to directly stream so that Joe public can see the video on a web site for instance.

For more information visit :- [Gstreamer](http://gstreamer.freedesktop.org/)

## Setting Up The Raspberry Pi To Use gstreamer
You need to edit the sources.list file so enter:


`sudo nano /etc/apt/sources.list`

and add the following to the end of the file:


`deb http://vontaene.de/raspbian-updates/ . main`

Press CTRL+X to save and exit

Now run an update (which will make use of the line just added):


sudo apt-get update 
Now install gstreamer


`sudo apt-get install gstreamer1.0` 

Note : You may have to install some gstreamer tools also, for more about this visit the [Gstreamer](http://gstreamer.freedesktop.org/) website

# To Stream The Video From the Raspberry Pi

#### Cloning this repository onto the Raspberry Pi

To install git:

    opkg install git

Then clone this repository using `git clone <git repo URL>`.

Edit the Shell Script :-

` nano stream_tcp.sh`

Here instead of RASPBERRYIP put the ip address of your pi.

The ip address of your pi can be found out by:-

` ifconfig `

Now run the Shell Script :-

` ./stream_tcp.sh `

# On the Client Machine view the Stream

### For Windows :-

Download Gstreamer from :- [Gstreamer](http://gstreamer.freedesktop.org/download)

Install the GStreamer Software :-

Do a Complete Install, as Typical Install leads to an error in the end.

Run command prompt as administrator

cd to the directory where GStreamer installed :-

For me it is : 
`cd E:`
`cd gstreamer/1.0/x86_64/bin`

Now type the following command on the command prompt :-

` gst-launch-1.0 -v tcpclientsrc host=VIDSERVERIP port=5000 ! gdpdepay ! rtph264depay ! avdec_h264 ! videoconvert ! autovideosink sync=false`

Where <VIDSERVERIP> is the IP Address of your Raspberry Pi.

And Boom....
You can now see the Stream on you're Windows Machine.........

### For Linux

Launch a terminal and type

` gst-launch-1.0 -v tcpclientsrc host=<IP-OF-THE-RPI> port=5000  ! gdpdepay !  rtph264depay ! avdec_h264 ! videoconvert ! autovideosink sync=false`

Where <IP-OF-THE-PI> is the IP Address of your Raspberry Pi.

### For MAC OSX

Launch a terminal and type

`gst-launch-1.0 -v tcpclientsrc host=<IP-OF-THE-RPI> port=5000  ! gdpdepay !  rtph264depay ! avdec_h264 ! videoconvert ! osxvideosink sync=false `

Where <IP-OF-THE-PI> is the IP Address of your Raspberry Pi.

And Enjoy!!!!!!!
