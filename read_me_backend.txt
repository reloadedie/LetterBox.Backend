Архитектурная сводка Проекта "LetterBox"
--------------------------------------------------------------------------------
Технологический стек

Платформа разработки: .NET 9.0
Контейнеризация: Docker Compose
архитектурный стиль: Clean Architecture

Backend - 
	Язык: C#,
	Веб-Фреймворк: ASP.NET Core,
	API Docs: Swagger UI + Open API,
	СУБД: PostgreSQL
	ORM: Entity Framework Core

Пакеты Nuget:
Npgsql.EntityFrameworkCore.PostgreSQL 9.0.4
Microsoft.EntityFrameworkCore.Design 9.0.9
Microsoft.EntityFrameworkCore.Tools 9.0.9
Microsoft.AspNetCore.OpenApi 9.0.9

Frontend - 
	Язык: TypeScript
	UI: React + HeroUI,
	Инструмент сборки и dev-сервер: Vite,
 	Runtime TS/JS: Node.js

Библиотека готовых компонентов для UI:
HeroUI

-----------------------------------------------------------------------------------
Структура проекта "LetterBox"
	LetterBox.Frontend--> ReactApp (typescript) with Vite + Node.js
		packages:
			1. Material UI (Библиотека пользовательских компонентов)
			2. 

	LetterBox.Backend --> Clean Architecture
		LetterBox.API --> C# ASP.NET WEB.API (controllers)
			packages:
			1. Microsoft.AspNetCore.OpenApi 9.0.9 (Provides APIs for annotating route handler endpoints in ASP.NET Core with OpenAPI annotations.)
			2. Microsoft.EntityFrameworkCore.Design 9.0.0 (Shared design-time components for Entity Framework Core tools.)
			3. Swashbuckle.AspNetCore 9.0.4 (Swagger tools for documenting API's)
			4. Swashbuckle.AspNetCore.SwaggerGen 9.0.4 (swagger generator for API's)

		LetterBox.Application --> Библиотека классов C# (Use Cases)
		LetterBox.Contracts --> Библиотека классов C# ()
		LetterBox.Domain --> Библиотека классов C# (Entities)
		LetterBox.Infrastructure --> Библиотека классов C# (Adapters)
		LetterBox.Infrastructure.Authentitication --> Библиотека классов C# (Adapters)
		
вспомогательные файлы:
dockerfile + .yml --> существует
SAST отчёт --> не существует
database.script --> не существует (миграции в C# ASP.NET WEB.API с Infrastructure)

==============================================
КАК ЗАПУСТИТЬ БЕКЕНД?

1. запустить pgAdmin и DockerDesktop. перекинуть контейнер из файла .yml в Docker letterboxbackend

2. в файлах фронта найти env.local и заменить на свои данные. если файла нет (вполне вероятно), создайте его в контексте

VITE_API_IP=ip компа с запущенным React Vite (frontend), ниже порт соответственно
VITE_API_PORT=7028

3. Миграции с проектов Infracstructure и Infracstructure-Authetnitication перекинуть (удалить папки Migrations и прописать команды ниже)

cd src

запуск миграции
dotnet ef migrations add initial -p .\letterbox.infrastructure\ -s .\letterbox.api

применение миграции
dotnet ef database update -p .\letterbox.infrastructure\ -s .\letterbox.api

прописать эту команду также и для Infracstructure-Authetnitication

4. в /API в Program.cs найти ip бекенда и указать свой. можно перекинуть в секреты

5. ознакомьтесь со следующей частью в файле "hot_to_full_work"
