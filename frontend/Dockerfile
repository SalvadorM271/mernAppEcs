ARG enviroment_conf

# build application
FROM node:16-alpine as build
WORKDIR /app
COPY package.json ./
COPY package-lock.json ./
RUN npm install
COPY . ./
RUN npm run build

# release application
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY $enviroment_conf /etc/nginx/$enviroment_conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]