FROM docker.io/library/node:21-alpine3.18 AS BUILDER

WORKDIR /backend

COPY package.json ./
COPY package-lock.json ./
COPY src/ ./
COPY tsconfig.json ./

CMD tree
RUN npm ci
RUN npm run build

FROM docker.io/library/node:21-alpine3.18 AS RUNNER

EXPOSE 8888

WORKDIR /backend

COPY package.json ./
COPY package-lock.json ./
# COPY --from=BUILDER /backend/dist ./

RUN npm ci --omit=dev

# CMD [ "node", "/backend/backend.js" ]
CMD [ "npm", "install" ]
CMD [ "npm", "run" , "dev" ]
CMD [ "npm", "run", "test" ]