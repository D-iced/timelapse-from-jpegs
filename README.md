#Making timelapse movies from images

guided by https://dlo.me/archives/2015/07/26/making-a-time-lapse-using-ffmpeg-and-imagemagick/

	1. resize
	2. match histograms
	3. make movie

## resize
Probably using Irfanview. Because I'm no wizard with Windows CLI.
In the batch conversion window, Set work as: Batch conversion rename results.
use advanced options (for bulk resize)
change the length to one of youtubes preferred widths.
Later they can be cropped from top or bottom,
but maybe you want to choose these values depending on the resulting movie.
ffmpeg can do that for you too.
Otherwise, use irfanview for a second run, and crop counting pixels,
since the canvas is resized to the correct width already.

Now, I've saved the settings to an inifile dedicated to resize for youtube.
Probably in two steps.

## match histograms.
Maybe Irfanview can do this?

##ffmpeg

```
ffmpeg -start_number 4120 -i "IMG_%04d.JPG" out.mpg
```

The filname must be contained in `"`'s in order to work properly.
