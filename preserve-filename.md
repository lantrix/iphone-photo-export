# Exiftool: Preserve original filename in Exif Metadata

Add an [XMP](https://exiftool.org/TagNames/XMP.html) PreservedFileName Tag to the file to preserve original filename.

```shell
exiftool -preserve -overwrite_original_in_place '-XMP-xmpMM:PreservedFileName<${filename;s/\.[^.]*$//}' "${file_name}"
```

Same as above but for all files in the current folder

```shell
exiftool -preserve -overwrite_original_in_place '-XMP-xmpMM:PreservedFileName<${filename;s/\.[^.]*$//}' .
```

Same as above but for all file in the current folder and all subfolders

```shell
exiftool -preserve -overwrite_original_in_place '-XMP-xmpMM:PreservedFileName<${filename;s/\.[^.]*$//}' -r .
```