# FROM node:14-alpine As development

# ENV PORT=3333
# ENV PORT_SSR=4000

# EXPOSE ${PORT}

# WORKDIR /usr/src/app

# COPY ["package*.json", "nx.json", "./"]
# # COPY nx.json .

# RUN npm install

# COPY . .

# RUN npm install -g @nrwl/cli@13.4.3

# RUN nx build --prod
# CMD nx serve fortnight

# -----------------------
FROM node:14-alpine As development

WORKDIR /usr/src/app

# COPY package*.json ./

COPY ["package*.json", "nx.json", "./"]

RUN npm install --only=development

COPY . .

RUN npm install -g @nrwl/cli@13.4.3 --only=development
RUN npm run build
# RUN nx build --prod

FROM node:14-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --only=production

COPY . .

# COPY --from=development /usr/src/app/dist ./dist/apps/fortnight
COPY --from=development /usr/src/app/dist/apps/fortnight ./

CMD ["node", "main"]

# -----------------------
# FROM node:14-alpine as builder
# WORKDIR /app

# COPY package.json yarn.lock ./

# RUN yarn

# COPY . .

# # Build
# RUN yarn nx run fortnight:build:production --no-cache

# COPY ./dist/apps/fortnight ./
# ENV PORT=3333
# EXPOSE ${PORT}
# RUN npm install --production
# # dependencies that nestjs needs
# RUN npm install reflect-metadata tslib rxjs @nestjs/platform-express
# CMD node ./main.js