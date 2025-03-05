#FROM node:20
FROM node:20.18.3-alpine3.21  as builder
#using this image as baseOS to reduce backend image size
WORKDIR /opt/backend
COPY package.json ./
COPY *.js ./
RUN npm install 

FROM node:20.18.3-alpine3.21 
RUN addgroup -S expense && adduser -S expense -G expense && \
#command to create user and grp in alpine
 mkdir /opt/backend && \
 chown -R expense:expense /opt/backend
WORKDIR /opt/backend
ENV DB_HOST="mysql"
USER expense
#container runs with expense user which is non root user which is secure way to run
COPY --from=builder /opt/backend /opt/backend
#Using multistage builder approach,here copying opt/backend dir from builder to our /opt/backend
CMD [ "node", "index.js" ]
