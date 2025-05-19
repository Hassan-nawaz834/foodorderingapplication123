# Build stage
FROM node:14 as builder

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

# Runtime stage
FROM node:14-alpine

WORKDIR /app

# Copy from builder stage
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app ./

# Environment variables
ENV MONGO_URI=mongodb://malikrashid:malikrashid@ac-ggtk7kz-shard-00-00.kk5lwo3.mongodb.net:27017,ac-ggtk7kz-shard-00-01.kk5lwo3.mongodb.net:27017,ac-ggtk7kz-shard-00-02.kk5lwo3.mongodb.net:27017/foodordering?replicaSet=atlas-13mxse-shard-0&ssl=true&authSource=admin
ENV PORT=5000
ENV NODE_ENV=production

# Install production dependencies only
RUN npm prune --production

# Create directory for logs
RUN mkdir -p ./logs

EXPOSE 5000

# Use your Express entry point
CMD ["node", "./bin/www"]