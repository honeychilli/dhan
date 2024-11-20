# Use an official Node.js image to build the app
FROM node:18 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the application source code
COPY . .

# Build the Vite app
RUN npm run build

# Use a lightweight web server (nginx) to serve the app
FROM nginx:alpine

# Copy the production build from the builder stage
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 80 to the host
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
