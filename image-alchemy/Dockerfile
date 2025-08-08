# Start with WINE:
FROM scottyhardy/docker-wine:latest

# Add DOSBox:
RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" apt-get install -y --no-install-recommends \
        dosbox \
    && rm -rf /var/lib/apt/lists/*

# Set up a working directory:
RUN mkdir /tool/
WORKDIR /tool/

## Download Image Alchemy 1.11:
#RUN wget -O ImageAlchemy.7z "http://old-dos.ru/dl.php?id=2687"
#RUN 7z x ImageAlchemy.7z
#RUN ls -la

# Download Image Alchemy 1.8 (no PNG support):
RUN wget "http://cd.textfiles.com/pdos9606/GRAPHICS/MISC/ALCH1_8.ZIP"
RUN unzip ALCH1_8.ZIP
RUN ls -la

# Download an unusual file (OS/2 BMP)
RUN wget -O TEST.BMP "https://discmaster.textfiles.com/file/570/OS2%20Arsenal%20v1.0%20(Disc%201)(Arsenal%20Computer).ISO/os2_max/dwnsrt60.zip/DOWNSORT.BMP"

# Run the test so we can check everything is set up:
# (this reads the TEST.BMP and writes a TEST.TIF)
RUN wine ALCHEMY.EXE TEST.BMP -t
# (this reads the TEST.BMP and writes a TEST.PNG)
#RUN wine ALCHEMY.EXE TEST.BMP ---n

# Default command to run:
CMD [ "wine", "ALCHEMY.EXE" ]

# Limit logging:
ENV WINEDEBUG=-all

# WINE entrypoint hook:
ENTRYPOINT ["/usr/bin/entrypoint"]
