# bpg testing
---

Repository created for testing bpg image format.
For a better explanation on the libs used, refer to the their pages.

## Folder structure
```
README.md -- this file
index.html -- HTML file with bpg, video and gifs embedded
assets -- Folder with all the assets
|-bpg
|-css
|-frames
|-gif
|-img
|-js
|-videos
```
Folder "frames" only used to generate bpg files and folder "gif" only used to check the gif size

## Workflow
1. Extracted the frames as `.png` from videos with [ffmpeg](https://www.ffmpeg.org/), using the following command:
```
$ ffmpeg -i assets/videos/[name-of-video].mp4 assets/frames/[name-of-video]/frame-%05d.png
```

2. Created the `.gif` version with [gifenc.sh](gifenc.sh) (got the script [here](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html), I removed the scale and updated the FPS for comparison purpose)
```
$ ./gifenc.sh assets/videos/[name-of-video].mp4 assets/gifs/[name-of-video].gif
```

3. Created the `.bpg` version of the videos with [bpgenc](http://bellard.org/bpg/), using the following command (*This took sometime to complete*):
```
bpgenc -a assets/frames/[name-of-video]/frame-%05d.png -fps 30 -loop 0 -o assets/bpg/[name-of-video].bpg
```
Also created the `.bpg` from the `.jpg`:
```
bpgenc assets/img/photo.jpg -o assets/bpg/[name-of-video].bpg
```

## Examples
[index.html](index.html) contains example of two animated bpg and one static bpg, with the size of each file.  
Used the `bpgdec8a.js`: bpg decoder with support for animation