# Handyplex
Handyplex allows you to control Plex via the XBox Kinect hardware. Using
simple hand gestures you can navigate through your library and initiate
playback commands such as Play/Pause, Volume Up/Down and Fast-Forward/Rewind.

See Handyplex in action: http://www.youtube.com/watch?v=wFM7pVMLIY4

Handyplex is currently a proof of concept and thus far has been tested
successfully on Mac OS X 10.6.8 (Snow Leopard) running Plex 0.9.3.4, and
Mac OS X 10.7 (Lion) running Plex 0.9.5.2 (Laika). Since all used libraries are
cross-platform, it should run on other platforms too.

Due to the experimental state of Handyplex one needs to be adept with the command
line to build and install dependencies, but hopefully the following instructions
will help you along.

## Requirements
To use Handyplex you'll need the following:

* Mac OS X Snow Leopard (other platforms might work, depending on
  OpenNI/Nite support)
* Python 2.7
* Plex (tested with 0.9.3.4 and 0.9.5.2)
* OSCeleton and it's dependencies

Hardware:

* Microsoft Xbox Kinect Camera

## Installing
The following is an abridged version of the installation instructions,
see the supplied INSTALL file for step-by-step instructions.

Make sure Python 2.7 (or later) is installed correctly. I recommend
[virtualenv](http://pypi.python.org/pypi/virtualenv) and [pip](http://www.pip-installer.org) to set up your Python environments.


1. Install OSCeleton and follow the instructions to install the OpenNI/NITE
   dependencies: [OSCeleton](https://github.com/Sensebloom/OSCeleton)
1. Clone Handyplex
1. Install Handyplex's Python dependencies. The easiest way to do this
   is to use pip with the supplied requirements.txt:

        $ pip install -r requirements.txt

   See [pip](http://www.pip-installer.org/en/latest/index.html) for more information.

(Optional) Install [wxPython](http://www.wxpython.org/) to play sounds when users are detected/lost.

## Configuring
Handyplex needs to know the IP where Plex Media Server is running, as well as
the name of the computer on which the Plex client is running.
Edit the following lines of settings.py accordingly:

    PLEX_SERVER_IP = '10.0.1.1'
    PLEX_CLIENT_NAME = 'mini.local'

For Handyplex to start OSCeleton you'll need to specify the directory where
the executable resides:

    OSCELETON_PATH = '/Users/mini/Development/OSCeleton'


## Using Handyplex
Make sure Plex is running, and the Kinect is connected via USB and is
receiving power.

1. Run Handyplex:

        $ python handyplex.py

1. Initiate gesture recognition with a 'wave' gesture. You should hear a
   sound letting you know your hand is recognized (if you have wxPython 
   installed), and should be good to go.


### Gesture Recognition
To get a feel for how the gesture recognition works see the demo video
on Youtube http://www.youtube.com/watch?v=wFM7pVMLIY4

#### Wave Gesture
To initiate gesture recognition start with a 'wave' gesture. Move your
hand on a horizontal axis 3 or 4 times, as if you are waving to
somebody.

#### Hold Gesture
Hold gestures are necessary to determine the start point for further
gesture recognition. Simply hold your hand in one place for a short
amount of time.

#### Swipe Gestures
Swipe gestures are best recognized if performed in a short motion, either
left, right, up, down, forwards or backwards. To implement a flick,
perform a swipe gesture and quickly move your hand back to the starting
position.

#### Repeating Swipe Gestures
If you 'hold' a gesture after it has been detected it
Handyplex will recognize 'repeat' actions, repeatedly performing the
last detected action. Repeat actions can be accelerated/decelerated by
moving your hand further away or closer to the gesture recognition
point. Only movements in the same direction as the original gesture are
considered to be repeat movements, moving your hand too far off the
original axis cancels the repeat action.

#### Fine-tuning
If you feel gesture recognition isn't working as smoothly as in the
demo video you might want to play around with the different thresholds
in settings.py.


## Running Unit Tests
Either run the tests individually, or use unittest test discover
functionality (run in tests directory):

    $ python -m unittest discover


## Known Issues
* Since there currently is no 'stop gesture recognition' command, you need to
  hide your hand (behind your back for example) in order to stop gesture
  recognition.
* Sometimes a gesture is not recognized with a small movements, move your
  hand in a exaggerated motion to one direction to reset.

## Future Plans
* Implement a gesture for ending further gesture recognition until
  user re-initializes session with 'wave'.
* Have PlexController send key commands instead of using the HTTP API
  for more flexibility.
* Use NITE's gesture recognition instead of the current Python
  implementation.
* Support for multi-hand gestures.

## Feedback
All feedback is very welcome.
Please use the github issue tracker to report issues, and the
[Plex forums](http://forums.plexapp.com/index.php/topic/33696-proof-of-concept-plex-with-kinect/)
for feedback / discussion.

The source code of Handyplex is available on Github:
https://github.com/jopdeklein/Handyplex
