# VoiceWaveView

[![License](https://img.shields.io/badge/license-Apache%202-green.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Download](https://api.bintray.com/packages/echohaha/maven/VoiceWaveView/images/download.svg) ](https://bintray.com/echohaha/maven/VoiceWaveView/_latestVersion)

**VoiceWaveView** - An Android library that provides a voice wave effect.

## Sample

<img src="http://i4.buimg.com/594670/436f0998cfeecbb6.gif" alt="sample" title="sample" width="300" height="450" />
<img src="http://i4.buimg.com/594670/fa9c4f90b46a4810.gif" alt="sample" title="sample" width="300" height="450" />

## Usage

**For a working implementation of this project see the `sample/` folder.**

### Dependency

Include the library as local library project or add the dependency in your build.gradle.

```groovy
dependencies {
    compile 'me.kankei.voicewaveview:library:0.0.4'
}
```

### Layout

Include the VoiceWaveView widget in your layout. And you can customize it like this. this view doesn't support `wrap_content`, Its size must be determined or `match_parent`.  

```xml
<me.kaneki.voicewaveview.VoiceWaveView
        android:id="@+id/voiceWaveView"
        android:layout_width="300dp"
        android:layout_height="40dp"
        android:layout_centerHorizontal="true"
        android:background="@drawable/msg_voice_panel_bg"
        app:lineWidth="1.5dp"
        app:dividerWidth="1dp"
        app:duration="30"
        app:refreshRatio="50"
        app:backgroundColor="#7f7f7f"
        app:activeLineColor="#ffffff"
        app:inactiveLineColor="#99ffffff"/>         
```

### Java

If you want to record or play the recorded data, you can write these code, etc in your Activity.

```java
    VoiceWaveView mVoiceWaveView = (VoiceWaveView) findViewById(R.id.voiceWaveView);

    //begin record
    mVoiceWaveView.startRecord();
    //set the record wave height percent (1-100), it can be used during other thread
    mVoiceWaveView.setWaveHeightPercent(random.nextInt(100) + 1);
    //stop record
    mVoiceWaveView.stopRecord();
    //get the last record data, you can change the waveData to json string or other type to save it
    WaveData waveData = mVoiceWaveView.getLastWaveData();
    //draw the give wave data as view
    mVoiceWaveView.drawWaveData(waveData);

    //start play, if the waveData is null, it will play the last record data
    mVoiceWaveView.starPlay(waveData);
    //pause the play or resume it
    mVoiceWaveView.pauseOrResumePlay();

```
`WaveData` contains last record wave list and  duration, you can serialize it for local storage.

```java
public class WaveData {
        private ArrayList<WaveBean> waveList;
        private long duration;

        public WaveData(ArrayList<WaveBean> waveList, long duration) {
            this.waveList = waveList;
            this.duration = duration;
        }

        public ArrayList<WaveBean> getWaveList() {
            return waveList;
        }

        public void setWaveList(ArrayList<WaveBean> waveList) {
            this.waveList = waveList;
        }

        public long getDuration() {
            return duration;
        }

        public void setDuration(long duration) {
            this.duration = duration;
        }
    }

```

## Customization

|name|format|description|
|:---:|:---:|:---:|
| backgroundColor | color |background color, default is `#7f7f7`
| activeLineColor | color | active line color, default is `#ffffff`
| inactiveLineColor | color | inactive line color, default is `#99ffffff`
| lineWidth | dimension | wave line width, default is `1dp`
| dividerWidth | dimension | divider width between two wave line, default is `1dp`
| duration | integer | max record time , default is `30s`
| refreshRatio | integer | view refresh ratio, default is `50ms`



**All attributes have their respective getters and setters to change them at runtime.**

## Change Log
### 0.0.4（2017-06-03）
- add new public interface `drawWaveData`.
- extract the inner class `WaveData` and `WaveBean` as public entity.
- change the structure of internal code `VoiceWaveView`

### 0.0.3（2017-05-19）
- removing personal configuration does not matter...

### 0.0.2（2017-05-19）
- fix get last wave data not contains duration.
- optimized wave data compression algorithm.

### 0.0.1（2017-05-17）
- library first build.


## Community

Looking for contributors, feel free to fork !

Tell me if you're using my library in your application, I'll share it in this README.

## Contact Me

I work as Android Development Engineer at Meili-inc Group.

If you have any questions or want to make friends with me, please feel free to contact me : [chenjianbo2222#gmail.com](mailto:chenjianbo2222@gmail.com)


## License

    Copyright 2016 Kaneki

	Licensed under the Apache License, Version 2.0 (the "License");
	you may not use this file except in compliance with the License.
	You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

	Unless required by applicable law or agreed to in writing, software
	distributed under the License is distributed on an "AS IS" BASIS,
	WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	See the License for the specific language governing permissions and
	limitations under the License.
