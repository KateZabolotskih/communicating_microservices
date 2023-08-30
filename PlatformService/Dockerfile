# Указываем базовый образ
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Копируем исходный код в контейнер
COPY *.csproj ./
# Восстанавливаем зависимости и выполняем сборку проекта
RUN dotnet restore

COPY . ./
# Публикуем собранный проект в отдельной директории
RUN dotnet publish -c Release -o out

# Отдельный образ для развертывания
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app

# Копируем только необходимые файлы из предыдущего образа
COPY --from=build-env /app/out .
# Запускаем приложение
ENTRYPOINT ["dotnet", "PlatformService.dll"]
