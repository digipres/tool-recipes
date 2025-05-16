---
title: MDI to TIFF File Converter
description: MDI to TIFF File Converter is a command line tool, which allows you to convert one or more MDI files to TIFF.
homepage:	https://www.microsoft.com/en-ca/download/details.aspx?id=30328
cost:	0
platforms:	Windows 7, Windows Server 2008, Windows Vista
input-formats:	MDI
output-formats:	TIFF
function:	File Format Migration
content-type:	Image
container-type: docker
container-tag: md2tif
os-type: windows
---

# MDI to TIFF File Converter

## Overview
MDI is a proprietary file format of MODI (Microsoft Office Document Imaging), which was deprecated as part of Office 2010. This conversion tool will allow you to view MDI files after they are converted to TIFF. TIFF files may be viewed using a variety of image viewing programs, such as the Windows Fax and Image Viewer.

## Links

- [MDI - Just Solve the File Format Problem](http://fileformats.archiveteam.org/wiki/MDI)
- [About Microsoft Document Imaging Format (MDI) - Julio Beltrán](http://juliobeltran.wikidot.com/trad:about-mdi-format)
- [Search DISCMASTER 2](https://discmaster.textfiles.com/search?extension=.mdi&format=microsoftDocumentImagingFormat) extension then use format filters, files ID with byte match using SF
- IA has software too: [Microsoft MDI2TIF Converter and Microsoft SharePoint Designer 2007 : Microsoft : Free Download, Borrow, and Streaming : Internet Archive](https://archive.org/details/mdi-2-tifconverter

## Builder

This builder uses a Windows Docker container to run the tool, because it does not seem to be compatible with WINE.  When running with WINE, issues like the ones below are logged, and the file write operation fails.

```
0024:fixme:enhmetafile:PlayEnhMetaFileRecord type 119 is unimplemented
0024:fixme:enhmetafile:PlayEnhMetaFileRecord EMR_EXTCREATEPEN: Need to copy brush bitmap
0024:fixme:enhmetafile:PlayEnhMetaFileRecord Unknown imode 4
```

Using Windows involves [switching modes in Docker Desktop](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-10-and-windows-11-2) and running from e.g. PowerShell not WSL2.  But this means `make` is not present, which complicated things.

```
> docker build -t mdi2tif .
```

```
> docker run mdi2tif
usage:    mdi2tif.exe -source <sourcefile> -log <logfile> [-dest <destfile]
              [-overwrite] [-subfolders]
examples: mdi2tif.exe -source contoso1.mdi -log log.txt
          mdi2tif.exe -source c:\mdifiles -dest c:\tiffiles -subfolders
                      -log c:\tiffiles\log.txt
-help or -?
       List of possible arguments
-source <sourcefile>
       Source directory path or filename. This argument is required. Example:
       mdi2tif.exe -source c:\mdifiles ...
-dest <destfile>
       Destination directory path or filename. Example:
       mdi2tif.exe ... -dest c:\tifoutput ...
-overwrite
       Specifies that the destination files should overwrite any existing file
-subfolders
       Specifies that files within the directory path and all its subfolders
       will be converted
-log <logfile>
       Specifies the log file for the conversion tool. This argument is
       required. Example:
       mdi2tif.exe ... -log c:\tiffs\convertlog.txt
-discardannot
       Specifies that the annotations in the source files should not be kept
       in the destination files
```

