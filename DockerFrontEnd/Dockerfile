# Stage 1: Build an Angular Docker Image
FROM node as build
WORKDIR /apps
COPY . .
RUN npm install
COPY . /apps
ARG configuration=production
RUN npm run build -- --outputPath=./dist/out --configuration $configuration

# Stage 2: Use the compiled app, ready for production with Nginx
FROM nginx:alpine
COPY nginx-custom.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /apps/dist/out/ /usr/share/nginx/html
