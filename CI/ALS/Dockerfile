# gives a docker image below 200 MB
FROM mhart/alpine-node:10

RUN apk add --update 	python 	build-base git
ENV NODE_ENV "production"
ENV PORT 3000
EXPOSE 3000
# create local user to avoid running as root
RUN addgroup mygroup && adduser -D -G mygroup myuser && mkdir -p /usr/src/app && chown -R myuser /usr/src/app

# Prepare app directory
WORKDIR /usr/src/app
COPY package*.json ./
COPY .snyk ./

USER myuser

RUN npm install

# Install our packages
RUN npm ci --production

# Copy the rest of our application, node_modules is ignored via .dockerignore
COPY . /usr/src/app

# Start the app
CMD ["node", "."]
