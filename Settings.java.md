```java
  /**
   * The keys used to access configuration values.
   */
  public enum ConfigKeys {
    /**
     * Codeword to be included in SMS messages to authenticate a superuser command.
     */
    SmsCodeword(String.class, ""),
    /**
     * Codeword to be included in SMS messages to authenticate a user command.
     */
    SmsUserCodeword(String.class, ""),
    /**
     * The public key for AWS.
     */
    AwsKeyId(String.class, ""),
    /**
     * The secret key for AWS.
     */
    AwsKeySecret(String.class, ""),
    /**
     * The AWS user name for the device.
     */
    AwsUserName(String.class, ""),
    /**
     * The AWS S3 bucket to use for uploading and downloading of files.
     */
    AwsBucket(String.class, ""),
    /**
     * S3 path to the latest APK update archive.
     */
    AwsAppName(String.class, ""),
    /**
     * S3 path to the latest health monitor service update archive.
     */
    AwsHealthMonitorName(String.class, ""),
    /**
     * S3 path to the latest image mask file.
     */
    AwsImageMaskName(String.class, ""),
    /**
     * The region to use for AWS Rekognition. Defaults to ap-southeast-2 (Sydney).
     */
    AwsRekognitionRegion(String.class, "ap-southeast-2"),
    /**
     * S3 path to the latest system tools update archive.
     */
    AwsToolsName(String.class, ""),
    /**
     * S3 path to the latest updater executable update archive.
     */
    AwsUpdaterName(String.class, ""),
    /**
     * S3 path to the latest stand-alone upgrade script file.
     */
    AwsUpgradeName(String.class, ""),
    /**
     * Time from which interval-based scheduled photo taking is enabled. Format: hh:mm.
     */
    ScheduleFrom(String.class, ""),
    /**
     * Time after which interval-based scheduled photo taking is disabled (inclusive).
     * Format: hh:mm.
     */
    ScheduleTo(String.class, ""),
    /**
     * The interval at which {@link ScheduleReceiver} is triggered, in minutes.
     */
    ScheduleInterval(Integer.class, 0),
    /**
     * The times at which {@link ScheduleReceiver} is triggered. These times are <b>not</b>
     * restricted by the time range [ScheduleFrom, ScheduleTo]. Comma-separated list of type
     * String, with elements formatted as: hh:mm. Example: "06:00, 13:30, 20:00".
     */
    ScheduleTimes(String[].class, EMPTY_STRING_ARRAY),
    /**
     * The maximum size for the longer side of the dimensions for photos taken on a recurring
     * schedule. See {@link #ScheduleInterval}.
     */
    ScheduleReso(Integer.class, Settings.DEFAULT_RESO),
    /**
     * The maximum size for the longer side of the dimensions for photos taken on a timed schedule.
     * See {@link #ScheduleTimes}.
     */
    ScheduleTimesReso(Integer.class, Settings.DEFAULT_RESO),
    /**
     * The maximum size for the longer side of the dimensions for event-triggered photos.
     */
    CamReso(Integer.class, Settings.DEFAULT_RESO),
    /**
     * The preferred aspect ratio for photos. Some {@link #CamFormat}s may support less aspect
     * ratios than others, in which case they fall back to 4:3. One of {"4:3", "16:9"}.
     */
    CamAspectRatio(String.class, "4:3"),
    /**
     * The camera configuration schedule. Format: Array of JSON objects with keys from
     * {@link CamScheduleKeys}.
     */
    CamSchedule(String.class, ""),
    /**
     * The camera edge enhancement mode. One of {off, fast, quality}.
     */
    CamEdgeMode(String.class, "fast"),
    /**
     * The camera noise reduction mode. One of {off, fast, quality}.
     */
    CamNoiseReductionMode(String.class, "fast"),
    /**
     * The camera tonemapping mode. One of {fast, quality}.
     */
    CamTonemapMode(String.class, "fast"),
    /**
     * The AE metering area. A rectangle described by percentage offsets left, top, right, bottom
     * from the top-left corner of the final image. List of int with values in range [0, 100].
     */
    CamExposureArea(int[].class, EMPTY_INT_ARRAY),
    /**
     * The camera exposure mode. One of {"auto", "manual"}.
     */
    CamExposureMode(String.class, "auto"),
    /**
     * The exposure time for use with manual exposure, in milliseconds.
     */
    CamExposureTime(Integer.class, 20),
    /**
     * The AF metering area. A rectangle described by percentage offsets left, top, right, bottom
     * from the top-left corner of the final image. List of int with values in range [0, 100].
     */
    CamFocusArea(int[].class, EMPTY_INT_ARRAY),
    /**
     * The camera focus mode. One of {"auto", "infinity"}.
     */
    CamFocusMode(String.class, "auto"),
    /**
     * The image format to capture. One of {"jpg", "raw"}.
     */
    CamFormat(String.class, "jpg"),
    /**
     * The ISO sensitivity for use with manual exposure.
     */
    CamISO(Integer.class, 200),
    /**
     * The camera capture mode. One of {photo, video}.
     */
    CamMode(String.class, "photo"),
    /**
     * The number of photos to capture per request. 0 for infinite (the sequence must be ended
     * explicitly).
     */
    CamRepeatCount(Integer.class, 1),
    /**
     * The target frame rate at which to capture repeating photos.
     */
    CamRepeatFPS(Double.class, 1.),
    /**
     * Lock capture settings (e.g. exposure) for the entire repeating photo sequence.
     */
    CamRepeatLocked(Boolean.class, false),
    /**
     * The AWB metering area. A rectangle described by percentage offsets left, top, right, bottom
     * from the top-left corner of the final image. List of int with values in range [0, 100].
     */
    CamWhiteBalanceArea(int[].class, EMPTY_INT_ARRAY),
    /**
     * Optional DCRaw arguments. These will be appended to the required options -w -c.
     */
    DCRawArgs(String.class, "-b 1.0"),
    /**
     * Enable the radar service.
     */
    EnableRadar(Boolean.class, false),
    /**
     * The region to crop images to before upload or further processing, specified as a list of
     * normalised values: x_offset, y_offset, width, height. Comma-separated list of type double
     * with 0 or 4 values.
     */
    ImageCropRegion(double[].class, EMPTY_DOUBLE_ARRAY),
    /**
     * The JPEG encoding quality. Range [0, 100].
     */
    JPEGQuality(Integer.class, 80),
    /**
     * The video encoding bit rate in bits/sec.
     */
    VideoBitrate(Integer.class, 5000000),
    /**
     * The video capture duration in milliseconds. The playback duration depends on the capture
     * duration, the capture rate and the playback rate.
     */
    VideoCaptureDuration(Integer.class, 10 * 1000),
    /**
     * The video capture rate in frames per second.
     */
    VideoCaptureFPS(Double.class, 1.),
    /**
     * The video playback rate in frames per second.
     */
    VideoPlaybackFPS(Integer.class, 5),
    /**
     * The video resolution. Format wxh. Example: 1920x1080 or 1280x720.
     */
    VideoReso(String.class, "1920x1080"),
    /**
     * The maximum size for the longer side of the dimensions for still captures taken during video
     * recording.
     */
    VideoStillReso(Integer.class, 1920),
    /**
     * The maximum size for the longer side of the dimensions for thumbnails captured during video
     * recording. A value of 0 disables thumbnail capture when possible.
     */
    VideoThumbnailReso(Integer.class, 0),
    /**
     * Enables uploading of computational data, such as frames used for image analysis.
     */
    EnableDataUpload(Boolean.class, false),
    /**
     * Enable number plate detection (localisation).
     */
    EnableNumberPlateDetection(Boolean.class, false),
    /**
     * Enable number plate recognition (OCR).
     */
    EnableNumberPlateRecognition(Boolean.class, false),
    /**
     * Enables uploading of videos.
     */
    EnableVideoUpload(Boolean.class, false),
    /**
     * The maximum size, in bytes, for a file to be uploaded.
     */
    MaxUploadSize(Long.class, 10 * 1024L * 1024L),
    /**
     * Enable Wifi.
     */
    UseWifi(Boolean.class, false),
    /**
     * Indicates whether the network broadcasts its SSID or not. Must be set to 1 (true) for hidden
     * networks.
     */
    WifiIsHidden(Boolean.class, false),
    /**
     * The WiFi pre-shared key.
     */
    WifiPSK(String.class, ""),
    /**
     * The access point SSID.
     */
    WifiSSID(String.class, ""),
    /**
     * Pause picture taking.
     */
    Pause(Boolean.class, false),
    /**
     * Pause the radar. This does not disable the service (see {@link #EnableRadar}), but it pauses
     * actions triggered by radar events.
     */
    PauseRadar(Boolean.class, false),
    /**
     * Force radios to always be enabled (i.e. disallow airplane mode).
     */
    RadioAlwaysOn(Boolean.class, true),
    /**
     * Sensor activation rules. Format: Array of JSON objects with keys from
     * {@link BleActivationsKeys}
     */
    BleActivations(String.class, ""),
    /**
     * Enable the Bluetoooth LE scanner.
     */
    BleOn(Boolean.class, false),
    /**
     * Scan duration in milliseconds.
     */
    BleDuration(Long.class, 3000L),
    /**
     * Delay between scan intervals in milliseconds.
     */
    BleDelay(Long.class, 2000L),
    /**
     * This many milliseconds may be added to BleDelay to schedule more efficiently.
     */
    BleFlex(Long.class, 200L),
    /**
     * One of the scan modes in {@link android.bluetooth.le.ScanSettings}. One of {0, 1, 2}.
     */
    BleScanMode(Integer.class, 2),
    /**
     * Device address filter. Comma-separated list of type String. Example:
     * "60:03:08:B7:F3:9B, AC:23:3F:A0:05:29".
     */
    BleDeviceAddresses(String[].class, EMPTY_STRING_ARRAY),
    /**
     * Service UUID filter. Comma-separated list of type String.
     */
    BleServiceUUIDs(String[].class, EMPTY_STRING_ARRAY),
    /**
     * The maximum frequency in milliseconds at which photos and sync tasks are triggered by BLE
     * sensors (i.e. the minimum wait between honoured requests).
     */
    BleMaxFrequency(Long.class, 30000L),
    /**
     * The minimum number of activations from different sensors in interval
     * {@link #BleMinActivationsDuration} required to trigger a photo.
     */
    BleMinActivations(Integer.class, 1),
    /**
     * The duration in milliseconds to wait for {@link #BleMinActivations} devices to trigger.
     */
    BleMinActivationsDuration(Long.class, 0L),
    /**
     * The duration, in seconds, to taper by if the maximum possible number of activations have been
     * observed during {@link #BleTaperWindow}.
     */
    BleTaperMaxDuration(Integer.class, 3600),
    /**
     * Parameter a for the tapering equation.
     */
    BleTaperParamA(Double.class, 30.),
    /**
     * Parameter b for the tapering equation.
     */
    BleTaperParamB(Double.class, 10.),
    /**
     * Parameter c for the tapering equation.
     */
    BleTaperParamC(Double.class, 30.),
    /**
     * The coefficient to the linear term of the tapering equation.
     */
    BleTaperParamLinear(Double.class, 1.),
    /**
     * The size of the window of time, ending at the current time, for which to count sensor
     * activations for the tapering equation, in seconds.
     */
    BleTaperWindow(Integer.class, 3600),
    /**
     * The duration, in milliseconds, before the output display is cleared. Zero disables automatic
     * clearing.
     */
    DisplayDuration(Integer.class, 5000),
    /**
     * The output line of the display to use for speed values. If unset or negative, the output is
     * disabled.
     */
    DisplayLineNumberPlate(Integer.class, -1),
    /**
     * The output line of the display to use for number plates. If unset or negative, the output is
     * disabled.
     */
    DisplayLineSpeed(Integer.class, -1),
    /**
     * Device address filter for light relays. Comma-separated list of type String.
     */
    LightAddresses(String[].class, EMPTY_STRING_ARRAY),
    /**
     * Time from which lights are enabled. Format: hh:mm.
     */
    LightsFrom(String.class, ""),
    /**
     * Time after which lights are disabled (inclusive). Format: hh:mm.
     */
    LightsTo(String.class, ""),
    /**
     * The number of photos to capture per live view request. Value > 0.
     */
    LiveViewCount(Integer.class, 30),
    /**
     * The target frame rate at which to capture live view photos.
     */
    LiveViewFPS(Double.class, 1.),
    /**
     * The maximum size for the longer side of the dimensions for live view photos.
     */
    LiveViewReso(Integer.class, 640),
    /**
     * The location update interval, in minutes.
     */
    LocationUpdateInterval(Integer.class, 60),
    /**
     * The log level. Only message at or above this level will be written to log files. One of
     * {VERBOSE, DEBUG, INFO, WARN, ERROR}.
     */
    LogLevel(String.class, "INFO"),
    /**
     * The region of the image used as input to the object detector. This is expressed by specifying
     * how the square receptive field is positioned in the input image. Its edge length is always
     * equal to the shorter side of the image. The alignment is specified in view-orientation of
     * the input (i.e. after rotation).
     * <p>
     * One of {start, end, centre}, where "start" refers to either left (landscape) or top
     * (portrait) alignment and "end" refers to right (landscape) or bottom (portrait) alignment.
     */
    DetectorInputAlignment(String.class, "centre"),
    /**
     * The longest exposure time for the object detector, in milliseconds. When the actual exposure
     * is longer than specified, the capture will be aborted and no further captures will be
     * performed for a fixed duration.
     */
    DetectorMaxExposureTime(Integer.class, 32),
    /**
     * The maximum number of frames in which no number plate can be detected after at least one
     * successful detection. When this threshold is exceeded, the current recording will be stopped.
     */
    NumberPlateMaxFailedDetections(Integer.class, 3),
    /**
     * The minimum confidence for number plate localisation. Range [0, 100].
     */
    NumberPlateBboxMinConfidence(Double.class, 40.),
    /**
     * The minimum confidence for number plate recognition. Range [0, 100].
     */
    NumberPlateOCRMinConfidence(Double.class, 40.),
    /**
     * The minimum confidence for vehicle localisation. Range [0, 100].
     */
    VehicleBboxMinConfidence(Double.class, 50.),
    /**
     * The angle of tolerance from the {@link #VehicleMotionFilterAngles}, in degrees.
     * Range [0, 180].
     */
    VehicleMotionFilterAngleTolerance(Double.class, 45.),
    /**
     * A filter for the allowed angles of motion of a vehicle between consecutive frames, in
     * counterclockwise degrees from the positive y-axis (i.e. the vertical image dimension, with
     * increasing values towards the bottom). Comma-separated list of type double with values in
     * [-180, 180]. If unset or empty, the filter is disabled.
     */
    VehicleMotionFilterAngles(double[].class, EMPTY_DOUBLE_ARRAY),
    /**
     * A high-pass filter for the normalised magnitude of motion of a vehicle between consecutive
     * frames. Range [0, sqrt(1+1)] (i.e. up to the normalised diagonal length).
     */
    VehicleMotionFilterMinMagnitude(Double.class, 0.007),
    /**
     * The shortest period, in milliseconds, at which radar readings are broadcast.
     */
    RadarMaxFrequency(Integer.class, 0),
    /**
     * The minimum speed reading for an event to be broadcast.
     */
    RadarMinSpeed(Integer.class, 0),
    /**
     * The file extensions of files found in {@link #APP_DIR_FAILED} for which uploading is retried.
     * All file types not listed here will be deleted instead. Comma-separated list of type String.
     */
    RetryUploadForTypes(String[].class, new String[]{"log", "jpg", "json"}),
    /**
     * The number of values to be tracked by the model.
     */
    SensorModelCapacity(Integer.class, 0),
    /**
     * The mininum difference between a measurement and the respective mean value for a measurement
     * to be considered an event.
     */
    SensorModelMinThreshold(Integer.class, 0),
    /**
     * The standard deviation factor for a measurement to be treated as an event.
     */
    SensorModelSigmaFactor(Double.class, 1.),
    /**
     * The software environment this device runs in. One of {DEV, PROD}.
     */
    SoftwareEnv(String.class, "PROD"),
    /**
     * The interval at which {@link StorageService} is triggered in minutes.
     */
    StorageCheckInterval(Integer.class, 180),
    /**
     * The minimum free storage in MiB below which some archived files will be deleted.
     */
    StorageMinimum(Integer.class, 5120),
    /**
     * The USB baud rate.
     */
    USBBaudRate(Integer.class, 19200),
    /**
     * A base64 encoded list of newline-separated commands to be sent to the USB device.
     */
    USBCommand(String.class, ""),
    /**
     * The USB data bits.
     */
    USBDataBits(Integer.class, 8),
    /**
     * The USB parity. One of {none, odd, even, mark, space}.
     */
    USBParity(String.class, "none"),
    /**
     * The USB stop bits.
     */
    USBStopBits(Integer.class, 1),
    /**
     * This is a placeholder for an unknown key with no current use.
     */
    UnknownKey(Object.class, new Object());

    @NonNull
    public final Class valueType;
    @NonNull
    private final Object defaultValue;

    <T> ConfigKeys(@NonNull Class<T> c, @NonNull T d) {
      valueType = c;
      defaultValue = d;
    }

    /**
     * Like {@link #valueOf}, but instead of throwing an exception if the given name does not match
     * one of the constants, it returns {@link #UnknownKey}.
     *
     * @param name The name of the enum constant.
     * @return The matching enum constant or {@link #UnknownKey}.
     */
    public static ConfigKeys from(String name) {
      try {
        return valueOf(name);
      } catch (IllegalArgumentException ex) {
        Log.d(TAG, "Unknown config key: ", name);
      }
      return UnknownKey;
    }

    /**
     * @return The name to use for intent extras that override this setting.
     */
    public String extraName() {
      return EXTRA_PREFIX + "." + name();
    }
  } // ConfigKeys

  /**
   * Keys supported by JSON documents in the array stored under {@link ConfigKeys#CamSchedule}.
   */
  public enum CamScheduleKeys {
    /**
     * Toggle additional cleaning of the foreground mask produced by bgsub before further analysis.
     * Type boolean. Default: true.
     */
    BGSubCleanFGMask,
    /**
     * Toggle inverting of images before they are applied to the model. Type boolean.
     * Default: false.
     */
    BGSubInvert,
    /**
     * The kernel. Type JSON String array representing BGSubKernelHeight x BGSubKernelWidth values.
     * An array element can provide a single value. It can also provide n equal values with format
     * "n: 0.1". A value can be either a float constant or a simple math expression (currently only
     * supports a single division using format "1.0 / 49").
     */
    BGSubKernel,
    /**
     * The kernel height. Type int.
     */
    BGSubKernelHeight,
    /**
     * The kernel width. Type int.
     */
    BGSubKernelWidth,
    /**
     * The threshold to apply to the output of filtering, range [0,1]. Type double.
     */
    BGSubThreshold,
    /**
     * {@link ConfigKeys#CamExposureMode}.
     */
    CamExposureMode,
    /**
     * {@link ConfigKeys#CamExposureTime}.
     */
    CamExposureTime,
    /**
     * {@link ConfigKeys#CamISO}.
     */
    CamISO,
    /**
     * Whether the configured values can be interpolated. Type boolean.
     */
    Interpolate,
    /**
     * The interval, in milliseconds, at which sequence photos are taken. Defaults to 1000.
     * Type long.
     */
    SequenceInterval,
    /**
     * The number of sequence images to be taken for an event-triggered photo. Defaults to 0, i.e.,
     * no sequence images. Type int.
     */
    SequenceLength,
    /**
     * The maximum size for the longer side of the dimensions for sequence photos. Defaults to 640.
     * Type int.
     */
    SequenceReso,
    /**
     * The time when the config first becomes active or reaches its peak effect if interpolated.
     * Type String. Format: hh:mm.
     */
    Time,
  } // CamScheduleKeys

  /**
   * Keys supported by the JSON documents in the array stored under
   * {@link ConfigKeys#BleActivations}.
   */
  public enum BleActivationsKeys {
    /**
     * An optional list of additional, delayed events to be generated when the rule is satisfied.
     * Each entry specifies an offset, in milliseconds since the rule was evaluated, after which a
     * follow-on event is produced. The initial event (t=0) should not be included here. Type long.
     */
    DelayedEvents,
    /**
     * A list of device addresses. Each device MAC address can optionally have a hyphen followed by
     * one or more suffixes for the type of sensors the rule applies to if the device can report
     * different types. Currently supported suffixes: A for accelerometers ; P for PIR. No suffix
     * implies any sensor provided by the device. Type JSON array of strings.
     */
    Devices,
    /**
     * Time from which the rule is enabled. Defaults to 00:00. Type String. Format: hh:mm.
     */
    EnabledFrom,
    /**
     * Time after which the rule is disabled (inclusive). Defaults to 23:59. Type String.
     * Format: hh:mm.
     */
    EnabledTo,
    /**
     * The minimum number of activations to satisfy this rule. Type int.
     */
    MinActivations,
    /**
     * The duration in milliseconds during which {@link #MinActivations} valid activations have to
     * occur. Type long.
     */
    MinActivationsDuration,
  } // BleActivationsKeys
```