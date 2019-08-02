# Configuring the camera

While basic configuration options are available through the Web UI, many more advanced settings can
only be set through a configuration file. These config files use the
[JSON](https://en.wikipedia.org/wiki/JSON) notation. Only the key/value pairs for settings that are
to be changed need to be included, all other settings will remain unmodified when the config file
is applied.



The most important settings you may be interested in are listed below. The full list of available settings including their documentation, data types and, where relevant, allowed ranges or value sets, can be found in file *Settings.java*.

* ScheduleInterval
* CamExposureMode
* CamFocusMode
* CamISO
* DetectorInputAlignment
* JPEGQuality
* EnableRadar
* VideoBitrate
* VideoCaptureDuration
* VideoCaptureFPS
* VideoPlaybackFPS
* VideoReso
* VideoStillReso
* VideoThumbnailReso
* EnableNumberPlateDetection
* EnableNumberPlateRecognition
* EnableVideoUpload
* Pause
* PauseRadar
* LiveViewCount
* LiveViewFPS
* LiveViewReso
* RadarMinSpeed
* USBBaudRate
* USBCommand
* USBDataBits
* USBParity
* USBStopBits
* VehicleMotionFilterAngles
* VehicleMotionFilterAngleTolerance
* VehicleMotionFilterMinMagnitude

Do not include the following critical settings unless you are confident the values are correct. Invalid values will disconnect the cam from the cloud.

* AwsKeyId
* AwsKeySecret
* AwsUserName
* AwsBucket

## Applying the config

The JSON config file is generally uploaded to AWS S3, from where the camera will fetch it. The path
and name of the file must be as follows `bucket/config/camera_id/config-s3.json`. For example,
a config file for the camera with ID `dfrhe45hbh` can be uploaded with this command:

```
aws s3 cp config-s3.json s3://xyzanpr-474j7eng54/config/dfrhe45hbh/config-s3.json
```

The camera looks for new config files on regular intervals, so you are done if you do not need the
config to be applied immediately. If you do, then the camera can easily be triggered to check for a
new config file by sending an SMS to it with the message `password download`, where `password` is
the camera's individual SMS password.

The processed and applied configuration set is uploaded back to the same location under subfolder `hist`. You can examine it to see if the requested change was applied correctly.

## Examples

Here is a simple config file with a single setting that will pause all actions triggered by the
radar (i.e. image capture and analysis), but will not turn it off completely so that speed readings
continue to be recorded:

```json
{
  "PauseRadar": 1
}
```

To re-enable full radar functionality, the value needs to be set back to `0` (we use `0` and `1`
for boolean values `false` and `true` respectively).
 
To ensure the radar is enabled, unpaused and set to report speed values above 30 km/h, the following
config file can be applied:

```json
{
  "EnableRadar": 1,
  "PauseRadar": 0,
  "RadarMinSpeed": 30
}
```

### Motion filter

The cam only processes vehicles moving in a specified direction encoded as an angle of motion in relation to the camera.

To configure the motion filter to only pass vehicles driving diagonally towards the camera, which is
the case when the camera itself is installed on the side of a road and slightly angled towards it,
the following configurations can be used.

When the camera is on the side of the oncoming traffic:

```json
{
  "VehicleMotionFilterAngleTolerance": 40,
  "VehicleMotionFilterAngles": -40
}
```

If the camera is instead installed on the opposite side of the road, then something similar to the
following would be required instead:

```json
{
  "VehicleMotionFilterAngleTolerance": 40,
  "VehicleMotionFilterAngles": 40
}
```

The motion filter angle describes the allowed angle of motion of vehicles as seen when overlaying a
coordinate system on a photo taken by the camera, with the positive y-axis extending towards the
bottom of the image. Positive angles describe counter-clockwise rotation from this axis and negative
angles clockwise rotation. The tolerance describes the angular region around this direction that is
accepted by the filter.

### App upgrade

Place the package in an S3 folder the cam can access (e.g. `app/deviceid/`) and use the following config setting to initiate the upgrade. Note, the file name and the version will be different.

```json
{
    "AwsAppName": "app/dfrhe45hbh/sensorable_cam_with_libbgsub_libtf.v893.tgz"
}
```

### USB Commands

Use the `USBCommand` property to send a command to the radar or any other connected USB device.

The value must be based64 encoded. https://www.base64encode.org/ and https://www.base64decode.org/ can help with converting ASCII values to/from base64.

* ASCII command: `set:RS=46`
* Config file: `{"USBCommand":"c2V0OlJTPTQ2IA=="}`

The cam **does not apply the command** if it is identical to the previous one. For example, if you need to send `info` command more than once one after the other you can add an end of line character to make them syntactically different:
```json
{"USBCommand":"aW5mbw=="}
{"USBCommand":"aW5mbwo="} (same as before + EOL)
```

**Get all the important settings**: `{"USBCommand":"Z2V0OkhJCmdldDpMTwpnZXQ6VU4KZ2V0OlNGCmdldDpTVApnZXQ6TU8KZ2V0Ok1ECmdldDpIVApnZXQ6VFIKZ2V0OlJT"}`

**Speed and format**:
115200 baud, 8 bit/no parity/1 stop, ASCII, + and CRLF
* set:RS=46
`{"USBCommand":"c2V0OlJTPTQ2IA=="}`

* get:UN
`{"USBCommand":"Z2V0OlVO"}`

* set:UN=1
`{"USBCommand":"c2V0OlVOPTE="}`

**Demo mode**:
* set:SF=-32767
`{"USBCommand":"c2V0OlNGPS0zMjc2Nwo="}`

**Strongest target:**
* set:SF=0
`{"USBCommand":"c2V0OlNGPTA="}`

**Sensitivity**

* info
* set:RS=46
* set:UN=1
* set:SF=0
* set:LO=0
* set:HI=150
* set:ST=25

`{"USBCommand":"c2V0OkxPPTAKc2V0OkhJPTE1MApzZXQ6U1Q9MjUK"}`


**All combined**

* info
* set:RS=46
* set:UN=1
* set:SF=0
* set:LO=0
* set:HI=150
* set:ST=25
* get:HI
* get:LO
* get:UN
* get:SF
* get:ST
* get:MO
* get:MD
* get:HT
* get:TR
* get:RS

`{"USBCommand":"aW5mbw0Kc2V0OlJTPTQ2DQpzZXQ6VU49MQ0Kc2V0OlNGPTANCnNldDpMTz0wDQpzZXQ6SEk9MTUwDQpzZXQ6U1Q9MjUNCmdldDpISQ0KZ2V0OkxPDQpnZXQ6VU4NCmdldDpTRg0KZ2V0OlNUDQpnZXQ6TU8NCmdldDpNRA0KZ2V0OkhUDQpnZXQ6VFINCmdldDpSUw0K"}`

