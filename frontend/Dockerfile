# Development stage - Optimized for Angular development
FROM node:20-alpine

WORKDIR /app

# Copy only package files first (better layer caching)
COPY package*.json ./

# Install dependencies including Angular CLI
RUN npm ci --prefer-offline --no-audit

# Copy source code
COPY . .

# Disable Angular analytics during build
RUN npx ng analytics off || true

# Expose port for Angular dev server
EXPOSE 4200

# Run Angular dev server with poll for file changes
# --poll detects changes in mounted volumes (important for Docker)
# --host 0.0.0.0 makes server accessible from host machine
CMD ["npx", "ng", "serve", "--host", "0.0.0.0", "--poll", "2000"]
