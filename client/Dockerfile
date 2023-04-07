# Set the base image to Node.js
FROM node:16-alpine AS builder

# Create and set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install the dependencies
RUN npm install --production --silent

# Copy the rest of the application code to the container
COPY . .

# Build the React app
RUN npm run build

# Set the base image to Nginx
FROM nginx:1.21-alpine

# Expose a react app port
EXPOSE 3000

# Copy the nginx config file to the container
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy the built React app from the previous stage to the container
COPY --from=builder /app/build /usr/share/nginx/html
