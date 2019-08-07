# rpi-docker-tensorflow

## Warning:

This is definitely not production code, but *it runs on my machine(tm)*.

It requires the latest nightly build of Docker for the Pi.

## Background:

I originally started this project to create a simple way for Pi owners to experiment with TensorFlow.

At the time, neither Docker nor TensorFlow were officially supported on the Pi.

More recently, this project has been dormant, because

1. TensorFlow  and Docker have officially supported Raspbian for a while, and
1. While TensorFlow *will run* in a Docker container with Jupyter, the limited memory of the Pi 3B+
meant that you couldn't do much with it.

This has changed with the 4 GB model of the Pi 4B.

I'm now attempting an experimental build for Raspbian buster that runs on a Raspberry Pi 4.

I am testing the build using Raspbian/buster and a 16 GB SD card on a Raspberry Pi model 4B with 4 GB of RAM.

The script builds a container based on
[Katsuya Hyodo's build of TensorFlow 1.14](https://github.com/PINTO0309/Tensorflow-bin) for
the Raspberry Pi, with TensorFlow Lite enabled.

The docker image contains TensorFlow, Jupyter and a TensorFlow
notebook copied from the official Google docker TensorFlow build.

The original build relied heavily on the work of resin.io, the Docker team, Sam Abrahams and
the Google TensorFlow team. Sources are listed below.

This is **not** an official TensorFlow port, so don't ask for or expect
support from the TensorFlow team.



## Build instructions

1. Install Docker nighly build on your Raspberry Pi.
  1. `curl -fsSL get.docker.com | CHANNEL=nightly sh`
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

You can *probably* ignore the warnings about the insecurity of the IPython server configuration so long as you do not store any
sensitive data or code in your notebooks.

## Connecting to the notebooks

Open a browser on `http://raspberrypi:8888` where raspberrypi is the
hostname of the Pi on which the docker image is running, or on
`http://localhost:8888` on the Pi itself.

You should see a screen like this:

aaand you're away to the races!

I'll [blog](http://blog.rareschool.com/) more info about this shortly,
and will commit the image to docker central once it's working.

## Stopping the image

In the terminal session where you ran the container, type Ctr-C twice in
quick succession. The container will stop.

# Sources

1. Docker: http://blog.alexellis.io/getting-started-with-docker-on-raspberry-pi/
1. [Katsuya Hyodo's build of TensorFlow 1.14](https://github.com/PINTO0309/Tensorflow-bin) for
1. Notebook from [The Tensorflow website](https://www.tensorflow.org/tutorials)





   
 
 


