# --- Giai đoạn 1: Build source code bằng Nodejs ---
FROM node:18-alpine as BUILD_IMAGE
WORKDIR /app

# Copy file package để cài thư viện trước (tối ưu cache)
COPY package*.json ./
RUN npm install

# Copy toàn bộ source code vào và build
COPY . .
RUN npm run build

# --- Giai đoạn 2: Chạy web bằng Nginx ---
FROM nginx:alpine

# Copy thư mục 'dist' vừa build được ở trên vào thư mục web của Nginx
COPY --from=BUILD_IMAGE /app/dist /usr/share/nginx/html

# Mở cổng 80 trong container
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]