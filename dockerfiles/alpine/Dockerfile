FROM alpine:3.18

# 1. Update and install core graphical components
RUN apk update && apk add --no-cache \
    xorg-server \
    xf86-video-dummy \
    i3wm \
    xterm \
    dbus \
    mesa-dri-swrast \
    xvfb

# 2. Environment setup
ENV DISPLAY=:0
WORKDIR /root

# 3. Create a more reliable entrypoint script
RUN printf "#!/bin/sh\n\
rm -f /tmp/.X0-lock\n\
Xvfb :0 -screen 0 1024x768x24 &\n\
sleep 2\n\
export DISPLAY=:0\n\
exec i3\n" > /entrypoint.sh && chmod +x /entrypoint.sh

# 4. Start the system
CMD ["/entrypoint.sh"]
