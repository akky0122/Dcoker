FROM node:14-alpine
WORKDIR /app
COPY package*.json ./
RUN apk add --no-cache npm && \
    npm install --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]

