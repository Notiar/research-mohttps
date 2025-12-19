FROM oven/bun

# Install ps
RUN apt-get update && apt-get install -y procps

WORKDIR /app
COPY package.json /app
COPY bun.lock /app
RUN bun install

COPY . /app

CMD ["bun", "run", "start:dev"]