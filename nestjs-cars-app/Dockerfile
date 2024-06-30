# Use Node.js 14 as the base image
FROM node:14 AS production

# Set the NODE_ENV environment variable
ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Set the working directory inside the container
WORKDIR /usr/src/api

# Copy package.json and yarn.lock files to the working directory
COPY package.json yarn.lock ./

# Install @nestjs/cli using npx
RUN yarn add --global @nestjs/cli

# Install production dependencies
RUN yarn install --production=true

# Install netcat for health checks or other purposes
RUN apt-get -q update && apt-get -qy install netcat

# Copy the rest of your application code
COPY . .

# Build your application
RUN yarn build

# Run TypeORM migrations and start the application
CMD ["sh", "-c", "yarn typeorm migration:run && yarn start:prod"]
