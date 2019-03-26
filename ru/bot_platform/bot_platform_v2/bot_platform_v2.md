# **Bot Platform 2.0**

  

# Content



- [Что такое Bot Platform](#что-такое-bot-platform)

- [Архитектура](#архитектура)

- [Как создать бота с помощью Bot Platform](#как-создать-бота-с-помощью-bot-platform)

- [Шаг 1. Регистрация бота в мессенджере](#шаг-1.-регистрация-бота-в-мессенджере.)

  - [Telegram](#**telegram**)

  - [Viber](#**viber**)

  - [Facebook Messenger](#**facebook-messenger**)

- [Шаг 2. Создание компании в Sender](#шаг-2.-создание-компании-в-sender)

- [Шаг 3. Подключение бота к Bot Platform](#шаг-3.-подключение-бота-к-bot-platform)

- [Базовый функционал Bot Platform](#базовый-функционал-bot-platform.)

  - [Курс валют](#курс-валют)

  - [Смена языка общения](#смена-языка-общения)

  - [Стандартный опрос](#стандартный-опрос)

  - [Подключение оператора](#подключение-оператора)

  - [Опрос NPS](#опрос-nps)

- [Объекты папки Bot Platform 2.0](#объекты-папки-bot-platform-2.0)

  - [Процессы Viber/Telegram/Facebook Receiver](#процессы-viber/telegram/facebook-receiver)

  - [Процесс Main](#процесс-main)

  - [Описание параметров](#описание-параметров)

  - [Event](#event)

  - [Процесс Router](#процесс-router)

  - [Процесс Send Message](#процесс-send-message)

  - [Описание параметров](#описание-параметров)

  - [Папка Config](#папка-config)

  - [Tokens](#tokens)

  - [Command](#command)

  - [Attachments](#attachments)

  - [Пример](#пример)

- [Как работает Dynamic attachment?](#как-работает-dynamic-attachment?)

- [Добавление шаблона](#добавление-шаблона)

- [Массив элементов items](#массив-элементов-items)

- [Преобразование JSON](#преобразование-json)

- [Localization](#localization)

- [User Profile](#user-profile)

- [Расширение функций бота](#расширение-функций-бота)

- [Добавление новой команды](#добавление-новой-команды)

- [Работа с конфигурацией в Bot platform](#работа-с-конфигурацией-в-bot-platform)

  - [Commands](#commands)

  - [Localization](#localization)

  - [Attachments](#attachments)

- [Логика процесса](#логика-процесса-авторизации)

  
  
  

# Что такое Bot Platform

**Bot Platform** - это набор универсальных процессов в Corezoid для создания и управления ботами в наиболее популярных мессенджерах:

-   Facebook Messenger
-   Viber
-   Telegram.

Благодаря Bot Platform Вы можете создавать универсальные бизнес-процессы, которые доступны во всех мессенджерах, а не разрабатывать бизнес-логику под каждый из мессенджеров отдельно.

# Архитектура

  ![](../img/botplatform2_0/architecture.png)
