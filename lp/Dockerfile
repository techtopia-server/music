FROM alpine
RUN apk update && apk upgrade
RUN apk add ffmpeg
WORKDIR /app
COPY ./start.sh /app/start.sh
ENTRYPOINT ffmpeg -y -i http://192.168.1.36:5005/stream -f u16le -acodec pcm_s16le -ac 2 -ar 48000 /tmp/snap/lp
