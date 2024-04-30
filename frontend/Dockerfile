FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /frontend

COPY package.json ./
COPY package-lock.json ./
COPY src/ ./src/
COPY tsconfig.json ./
COPY tsconfig.node.json ./


RUN npm ci
RUN npm install

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

EXPOSE 80

WORKDIR /frontend

COPY package.json ./
COPY package-lock.json ./
COPY --from=BUILDER /frontend/dist ./dist/

RUN npm ci --only=production

CMD ["npm", "run", "dev"]
