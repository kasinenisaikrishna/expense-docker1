FROM node:20 as builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


FROM node:20.18.0-alpine3.20 
EXPOSE 8080
ENV DB_HOST="mysql"
# adding expense user and group to restrict the root access to other users
RUN addgroup -S expense && adduser -S expense -G expense && \
    mkdir /opt/server && \
# changing the ownership to expense user
    chown -R expense:expense /opt/server
WORKDIR /opt/server
COPY --from=builder /opt/server /opt/server
USER expense
CMD [ "node", "index.js" ]

# Before best practices implemented
# FROM node:20
# EXPOSE 8080
# # we have to specify mysql container ip address in DB_HOST but mysql container is in docker bridge network created by docker now it is docker responsibility to provide mysql container ip address as ip address is not permanent we have to make use of route53 records but in docker route53 we cannot use, hence we have to name the mysql container and use the name as below, to name a container docker run -d --name mysql mysql:v1 if container exists remove the container and name it.
# # remove step for container docker ps and docker rm -f container-id(force-remove)
# # containers inside the docker default bridge network cannot able to communicate each other hence we have to create our own network to establish communication between containers
# ENV DB_HOST="mysql"
# # creating dir /opt/server same like /app in our vm we use RUN instruction to create dir
# RUN mkdir /opt/server 
# # instead of cd we have to use WORKDIR to move to /opt/server
# WORKDIR /opt/server
# # copying package.json and all .js files into current folder that is /opt/server . denotes current folder as the code is already extracted here we are using COPY if code is not extracted we have to use ADD instruction to extract code, schema is not required as we already configured backend
# COPY package.json .
# COPY *.js .
# # next we need to install dependencies to install dependencies we have to run npm install and npm install we have to run where package.json exists
# RUN npm install
# # now we need to run index.js as below
# CMD [ "node", "index.js" ]
# # now backend has to connect to mysql 