## TRTCCloud

### Basic APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/sharedInstance.html) | Creates a TRTCCloud singleton. |
| [destroySharedInstance](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/destroySharedInstance.html) | Destroys a TRTCCloud singleton. |
| [registerListener](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/registerListener.html) | Registers an event listener. |
| [unRegisterListener](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/unRegisterListener.html) | Unregisters an event listener. |

### Room APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/enterRoom.html) | Enters a room. If the room does not exist, the system will create one automatically.           |
| [exitRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/exitRoom.html) | Exits a room.                                                   |
| [switchRole](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/switchRole.html) | Switches roles. This API works only in live streaming scenarios (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [setDefaultStreamRecvMode](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setDefaultStreamRecvMode.html) | Sets the audio/video data receiving mode, which must be set before room entry to take effect.           |
| [connectOtherRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/connectOtherRoom.html) | Requests a cross-room call (anchor competition).                                    |
| [disconnectOtherRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/disconnectOtherRoom.html) | Exits a cross-room call.                                               |
| [switchRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/switchRoom.html) | Switches rooms.                                                   |



### CDN APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startPublishing.html) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopPublishing.html) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startPublishCDNStream.html) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopPublishCDNStream.html) | Stops relaying to the live streaming CDN of a non-Tencent Cloud vendor.      |
| [setMixTranscodingConfig](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html) | Sets On-Cloud MixTranscoding parameters.      |


### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalPreview](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startLocalPreview.html) | Enables preview of the local video.                                     |
| [stopLocalPreview](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopLocalPreview.html) | Stops local video capturing and preview.                                     |
| [muteLocalVideo](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteLocalVideo.html) | Pauses/Resumes pushing local video data.                                |
| [startRemoteView](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startRemoteView.html) | Starts displaying the image of a remote user.                                       |
| [stopRemoteView](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopRemoteView.html) | Stops displaying the video image of a remote user and pulling the user’s video stream.   |
| [stopAllRemoteView](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopAllRemoteView.html) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteRemoteVideoStream.html) | Pauses/Resumes receiving a specified remote video stream.                              |
| [muteAllRemoteVideoStreams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteAllRemoteVideoStreams.html) | Pauses/Resumes receiving all remote video streams.                                |
| [setVideoEncoderParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setVideoEncoderParam.html) | Sets video encoder parameters.                                     |
| [setNetworkQosParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setNetworkQosParam.html) | Sets QoS control parameters.                                       |
| [setLocalRenderParams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setLocalRenderParams.html) | Sets the rendering mode of the local image. |
| [setRemoteRenderParams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setRemoteRenderParams.html) | Sets remote image parameters. |
| [setVideoEncoderRotation](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setVideoEncoderRotation.html) | Sets the rotation of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setVideoEncoderMirror.html) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setGSensorMode.html) | Sets the adaptation mode of the G-sensor. |
| [enableEncSmallVideoStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/enableEncSmallVideoStream.html) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setRemoteVideoStreamType.html) | Switches between the small and big images of a specified user.                          |
| [snapshotVideo](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/snapshotVideo.html) | Takes a video screenshot. |


### Audio APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startLocalAudio.html) | Enables local audio capturing and upstream data transfer.           |
| [stopLocalAudio](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopLocalAudio.html) | Disables local audio capturing and upstream data transfer.           |
| [muteLocalAudio](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteLocalAudio.html) | Mutes/Unmutes the local audio.            |
| [setVideoMuteImage](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setVideoMuteImage.html) | Sets the image to be pushed when local video pushing is paused. |
| [setAudioRoute](https://comm.qq.com/trtc-flutter-en/api/tx_device_manager/TXDeviceManager/setAudioRoute.html) | Sets the audio route.                       |
| [muteRemoteAudio](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteRemoteAudio.html) | Mutes/Unmutes the audio of a specified remote user.  |
| [muteAllRemoteAudio](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/muteAllRemoteAudio.html) | Mutes/Unmutes all users.        |
| [setAudioCaptureVolume](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setAudioCaptureVolume.html) | Sets the SDK capturing volume.                  |
| [getAudioCaptureVolume](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getAudioCaptureVolume.html) | Gets the SDK capturing volume.                  |
| [setAudioPlayoutVolume](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setAudioPlayoutVolume.html) | Sets the SDK playback volume.                  |
| [getAudioPlayoutVolume](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getAudioPlayoutVolume.html) | Gets the SDK playback volume.                  |
| [enableAudioVolumeEvaluation](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/enableAudioVolumeEvaluation.html) | Enables volume reminders.                   |
| [startAudioRecording](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startAudioRecording.html) | Starts audio recording.                           |
| [stopAudioRecording](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopAudioRecording.html) | Stops audio recording.                           |
| [setSystemVolumeType](https://comm.qq.com/trtc-flutter-en/api/tx_device_manager/TXDeviceManager/setSystemVolumeType.html) | Sets the system volume type used during calls.       |


### Device management APIs

| API | Description |
|-----|-----|
| [getDeviceManager](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getDeviceManager.html) | Gets the device management module. For details, see [device management APIs](https://comm.qq.com/trtc-flutter-en/api/tx_device_manager/TXDeviceManager-class.html). |


### Beauty filter APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getBeautyManager.html) | Gets the beauty filter management object. For details, see the [document on beauty filter management](https://comm.qq.com/trtc-flutter-en/api/tx_beauty_manager/TXBeautyManager-class.html). |
| [setWatermark](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setWatermark.html) | Adds watermarks.                                                   |


### Music and voice effect APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getAudioEffectManager.html) | Gets the audio effect management class `TXAudioEffectManager`, which is used to manage background music, short audio effects, and voice effects. For details, see the [document on audio effect management](https://comm.qq.com/trtc-flutter-en/api/tx_audio_effect_manager/TXAudioEffectManager-class.html). |

### Substream APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | -------------- |
| [startScreenCapture](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startScreenCapture.html) | Starts screen sharing. |
| [stopScreenCapture](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopScreenCapture.html) | Stops screen sharing. |
| [pauseScreenCapture](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/pauseScreenCapture.html) | Pauses screen sharing. |
| [resumeScreenCapture](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/resumeScreenCapture.html) | Resumes screen sharing. |

### Custom message sending APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sendCustomCmdMsg](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/sendCustomCmdMsg.html) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/sendSEIMsg.html) | Embeds small-volume custom data in video frames. |


### Network testing APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/startSpeedTest.html) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/stopSpeedTest.html) |  Stops server speed testing.                                             |


### Log APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/getSDKVersion.html) | Gets the SDK version.         |
| [setLogLevel](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setLogLevel.html) | Sets the log output level.         |
| [setLogDirPath](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setLogDirPath.html) | Changes the path to save logs.          |
| [setLogCompressEnabled](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setLogCompressEnabled.html) | Enables/Disables local log compression. |
| [setConsoleEnabled](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud/setConsoleEnabled.html) | Enables/Disables console log printing.  |


## TRTCCloudListener

Callback APIs for the TRTC video call feature

### Error and warning event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onError) | Error callback. This indicates that the SDK encountered an irrecoverable error. Such errors must be listened for, and UI messages should be displayed to users if necessary. |
| [onWarning](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onWarning) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onEnterRoom) | Callback of room entry                  |
| [onExitRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onExitRoom) | Callback of room exit                |
| [onSwitchRole](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSwitchRole) | Callback of role switching                |
| [onConnectOtherRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectOtherRoom) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisConnectOtherRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onDisConnectOtherRoom) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSwitchRoom) | Callback of the result of room switching (`switchRoom`)  |

### User event callback APIs

| API                                                          | Description                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onRemoteUserEnterRoom) | Callback of the entry of a user                                   |
| [onRemoteUserLeaveRoom](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onRemoteUserLeaveRoom) | Callback of the exit of a user                                   |
| [onUserVideoAvailable](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onUserVideoAvailable) | Callback of whether a remote user has a playable primary image (usually the image of the camera) |
| [onUserSubStreamAvailable](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onUserSubStreamAvailable) | Callback of whether a remote user has a playable substream image (usually the screen sharing image) |
| [onUserAudioAvailable](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onUserAudioAvailable) | Callback of whether a remote user has playable audio                    |
| [onFirstVideoFrame](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onFirstVideoFrame) | Callback of rendering the first video frame of the local user or a remote user                      |
| [onFirstAudioFrame](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onFirstAudioFrame) | Callback of playing the first audio frame of a remote user. No notifications are sent for local audio.       |
| [onSendFirstLocalVideoFrame](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSendFirstLocalVideoFrame) | Callback of sending the first local video frame                           |
| [onSendFirstLocalAudioFrame](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSendFirstLocalAudioFrame) | Callback of sending the first local audio frame                           |

### Callback APIs for background music playback

Callback APIs for background music playback

| API                                                          | Description                     |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverStart) | Callback of starting music playback |
| [onMusicObserverPlayProgress](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverPlayProgress) | Callback of the music playback progress |
| [onMusicObserverComplete](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverComplete) | Callback of ending music playback |

### Callback APIs for statistics on network quality and technical metrics

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onNetworkQuality) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the quality of current upstream and downstream data transfer. |
| [onStatistics](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onStatistics) | Callback of statistics on technical metrics                                           |


### Server event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectionLost) | Callback of the disconnection of the SDK from the server                                     |
| [onTryToReconnect](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onTryToReconnect) | Callback of the SDK trying to connect to the server again                                   |
| [onConnectionRecovery](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectionRecovery) | Callback of the reconnection of the SDK to the server                                     |
| [onSpeedTest](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSpeedTest) | Callback of server speed test results. The SDK tests the speed of multiple server addresses, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onCameraDidReady) | Callback of the camera being ready                                             |
| [onMicDidReady](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onMicDidReady) | Callback of the mic being ready                                             |
| [onUserVoiceVolume](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onUserVoiceVolume) | Callback of volume, including the volume of each `userId` and the total remote volume |


### Custom message receiving callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onRecvCustomCmdMsg](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onRecvCustomCmdMsg) | Callback of receiving a custom message |
| [onMissCustomCmdMsg](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onMissCustomCmdMsg) | Callback of losing a custom message |
| [onRecvSEIMsg](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onRecvSEIMsg) | Callback of receiving an SEI message |


### Callback APIs for CDN relayed push

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onStartPublishing) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud-class.html#startPublishing) |
| [onStopPublishing](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onStopPublishing) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud-class.html#stopPublishing) |
| [onStartPublishCDNStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onStartPublishCDNStream) | Callback of the completion of starting relayed push to CDNs |
| [onStopPublishCDNStream](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onStopPublishCDNStream) | Callback of the completion of stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSetMixTranscodingConfig) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud/TRTCCloud-class.html#setMixTranscodingConfig) |


### Screen sharing callback APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ---------------- |
| [onScreenCaptureStarted](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onScreenCaptureStarted) | Callback of starting screen sharing |
| [onScreenCapturePaused](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onScreenCapturePaused) | Callback of pausing screen sharing via the calling of `pauseScreenCapture()` |
| [onScreenCaptureResumed](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onScreenCaptureResumed) | Callback of resuming screen sharing via the calling of `resumeScreenCapture()` |
| [onScreenCaptureStopped](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onScreenCaptureStopped) | Callback of stopping screen sharing |

### Screenshot callback API

| API                                                          | Description                  |
| ------------------------------------------------------------ | ---------------- |
| [onSnapshotComplete](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_listener/TRTCCloudListener-class.html#onSnapshotComplete) | Callback of the completion of a screenshot |


## Definitions of Key Classes

| Class                                                         | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCCloudDef-class.html) | Variables for key class definitions                                   |
| [TRTCParams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCParams-class.html) | Room entry parameters                                          |
| [TRTCSwitchRoomConfig](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCSwitchRoomConfig-class.html) | Room switching parameters   |
| [TRTCVideoEncParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCVideoEncParam-class.html) | Video encoding parameters                                      |
| [TRTCNetworkQosParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCNetworkQosParam-class.html) | QoS control parameters                                  |
| [TRTCRenderParams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCRenderParams-class.html) | Remote image parameters |
| [TRTCMixUser](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCMixUser-class.html) | Position of the image of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCTranscodingConfig-class.html) | On-Cloud MixTranscoding configuration |
| [TXVoiceChangerType](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TXVoiceChangerType-class.html) | Definitions of voice changing types (little girl, middle-aged man, metal, foreign accent, etc.) |
| [TXVoiceReverbType](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TXVoiceReverbType-class.html) | Definitions of reverb effect types (karaoke, room, hall, low and deep, resonant, etc.) |
| [AudioMusicParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/AudioMusicParam-class.html) | Parameters for music and voice effect setting APIs |
| [TRTCAudioRecordingParams](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCAudioRecordingParams-class.html) | Audio recording parameters |
| [TRTCPublishCDNParam](https://comm.qq.com/trtc-flutter-en/api/trtc_cloud_def/TRTCPublishCDNParam-class.html) | CDN relayed push parameters |
