# Product Service Dockerfile
FROM node:16-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package files first for better caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all source files
COPY . .

# Expose the application port
EXPOSE 3001

# Start the application 
CMD ["npm", "start"]
