FROM alpine:latest

# 1. Install only the absolute essentials for a GUI
RUN apk add --no-cache \
    xorg-server \
    xvfb \
    i3wm \
    xterm \
    dbus \
    mesa-dri-swrast \
    ttf-dejavu

# 2. Setup Environment
ENV DISPLAY=:0
WORKDIR /root

# 3. Create entrypoint
RUN printf "#!/bin/sh\n\
rm -f /tmp/.X0-lock\n\
Xvfb :0 -screen 0 1024x768x24 &\n\
sleep 2\n\
export DISPLAY=:0\n\
exec i3\n" > /entrypoint.sh && chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
