Image Alchemy
=============


```
docker build -t alchemy .
```

```
docker run alchemy wine ALCHEMY.EXE 
```

Convert Spaceward Graphics to TIFF:
```
ALCHEMY.EXE "FILE.R" -t
```

You can use `---n` to convert to PNG, but only later versions support that (1.8 does not, 1.11 does).

Quickly becomes a pain due to file permissions - the container runs as a different user.  Copying the test file to `/tmp/` first does work:

```
cp DOWNSORT.BMP /tmp
docker run -v /tmp:/tmp -w /tmp alchemy wine /tool/ALCHEMY.EXE DOWNSORT.BMP ---n
cp /tmp/DOWNSORT.PNG .
```

So this could be wrapped up as a script.

Noting this:

```
display DOWNSORT.BMP
display-im6.q16: length and filesize do not match `DOWNSORT.BMP' @ error/bmp.c/ReadBMPImage/848.
```
and it also looks wonky. But then it's an OS/2 BMP so maybe that's the problem

Related: 

- [Image Alchemy - Just Solve the File Format Problem](http://justsolve.archiveteam.org/wiki/Image_Alchemy)
- [Image Alchemy User's Manual - Internet Archive](https://archive.org/details/manualzilla-id-5894277/mode/2up)
- [notebook/spaceward-research.md at main · anjackson/notebook](https://github.com/anjackson/notebook/blob/main/spaceward-research.md)


![](discmaster-v1.8-demo-warning.png)