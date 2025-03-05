# Используем официальный образ Node.js
FROM node:20

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем package.json и устанавливаем зависимости
COPY package.json ./
RUN npm install

# Копируем остальной код
COPY . .

RUN npm update

# Собираем проект
RUN npm run build

# Запускаем сервер
CMD ["npm", "start"]