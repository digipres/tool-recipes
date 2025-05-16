# Start from the will Windows image
FROM mcr.microsoft.com/windows:ltsc2019

# Add and install the software:
ADD MDI2TIFConverter.exe /temp/
RUN /temp/MDI2TIFConverter.exe /quiet /passive

# Use the install folder as the working directory:
WORKDIR "/Program Files (x86)/modiconv/"

RUN dir

# Always run this tool:
ENTRYPOINT [ "/Program Files (x86)/modiconv/MDI2TIF.EXE" ]
#CMD [ "MDI2TIF.EXE" ]