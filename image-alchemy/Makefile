
build:
	docker build -t alchemy .

DOWNSORT.BMP:
	wget "https://discmaster.textfiles.com/file/570/OS2%20Arsenal%20v1.0%20(Disc%201)(Arsenal%20Computer).ISO/os2_max/dwnsrt60.zip/DOWNSORT.BMP"

test: DOWNSORT.BMP build
	file DOWNSORT.BMP
	cp DOWNSORT.BMP /tmp
	docker run -v /tmp:/tmp -w /tmp alchemy wine /tool/ALCHEMY.EXE DOWNSORT.BMP ---n 
	cp /tmp/DOWNSORT.PNG .
	file DOWNSORT.PNG