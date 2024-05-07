FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /backend

COPY package.json ./
COPY package-lock.json ./
COPY src/ src/
COPY tsconfig.json ./

RUN npm ci
RUN npm install
RUN npm run build

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

WORKDIR /backend

COPY package.json ./
COPY package-lock.json ./
COPY --from=BUILDER /backend/dist ./

#RUN npm ci --omit=dev

CMD [ "node", "/backend/server.js" ]