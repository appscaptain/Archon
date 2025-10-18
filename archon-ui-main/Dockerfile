# Simple Vite dev server setup
FROM node:18-alpine

WORKDIR /app

# Install system dependencies needed for some npm packages
RUN apk add --no-cache python3 make g++ git curl

# Copy package files
COPY package*.json ./

# Install dependencies including dev dependencies for testing
RUN npm ci

# Create coverage directory with proper permissions
RUN mkdir -p /app/coverage && chmod 777 /app/coverage

# Copy source code
COPY . .

# --- SURGICAL CHANGE 1: Add production build step ---
# This command compiles the React/Vite app into static files in the /app/dist/ directory.
RUN npm run build

# --- SURGICAL CHANGE 2: Install a production-ready static server ---
RUN npm install -g serve

# Expose the port configured in package.json (3737)
EXPOSE 3737

# --- SURGICAL CHANGE 3: Replace dev server CMD with production server CMD ---
# The old command is commented out and replaced. 'serve' will host the static files
# from the 'dist' directory created by the build step.
# CMD ["npm", "run", "dev"]
CMD ["serve", "-s", "dist", "-l", "3737"]
