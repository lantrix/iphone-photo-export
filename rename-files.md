# Exiftool: Rename image files according to their Original date

The following is based upon the excellent article by [@ellelstone](https://github.com/ellelstone) entitled [ExifTool Commands for Image Organization](https://ninedegreesbelow.com/photography/exiftool-commands.html#rename)

The following command renames all `.heic` (Apple), `.jpg` (JPEG)`.mov` (Apple) abd `.mp4` (Apple) files from metadata specific to each media type:

### iPhone Images

iPhone correctly uses [EXIF](https://exiftool.org/TagNames/EXIF.html) `DateTimeOriginal`.

```shell
exiftool -overwrite_original -preserve '-filename<DateTimeOriginal' -d %Y-%m-%d_%H%M_%S%%+c.%%le -r -ext heic -ext jpg /Users/lantrix/Pictures/_temp
```

### iPhone Movies

iPhone movie files uses [QuickTime](https://exiftool.org/TagNames/QuickTime.html) Keys Tag `CreationDate`.

```shell
exiftool -overwrite_original -preserve '-filename<CreationDate' -d %Y-%m-%d_%H%M_%S%%+c.%%le -r -ext mov /Users/lantrix/Pictures/_temp
```

### Other Movies

Other movie files exported use [QuickTime](https://exiftool.org/TagNames/QuickTime.html) MovieHeader Tag `CreateDate`.
```shell
exiftool -overwrite_original -preserve '-filename<CreateDate' -d %Y-%m-%d_%H%M_%S%%+c.%%le -r -ext mp4 /Users/lantrix/Pictures/_temp
```

## Details

As noted in the [exiftool man page](https://exiftool.org/exiftool_pod.html):

* `'-filename<DateTimeOriginal'` will rename the image file using `DateTimeOriginal`.
* `-d` is _Set format for date/time values_.
  * `%Y-%m-%d_%H%M_%S%%+c.%%le` is the dateFormat to use for the date and time when renaming the file, being:
    * `%Y-%m-%d_` means four digits for year, two digit for month and day and an underscore after the date.
    * `%H%M_%S` means 24 Hour format hour, minute, and second of the creation time, all represented by two digits with an underscore between HHMM and SS.
    * `%%+c` _represents a copy number which is automatically incremented if the file already exists_ to give each image with the same time a unique name.
      * The %c is escaped with another % as a format code _used within a date format string, an extra '%' must be added to pass these codes through the date/time parser_
      * The `+c _adds an underline_ before the copy number.
    * `.%%le` means keep the original file name extension, but make it lower-case if it was originally upper-case, also a double `%%` as escaping _to pass these codes through the date/time parser_.
* `-ext heic` and `-ext jpg` means only rename files with the `.heic` or `.jpg` extension.
* `-r` will _Recursively process subdirectories_
* `/Users/lantrix/Pictures/_temp` is the absolute path to the top folder holding all the media to be renamed.