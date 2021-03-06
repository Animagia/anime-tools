AV1 codec
=========

Aomenc
------

### Installation

#### Windows
<https://nwgat.ninja/compile-av1-using-msys2-mingw/>

#### Linux
<https://nwgat.ninja/compiling-aomedia-av1-on-ubuntu/>

<https://aomedia.googlesource.com/aom/#building-the-library-and-applications>

### Video encoding
#### Using intermediate files
##### Windows
```
ffmpeg -i [input] -pix_fmt yuv420p [file].y4m

.\aomenc.exe -p 2 --pass=1 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=1500 --fpf=[output].log -o [output].mkv [file].y4m

.\aomenc.exe -p 2 --pass=2 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=1500 --fpf=[output].log -o [output].mkv [file].y4m
```

##### Linux
```
ffmpeg -i [input] -pix_fmt yuv420p [file].y4m

./aomenc -p 2 --pass=1 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=1500 --fpf=[output].log -o [output].mkv [file].y4m

./aomenc -p 2 --pass=2 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=1500 --fpf=[output].log -o [output].mkv [file].y4m
```

#### Using pipes
##### Linux
```
ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | ./aomenc -p 2 --pass=1 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=800 --fpf=[output].log -o [output].mkv -

ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | ./aomenc -p 2 --pass=2 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=800 --fpf=[output].log -o [output].mkv -
```

##### Windows:
**cmd only, PowerShell loses frames in input data**

```
ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | .\aomenc.exe -p 2 --pass=1 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=800 --fpf=[output].log -o [output].mkv -

ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | .\aomenc.exe -p 2 --pass=2 -t 3 --cpu-used=4 --tile-columns=6 --frame-parallel=1 -w 1280 -h 720 --auto-alt-ref=1 --lag-in-frames=25 --profile=0 --end-usage=q --target-bitrate=800 --fpf=[output].log -o [output].mkv -
```

## Rav1e

### Installation
<https://github.com/xiph/rav1e>

### Video encoding
#### Using intermediate files
##### Windows
```
ffmpeg -i [input] -pix_fmt yuv420p [file1].y4m

.\rav1e.exe [file1].y4m -o [file2].ivf --quantizer 85 --speed 3

ffmpeg -i [file2].ivf -c:v copy [output].mkv
```

##### Linux
```
ffmpeg -i [input] -pix_fmt yuv420p [file1].y4m

./rav1e [file1].y4m -o [file2].ivf --quantizer 85 --speed 3

ffmpeg -i [file2].ivf -c:v copy [output].mkv
```

#### Using pipes
##### Linux
```
ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | ./rav1e - -o [output].ivf --quantizer 85 --speed 3

ffmpeg -i [output].ivf -c:v copy [output].mkv
```

##### Windows
**cmd only, PowerShell has memory leakage problem**

```
ffmpeg -i [input] -pix_fmt yuv420p -f yuv4mpegpipe - | .\rav1e.exe - -o [output].ivf --quantizer 85 --speed 3

ffmpeg -i [output].ivf -c:v copy [output].mkv
```

## Video players which supports AV1
### VLC
<https://www.videolan.org/vlc/> - stable release, works on Linux only

<https://nightlies.videolan.org/> - unstable builds 

### MPC-HC (unofficial)
<https://github.com/clsid2/mpc-hc/releases>

### MPV
<https://mpv.io/>

### MPC-BE
<https://sourceforge.net/projects/mpcbe/files/MPC-BE/Release%20builds/>
