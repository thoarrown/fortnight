FROM node:lts-alpine
WORKDIR /app

COPY package.json yarn.lock ./

RUN npm install --frozen-lockfile

COPY . .
COPY --from=deps /app/node_modules ./node_modules

RUN sh ./tools/docker/images/api/build.sh
# Build
RUN npx nx run api:build:production --no-cache

COPY --from=builder /app/dist/apps/fortnight ./
ENV PORT=3333
EXPOSE ${PORT}
RUN npm install --production
# dependencies that nestjs needs
RUN npm install reflect-metadata tslib rxjs @nestjs/platform-express
CMD node ./main.js