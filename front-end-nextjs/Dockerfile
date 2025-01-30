FROM node:18-alpine AS base 

# Set the working directory inside the container
WORKDIR /app 

# Copy lock files for dependency management
COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

# Install dependencies based on the lockfile available
RUN \
 if [ -f yarn.lock ]; then yarn --frozen-lockfile; \
 elif [ -f package-lock.json ]; then npm ci; \
 elif [ -f pnpm-lock.yaml ]; then corepack enable pnpm && pnpm i --frozen-lockfile; \
 else echo "Lockfile not found." && exit 1; \
 fi

 # Copy all project files to the working directory
COPY . . 

# Build the application
RUN npm run build

# Expose port 3000 for the application
EXPOSE 3000

# Define the command to run the application
CMD ["npm", "start"]