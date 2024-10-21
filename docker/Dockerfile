# Use a Node.js base image
FROM node:20.15.1

# Install wrangler CLI
RUN npm install -g @cloudflare/wrangler

# Set the working directory inside the container
WORKDIR /app

# Copy necessary files
COPY package.json pnpm-lock.yaml bindings.sh ./
COPY docker/.env ./

# Install dependencies
RUN npm install -g pnpm && pnpm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN pnpm run build

# Expose the port the app runs on
EXPOSE 3000

# Start the application
CMD ["/bin/bash", "-c", "bindings=$(./bindings.sh) && wrangler pages dev ./build/client $bindings