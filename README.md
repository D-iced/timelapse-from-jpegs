#Making timelapse movies from images

guided by https://dlo.me/archives/2015/07/26/making-a-time-lapse-using-ffmpeg-and-imagemagick/

	1. resize
	2. match histograms
	3. make movie

## resize
Probably using [Irfanview](http://irfanview.com "Irfanview").
Probably in two steps.
Because I'm no wizard with Windows CLI.

In the batch conversion window:
- Set work as: Batch conversion rename results.
- use advanced options (for bulk resize) (click the button)
  in the following window:
	- change the length to one of youtubes preferred widths.
	Later they can be cropped from top or bottom,
	you'll probably want to choose these values depending on the resulting movie.
	[ffmpeg](http://ffmpeg.org "ffmpeg") can do that for you too.
	Otherwise, use irfanview for a second run, and crop counting pixels,
	since the canvas now has the correct width already.

I've saved the settings to an [inifile](resize_for_youtube.ini "The ini-file") dedicated to resize for youtube.

## match histograms.
Maybe Irfanview can do this?

## ffmpeg
Without resizing, the filnames start at what the camera used as a number.
The filname must be contained in `"`'s in order to work properly.
```
ffmpeg -start_number 4120 -i "IMG_%04d.JPG" out.mpg
```

After resizing, the files were renamed and I could drop the `start_number` parameter.
But I still needed to crop the images from the top 240 pixes,
so I could catch the most interesting part in the video.
```
ffmpeg -i "%04d.jpg" -filter:v "crop=1280:720:0:240" out.mpg
```
Still it ended up too large, so I added `crf 25` in the libx264 codec setting
```
ffmpeg -i "%04d.jpg" -filter:v "crop=1280:720:0:240" -c:v libx264 -preset veryslow -crf 25 out.mpg
```
crf|0|15|20|25|
--- |---|---|---|
size [Mb] | 124|25|10|4



