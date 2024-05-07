FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /backend

COPY package.json ./
COPY package-lock.json ./
COPY src/ src/
COPY tsconfig.json ./
COPY .env.sample ./.env

RUN npm install
RUN npm run build

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

WORKDIR /backend

EXPOSE 8888

COPY package.json ./
COPY package-lock.json ./
COPY --from=BUILDER /backend/dist ./dist
COPY .env.sample ./.env

RUN npm install

CMD ["npm", "run", "start"]