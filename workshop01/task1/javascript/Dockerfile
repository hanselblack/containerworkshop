FROM node:17

#Set Argument

ARG APP_DIR=/app

## build
WORKDIR ${APP_DIR}

# copy files from local into the image
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views

# install dependencies
RUN npm ci

# run
ENV APP_DIR=/app
ENV PORT=3000

WORKDIR ${APP_DIR}

# what are the required ports
EXPOSE ${PORT}

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl http://localhost:${PORT}}/healthz || exit 1

# run the app
ENTRYPOINT [ "node", "main" ]
