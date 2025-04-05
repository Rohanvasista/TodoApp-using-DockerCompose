# -------- Stage 1: Build Stage --------
FROM node:18 AS builder

# Set working directory
WORKDIR /app

# Copy dependency files and install
COPY package*.json ./
RUN npm install

# Copy the rest of the app
COPY . .

# -------- Stage 2: Production Stage (Distroless) --------
FROM gcr.io/distroless/nodejs18

# Set working directory inside distroless
WORKDIR /app

# Copy only the built app and dependencies from builder
COPY --from=builder /app /app

# Expose port (for documentation purposes; distroless ignores EXPOSE)
EXPOSE 5000

# Run the app (no shell, no bash in distroless, use absolute path)
CMD ["server.js"]
