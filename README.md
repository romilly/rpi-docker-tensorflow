# rpi-docker-tensorflow

## Update:

Docker now officially support ARM architecture and this build uses the new Docker package for the Pi.

I tested the build using the latest version of raspbian/jessie-lite and a **16 Gb** SD card on a Raspberry Pi model 3B.

Earlier attempts using an 8Gb card failed with disk full.

The build creates a docker image for the
Raspbery Pi which contains TensorFlow, Jupyter and two TensorFlow
notebooks copied from the official Google docker TensorFlow build.

The build relies heavily on the work of resin.io, the Docker team, Sam Abrahams and
the Google TensorFlow team. Sources are listed below.

This is **not** an official TensorFlow port, so don't ask for or expect
support from the TensorFlow team.

The script builds a container based on Sam Abraham's initial release of TensorFlow 0.10 for
the Raspberry Pi.


## Build instructions

1. Install Docker on your Raspberry Pi.
  1. `curl -sSL get.docker.com | sh`
  1. `sudo usermod -aG docker pi`
  1. log out, then log back in again for the change to take effect
  1. `sudo systemctl start docker`
1. Clone this repository into a directory of your choice
  1. `git clone https://github.com/romilly/rpi-docker-tensorflow.git`
1. Build the image
  1. `cd rpi-docker-tensorflow/build-tensor-pi/`
  1. `docker build -t='yourName/rpi-docker-tensorflow' .`

## Running the image

This run instruction expects a directory called myNotebooks within your
home directory.

If you save an IPython notebook to the `myNotebooks` sub-directory
while running your container, it will get saved to the `myNotebooks`
directory on your Pi.

Notebooks saved to that directory will be _persistent_ - in other words,
they will still be there when the container is stopped and restarted.

`docker run -it -p 8888:8888 -v ~/myNotebooks:/notebooks/myNotebooks yourName/rpi-docker-tensorflow`

Previously there were some spurious warnings when the container started but the latest resin image fixes these.
(Thanks, *resinators*!)

You can *probably* ignore the warnings about the insecurity of the IPython server configuration so long as you do not store any
sensitive data or code in your notebooks.

## Connecting to the notebooks

Open a browser on `http://raspberrypi:8888` where raspberrypi is the
hostname of the Pi on which the docker image is running, or on
`http://localhost:8888` on the Pi itself.

You should see a screen like this:

aaand you're away to the races!

I'll [blog](http://blog.rareschool.com/) more info about this shortly,
and will commit the image to docker central.

## Stopping the image

In the terminal session where you ran the container, type Ctr-C twice in
quick succession. The container will stop.

# Sources

1. Docker: http://blog.alexellis.io/getting-started-with-docker-on-raspberry-pi/
1. [Base image](https://hub.docker.com/r/resin/rpi-raspbian/): from [a post by the chaps at resin.io](https://resin.io/blog/docker-on-raspberry-pi-in-4-simple-steps/)
1. [Pi tensorflow whl file](https://github.com/samjabrahams/tensorflow-on-raspberry-pi/raw/master/bin/tensorflow-0.9.0-cp27-none-linux_armv7l.whl)
from [Sam Abrahm's Github project](https://github.com/samjabrahams/tensorflow-on-raspberry-pi)
1. Notebooks and notebook config from [The Tensorflow Docker Build on Github](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/tools/docker)





   
 
 


