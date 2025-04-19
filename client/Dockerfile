# Use an official Node.js image as the base (LTS version for stability)
FROM node:18-alpine AS base

# Set working directory inside the container
WORKDIR /app

# Copy package.json and yarn.lock for dependency installation
COPY react/package.json react/yarn.lock ./

# Install dependencies using Yarn
RUN yarn install --frozen-lockfile

# Copy the rest of the application code
COPY ./react/ .

# Build the React app for production
RUN yarn build


# Use a lightweight Nginx image to serve the built app
FROM nginx:alpine AS production

# Copy the built files from the previous stage
COPY --from=base /app/dist /usr/share/nginx/html

# Copy a custom Nginx configuration (optional, for SPA routing)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 for the Nginx server
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
