# User Service Dockerfile
FROM node:16-alpine

# Install curl for health checks
RUN apk add --no-cache curl

# Set working directory
WORKDIR /usr/src/app

# Copy package files first for better caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all source files
COPY . .

# Expose the application port
EXPOSE 3000

HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

# Start the application 
CMD ["npm", "start"]
