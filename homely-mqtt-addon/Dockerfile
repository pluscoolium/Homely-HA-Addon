FROM ghcr.io/home-assistant/amd64-base:3.19

# Install dependencies (Node 20 is default in Alpine 3.19)
RUN apk add --no-cache nodejs npm python3 make g++

WORKDIR /app

# Copy the entire application
COPY rootfs/app /app

# Install dependencies including js-yaml
RUN npm install
RUN npm install js-yaml

# Build TypeScript
RUN npm run build

# Remove devDependencies but keep js-yaml
RUN npm prune --production

# Copy our add-on run script
COPY run.sh /
RUN chmod a+x /run.sh

CMD ["/run.sh"]
