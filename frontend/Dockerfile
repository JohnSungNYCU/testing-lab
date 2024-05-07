FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /frontend

COPY package.json ./
COPY package-lock.json ./
COPY src/ src/
COPY tsconfig.json ./
COPY tsconfig.node.json ./
COPY index.html ./

RUN npm install
RUN npm run build

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

EXPOSE 5173

WORKDIR /frontend

COPY package.json ./
COPY package-lock.json ./
COPY tsconfig.json ./
COPY tsconfig.node.json ./
COPY --from=BUILDER /frontend/dist ./

RUN npm install

CMD ["npm", "run", "dev"]