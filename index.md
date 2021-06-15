## fijkplayer -- Flutter plugin for ijkplayer

fijkplayer is a media player plugin for flutter ecosystem which wraps the native ijkplayer into flutter and supports both Android and iOS. fijkplayer uses ijkplayer as the player kernel. The ijkplayer uses ffmpeg for audio and video demuxing and decoding, while adding hardware-accelerated decoding capabilities specific to Android and iOS platforms.

fijkplayer has the same playback capabilities as ijkplayer and is very convenient to use. fijkplayer’s API is easy to use, and it’s easy to add fijkplayer to your flutter app. There is no need bu build ffmpeg and native ijkplayer yourself.

fijkplayer brings the video from native to Flutter through Texture, which has better performance than PlatformView. fijkplayer has build-in ijkplayer, which hosted separately on jcenter and CocoaPods.

This site contains a lot of fijkplayer documentation to help you use and understand fijkplayer.

### Create FijkPlayer

open main.dart, edit and update class _MyHomePageState as bellow.

```markdown
class _MyHomePageState extends State<MyHomePage> {
  final FijkPlayer player = FijkPlayer();

  @override
  void initState() {
    super.initState();
    player.setDataSource(
        "https://sample-videos.com/video123/flv/240/big_buck_bunny_240p_10mb.flv",
        autoPlay: true);
  }

  @override
  void dispose() {
    super.dispose();
    player.release();
  }


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.
        child: FijkView(player: player),
      ),
    );
  }
}
```

important changes:

Initialize a FijkPlayer instance player in class _MyHomePageState.
Call the player.setDataSource API in the initState method.
Call the player.release API in the dispose method to release the resources occupied by the player.
Add FijkView to the UI Widgets Tree in the build method.

### Brief description

A FijkPlayer instance is bound to a playback (native ijkplayer). After the Fijkplayer is constructed, the corresponding native ijkplayer is also initialized. FijkPlayer has almost all the APIs of ijkplayer. FijkPlayer is a dart wrapper for the native C layer ijkplayer, and the APIs are consistent.
FijkPlayer handles all playback-related work. The actual work is done by the native C-layer ijkplayer, which includes checking the media information in the dataSource, opening the decoder and decoding threads, turning on the audio output device, and outputting the decoded data to the audio device or display device. FijkPlayer occupies a lot memory or resources, and should call the API release explicitly for release when not in use.

FijkView only does one thing: display the decoded video content of FijkPlayer.
FijkView has almost no extra API. If new API is added later, it is also related to the UI display.

### Screenshots

![Screenshots](https://github.com/dabaitu2018/fijkplayer/blob/gh-pages/Screenshots.jpeg?raw=true)
