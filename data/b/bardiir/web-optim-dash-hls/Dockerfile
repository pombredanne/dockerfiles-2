FROM bardiir/caesium  
  
RUN buildDeps="build-base \  
zlib-dev \  
freetype-dev \  
jpeg-dev \  
git \  
libmad-dev \  
ffmpeg-dev \  
coreutils \  
yasm-dev \  
lame-dev \  
x264-dev \  
libvpx-dev \  
x265-dev \  
libass-dev \  
libwebp-dev \  
opus-dev \  
libogg-dev \  
libvorbis-dev \  
libtheora-dev \  
libxv-dev \  
alsa-lib-dev \  
xvidcore-dev \  
openssl-dev \  
libpng-dev \  
jack-dev \  
sdl-dev \  
openjpeg-dev \  
expat-dev" && \  
apk add --no-cache --update ${buildDeps} ffmpeg libxslt openssl libpng bash &&
\  
git clone https://github.com/squidpickles/mpd-to-m3u8.git /app/mpd-to-m3u8 &&
\  
rm -rf !$/.git && \  
git clone https://github.com/gpac/gpac.git /tmp/gpac && \  
cd /tmp/gpac && ./configure && make -j4 && make install && make distclean &&
rm -rf /tmp && \  
apk del ${buildDeps} && rm -rf /var/cache/apk/*  
  
COPY ./transcode.sh /app/transcode.sh

