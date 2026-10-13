# Stage 1: Build React Application
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install --legacy-peer-deps

COPY . .

# Frontend API paths
ENV REACT_APP_USER_SERVICE=/api/users
ENV REACT_APP_SEARCH_SERVICE=/api/search
ENV REACT_APP_BOOKING_SERVICE=/api/bookings
ENV REACT_APP_PAYMENT_SERVICE=/api/payments
ENV REACT_APP_NOTIFICATION_SERVICE=/api/notifications

RUN CI=true npm run build

# Stage 2: Nginx Runtime
FROM nginx:alpine

COPY --from=builder /app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
