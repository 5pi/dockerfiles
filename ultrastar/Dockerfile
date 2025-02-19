FROM debian AS builder

RUN apt-get update && apt-get install -y git build-essential

RUN git clone https://github.com/UltraStar-Deluxe/USDX.git /usr/src/ultrastar
WORKDIR /usr/src/ultrastar

RUN apt-get install -qy automake make gcc fpc libsdl2-image-dev libavformat-dev \
    libavcodec-dev libavutil-dev libswresample-dev libswscale-dev libsqlite3-dev \
    libfreetype6-dev portaudio19-dev libportmidi-dev liblua5.3-dev libopencv-videoio-dev \
    fonts-dejavu

RUN ./autogen.sh
RUN ./configure
RUN make

FROM debian
RUN apt-get -qy update && apt-get install -y libsdl2-image-2.0-0 libsqlite3-0 libportaudio2 \
    libportmidi0 libavcodec59 libavformat59 libswscale6 liblua5.3-0 xserver-xorg \
    xserver-xorg-input-evdev xserver-xorg-input-all

COPY --from=builder /usr/src/ultrastar/game /ultrastar
COPY run.sh /
CMD ["/run.sh"]
