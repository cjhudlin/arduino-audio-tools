This functionality provides the glue which makes different audio processing components work together.

### Example

Here is a simple example which streams a file from the Flash Memory and writes it to I2S: 

```C++
#include "AudioTools.h"
#include "StarWars30.h"

uint8_t channels = 2;
uint16_t sample_rate = 22050;
uint8_t bits_per_sample = 16;

MemoryStream music(StarWars30_raw, StarWars30_raw_len);
I2SStream i2s;  // Output to I2S
StreamCopy copier(i2s, music); // copies sound into i2s

void setup(){
    Serial.begin(115200);

    auto config = i2s.defaultConfig(TX_MODE);
    config.sample_rate = sample_rate;
    config.channels = channels;
    config.bits_per_sample = bits_per_sample;
    i2s.begin(config);

    music.begin();
}

void loop(){
    copier.copy();
}

```
Each stream has it's own [configuration object](https://pschatzmann.github.io/arduino-audio-tools/structaudio__tools_1_1_audio_info.html) that should be passed to the begin method. The defaultConfig() method is providing a default proposal which will usually "just work". Please consult 
the [class documentation](https://pschatzmann.github.io/arduino-audio-tools/modules.html) for the available configuration parameters. You can also __easily adapt__ any provided examples: If you e.g. replace the I2SStream with the AnalogAudioStream class, you will get analog instead of digital output.

I suggest you continue to read the more [detailed introduction](https://github.com/pschatzmann/arduino-audio-tools/wiki/Introduction).

Further examples can be found in the [Wiki](https://github.com/pschatzmann/arduino-audio-tools/wiki/Examples). 

Dependent on the example you might need to install some [additional libaries](https://github.com/pschatzmann/arduino-audio-tools/wiki/Optional-Libraries)

### AudioPlayer

The library also provides a versatile [AudioPlayer](https://pschatzmann.github.io/arduino-audio-tools/classaudio__tools_1_1_audio_player.html). Further information can be found in the [Wiki](https://github.com/pschatzmann/arduino-audio-tools/wiki/The-Audio-Player-Class)


### Logging

The application uses a built in logger: By default we use the log level warning and the logging output is going to Serial. You can change this in your sketch by calling e.g:

```C++
AudioToolsLogger.begin(Serial, AudioToolsLogLevel::Debug);
```
You can log to any object that is a subclass of Print and valid log level values are: Debug, Info, Warning, Error.


You can also deactivate the logging by changing USE_AUDIO_LOGGING to false in the AudioConfig.h to decrease the memory usage: 

```C++
#define USE_AUDIO_LOGGING false
```
