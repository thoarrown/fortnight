FROM node:12.18-alpine as builder
WORKDIR /app

COPY package.json yanr.lock ./

RUN yarn

COPY . .

# COPY /app/node_modules ./node_modules
# COPY --from=deps /app/node_modules ./node_modules

# Build
RUN yarn nx run fortnight:build:production --no-cache

COPY ./dist/apps/fortnight ./
ENV PORT=3333
EXPOSE ${PORT}
RUN npm install --production
# dependencies that nestjs needs
RUN npm install reflect-metadata tslib rxjs @nestjs/platform-express
CMD node ./main.js