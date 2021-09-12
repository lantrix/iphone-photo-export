# Lowercase image file name extensions

```shell
for i in *.HEIC; do mv "$i" "${i%%.HEIC}.heic"; done
for i in *.JPG; do mv "$i" "${i%%.JPG}.jpg"; done
for i in *.MOV; do mv "$i" "${i%%.MOV}.mov"; done
for i in *.AAE; do mv "$i" "${i%%.AAE}.aae"; done
for i in *.MP4; do mv "$i" "${i%%.MP4}.mp4"; done
for i in *.PNG; do mv "$i" "${i%%.PNG}.png"; done
```