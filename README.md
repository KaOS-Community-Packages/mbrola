# mbrola
This package installs the mbrola synthesizer and the british english voice en1 (see [MBROLA-voices](https://github.com/numediart/MBROLA-voices)). To install
```
kcp -u
kcp -i mobrola
```
You can test the installation by using an example *.pho* file like [this](https://raw.githubusercontent.com/numediart/MBROLA-voices/master/data/en1/TEST/euler.pho). Then, you can here it by running
```
mbrola /usr/share/mbrola/en1/en1 euler.pho -.au | paplay
```
If you have espeak installed, you can also test the installation runnning
```
espeak -v mb-en1 "Hello world"
```

[Mbrola](https://github.com/numediart/MBROLA) is a speech synthesizer based on the concatenation of diphones. It takes a list of phonemes as input, together with prosodic information (duration of phonemes and a piecewise linear description of pitch), and produces speech samples on 16 bits (linear), at the sampling frequency of the diphone database.

Please look at [MBROLA-voices](https://github.com/numediart/MBROLA-voices) project homepage to get the voices. You may also develop your own voices using the [MBROLATOR](https://github.com/numediart/MBROLATOR).

## Adding new voices
To add a voice to MBROLA, for example us1, download the corresponding file from the [MBROLA-voices github page](https://github.com/numediart/MBROLA-voices). Then, create a new folder under **/usr/share/mbrola/** named us1, using a terminal you can do it by running
```
sudo mkdir /usr/share/mbrola/us1
```
Now place the downloaded file in that folder, running for example
```
sudo cp path-of-downloaded-file /usr/share/mbrola/us1
```

You can test the newly installed voice using espeak
```
espeak -v mb-us1 "Hello world"
```

## Using MBROLA voices with Okular
To do so, you need to install espeak
```
sudo pacman -Su espeak
```
and set the appropriate files of speech-dispatcher.

1. *Open the file* '.config/speech-dispatcher/modules/espeak-ng-mbrola-generic.conf'
```
kate .config/speech-dispatcher/modules/espeak-ng-mbrola-generic.conf
```
and uncomment (*i.e.* remove the hash) the rows
```
GenericExecuteSynth \
"printf %s \'$DATA\' | espeak-ng -v mb-$VOICE -s $RATE -p $PITCH $PUNCT -stdin"
```
then save.

2. *Open the file* `.config/speech-dispatcher/speechd.conf`
```
kate .config/speech-dispatcher/speechd.conf
```
and uncomment the line
```
AddModule "espeak-ng-mbrola-generic" "sd_generic"   "espeak-ng-mbrola-generic.conf"
```
and modify the line
```
DefaultModule   espeak
```
to
```
DefaultModule   espeak-ng-mbrola-generic
```

3. *Restart Okular.* Now the TTS function of Ocular uses the MBROLA voices. Please note that whenever a voice is missing, the output is mute. Install the appropriate languages; to check the output you can compare the default
```
spd-say -l en "Hello"
```
with the explicit call to MBROLA
```
espeak-ng -vmb-en1 "Hello"
```
Omitting the option `-l en` will select your system default language; be shure to have the corresponding MBROLA voice.
