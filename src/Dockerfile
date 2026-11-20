FROM node:26-alpine

# Porta padrão da aplicação. Pode ser trocada:
#   no build: docker build --build-arg PORT=4000 ...
#   na execução: docker run -e PORT=4000 ...
ARG PORT=3000
ENV NODE_ENV=production \
    PORT=${PORT}

WORKDIR /app

# Dependências primeiro, para aproveitar o cache de camadas
COPY package.json package-lock.json ./
RUN npm ci --omit=dev && npm cache clean --force

# Somente os arquivos necessários para rodar a aplicação
COPY --chown=node:node server.js convert.js ./
COPY --chown=node:node config ./config
COPY --chown=node:node views ./views

# Não rodar como root
USER node

EXPOSE ${PORT}

CMD ["node", "server.js"]
