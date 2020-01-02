FROM node:alpine

EXPOSE 3001

ENV NODE_ENV=production
ENV MONGODB_URI=mongodb+srv://docker-user:Docker12345@mycluster0-ox0pu.mongodb.net/full_stack_course?retryWrites=true&w=majority
ENV PORT=3001

WORKDIR /app
COPY ./backend .

RUN npm install

CMD npm start