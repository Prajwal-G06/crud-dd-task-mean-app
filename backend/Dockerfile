# ---------- deps stage ----------
FROM node:18-alpine AS deps

WORKDIR /app

# install only production deps
COPY package*.json ./
RUN npm install --omit=dev

# ---------- runtime stage ----------
FROM node:18-alpine

WORKDIR /app

# copy node_modules from deps stage
COPY --from=deps /app/node_modules ./node_modules

# copy app source
COPY . .

# security best practice
USER node

EXPOSE 3000

CMD ["node", "server.js"]
