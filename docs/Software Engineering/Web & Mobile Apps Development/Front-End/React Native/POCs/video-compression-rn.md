## video compression in react native

react-native-compressor : zubair had worked on it in hefazat mobile app using react native

```jsx showLineNumbers
    "react-native-compressor": "^1.6.1",
```

```jsx showLineNumbers
const captureVideo = async (setVideo: any) => {
    let options: CameraOptions = {
      mediaType: 'video',
      cameraType: 'back',
      videoQuality: 'low',
      includeBase64: true,
      durationLimit: 60,

      //presentationStyle: 'popover'
    };
    setVideo('');
    launchCamera(options, async (response: ImagePickerResponse) => {
      if (response.didCancel) {
        console.log('User cancelled image picker');
      } else if (response.errorCode) {
        console.log('ImagePicker Error: ', response.errorCode);
        if (response.errorMessage) {
          console.log('ImagePicker Error Message: ', response.errorMessage);
        }
      } else {
        if (response.assets != null && response.assets.length > 0) {
          const asset = response.assets[0];
          //console.log(`file type is ${asset.type}`);
          //console.log(`file name is ${asset.fileName}`);
          if (asset.base64) {
            //console.log('video base64');
            setVideo(asset.base64);
          } else if (asset.uri) {
            try {
              const {path, metaData, realPath} = await videoCompressor(asset.uri);
              console.log('BEFORE:', asset, 'AFTER', {realPath,path, metaData});
              RNFS.readFile(path, 'base64')
                .then((data: string) => {
                  setVideo(data);
                })
                .catch((reason: any) => {
                  console.log(`error: ${JSON.stringify(reason)}`);
                });
            } catch (er) {
              console.warn(er, 'Check error');
            }
          }
        }
      }
    });
  };

const videoCompressor = async (
    path = 'file://path_of_file/BigBuckBunny.mp4',
  ) => {
    const result = await Video.compress(path, {
      compressionMethod: 'auto',
    });

    const metaData = await getVideoMetaData(result);
    const realPath = await getRealPath(result, 'video');
   // console.log(result, metaData, realPath, 'after compress see result');
    return {metaData, path: result, realPath};
  };


usage
return(
...
     <Icon
                  name="plus-square"
                  size={40}
                  color="#aaaaaa"
                  onPress={() => captureVideo(setMobileVideo)}
                />
    ...
)

```
