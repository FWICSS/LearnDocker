FROM alpine
ARG folder=/app
ARG file


RUN apk add --update nodejs

LABEL authors="dimitriaigle"

COPY $file $folder/

WORKDIR $folder

CMD ["node", "app.js"]
#CMD ["node", "/app/app.js"]
