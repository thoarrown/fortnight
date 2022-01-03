FROM node:12.18-alpine as builder
WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install --frozen-lockfile

COPY . .
RUN ls

# COPY /app/node_modules ./node_modules
# COPY --from=deps /app/node_modules ./node_modules

# Build
RUN npx nx run fortnight:build:production --no-cache

COPY --from=builder /app/dist/apps/fortnight ./
ENV PORT=3333
EXPOSE ${PORT}
RUN npm install --production
# dependencies that nestjs needs
RUN npm install reflect-metadata tslib rxjs @nestjs/platform-express
CMD node ./main.js