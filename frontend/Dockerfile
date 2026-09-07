# =========================
# BUILD STAGE
# =========================
FROM node:24-alpine AS builder

RUN apk update && apk upgrade

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build


# =========================
# PRODUCTION STAGE
# =========================
FROM dhi.io/nginx:1.30-alpine


COPY --from=builder /app/dist /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80

CMD ["-g", "daemon off;"]

