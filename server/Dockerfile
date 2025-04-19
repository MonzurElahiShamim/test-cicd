# Use official Node.js LTS image as base
FROM node:lts-bullseye

# Set working directory
WORKDIR /app/server

# Set environment variable for Prisma
ENV DATABASE_URL=postgresql://postgres:postgres@host.docker.internal:5434/PRO_CG?sslmode=require
# Install PM2 globally
RUN npm install -g pm2@latest

# Copy package.json and install project dependencies
COPY node/package.json node/package-lock.json ./
RUN npm install

# Copy the rest of the server code
COPY node/ ./

# Copy the .server_env file
COPY .server_env /app/

# Validate and generate Prisma
RUN npx prisma validate
RUN npx prisma generate

# Expose the port your app runs on
EXPOSE 3000

# Start the server with PM2
CMD ["pm2-runtime", "server.js"]

