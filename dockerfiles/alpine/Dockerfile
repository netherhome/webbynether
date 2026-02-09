FROM alpine:3.18

# 1. Install the graphical environment (X11 + i3 window manager)
RUN apk add --no-cache \
    xorg-server \
    xf86-video-dummy \
    i3wm \
    i3status \
    xterm \
    xhost \
    font-noto \
    dbus \
    mesa-dri-swrast

# 2. Set up the environment for the browser engine
ENV DISPLAY=:0
WORKDIR /root

# 3. Create a simple startup script to launch the desktop
RUN echo '#!/bin/sh\n\
rm -f /tmp/.X0-lock\n\
Xvfb :0 -screen 0 1024x768x24 &\n\
sleep 2\n\
exec i3' > /entrypoint.sh && chmod +x /entrypoint.sh

# 4. Tell WebVM to run the desktop script on boot
CMD ["/entrypoint.sh"]
