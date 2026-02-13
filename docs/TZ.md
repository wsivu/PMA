1. Общее описание проекта

Personal Media Aggregator — это персональная система агрегации стриминговых источников с единым интерфейсом для поиска и просмотра фильмов, сериалов и аниме. Система не хранит контент, а интеллектуально ищет его по различным источникам в интернете и предоставляет единый интерфейс для просмотра.
Ключевые особенности:

    Единый каталог из TMDB и Shikimori

    Автоматический поиск видео по множеству источников

    Умный выбор лучшего источника для каждого контента

    Поддержка торрент-стриминга через WebTorrent

    Многопользовательская система с синхронизацией прогресса

    Персонализация на основе поведения пользователя

2. Цели и задачи
Основные цели:

    Создать единую точку доступа к разрозненным видео-источникам

    Обеспечить максимальное качество и доступность контента

    Предоставить персонализированный опыт просмотра

    Поддержать синхронизацию между устройствами

Задачи:

    Разработать бэкенд на Python + FastAPI

    Создать фронтенд на TypeScript + Next.js

    Реализовать систему поиска и агрегации источников

    Разработать универсальный видео-плеер

    Реализовать систему пользователей и синхронизации

    Настроить автоматическое обновление источников

3. Архитектура системы
3.1. Компоненты системы
text

┌─────────────────────────────────────────────────────────────┐
│                        Frontend (Next.js)                   │
│  • TypeScript + React + Tailwind CSS                        │
│  • Универсальный плеер (Video.js + WebTorrent)              │
│  • Адаптивный интерфейс                                     │
└──────────────────────────────┬──────────────────────────────┘
                                │ HTTP/WebSocket
┌──────────────────────────────▼──────────────────────────────┐
│                        Backend (FastAPI)                    │
│  • Python 3.11+                                             │
│  • FastAPI + SQLAlchemy + Pydantic                          │
│  • Асинхронные запросы к источникам                         │
└─────────────────┬─────────────────────┬─────────────────────┘
                  │                     │
         ┌────────▼────────┐    ┌──────▼────────┐
         │   SQLite/Redis  │    │ Внешние API   │
         │   • Кеш         │    │ • TMDB        │
         │   • Сессии      │    │ • Shikimori   │
         │   • Статистика  │    │ • Трекеры     │
         └─────────────────┘    └───────────────┘

3.2. Модульная структура
text

src/
├── backend/
│   ├── app/
│   │   ├── api/              # Маршруты FastAPI
│   │   │   ├── v1/           # API v1
│   │   │   │   ├── auth.py   # Аутентификация
│   │   │   │   ├── media.py  # Медиа-поиск
│   │   │   │   ├── player.py # Управление плеером
│   │   │   │   └── users.py  # Пользователи
│   │   ├── core/             # Конфигурация
│   │   ├── db/               # Модели и миграции
│   │   ├── services/         # Бизнес-логика
│   │   │   ├── aggregator/   # Агрегатор источников
│   │   │   ├── metadata/     # Поиск метаданных
│   │   │   ├── player/       # Сервис плеера
│   │   │   └── scanner/      # Сканер источников
│   │   └── utils/            # Утилиты
│   ├── migrations/           # Alembic миграции
│   └── requirements.txt
├── frontend/
│   ├── app/                  # Next.js App Router
│   │   ├── (auth)/           # Страницы аутентификации
│   │   ├── (dashboard)/      # Основной интерфейс
│   │   │   ├── browse/       # Поиск и каталог
│   │   │   ├── watch/        # Страница просмотра
│   │   │   └── library/      # Библиотека пользователя
│   │   └── api/              # API routes (если нужно)
│   ├── components/           # React компоненты
│   │   ├── player/           # Плеер и контролы
│   │   ├── ui/               # Базовые компоненты
│   │   └── media/            # Карточки медиа
│   ├── lib/                  # Утилиты и конфиги
│   │   ├── api/              # Клиенты API
│   │   ├── db/               # Frontend база (indexedDB)
│   │   └── utils/            # Вспомогательные функции
│   ├── hooks/                # React хуки
│   ├── styles/               # Tailwind/SCSS
│   └── types/                # TypeScript типы
└── docker-compose.yml        # Докеризация

4. Функциональные требования
4.1. Поиск и каталог

    Поиск по названию с автодополнением

    Фильтры: жанр, год, рейтинг, тип (фильм/сериал/аниме)

    Категории: популярное, новинки, рекомендованное

    Интеграция с TMDB и Shikimori для метаданных

    Кеширование результатов поиска

4.2. Агрегация источников

    Поддержка типов источников:

        Торренты (magnet-ссылки, .torrent файлы)

        IFrame-вставки (сторонние плееры)

        HLS/DASH потоки

        Прямые ссылки на видеофайлы

    Параллельный поиск по всем источникам

    Интеллектуальный выбор лучшего источника

    Автоматическая проверка доступности источников

4.3. Универсальный плеер

    Поддержка всех типов источников

    Адаптивное качество (переключение 480p-4K)

    Субтитры: загрузка, выбор, синхронизация

    Управление: скорость, аудиодорожки, цветокоррекция

    Прогресс: автосохранение, продолжение с места

    WebTorrent интеграция для торрент-стриминга

4.4. Пользовательская система

    Регистрация/авторизация (JWT + OAuth опционально)

    Профиль с настройками просмотра

    История просмотра с синхронизацией

    Закладки и плейлисты

    Персонализация на основе поведения

4.5. Администрирование

    Панель управления источниками

    Статистика использования

    Мониторинг доступности источников

    Логирование действий пользователей

5. Технические требования
5.1. Бэкенд (Python)
yaml

Технологии:
  - Python 3.11+
  - FastAPI (веб-фреймворк)
  - SQLAlchemy 2.0 (ORM)
  - Alembic (миграции)
  - Pydantic (валидация)
  - Redis (кеширование)
  - Celery (фоновые задачи, опционально)

Библиотеки для парсинга:
  - aiohttp/httpx (HTTP клиенты)
  - BeautifulSoup4 (парсинг HTML)
  - lxml (XML парсинг)
  - selenium/playwright (для JS-сайтов)

Библиотеки для торрентов:
  - libtorrent (python-libtorrent)
  - bencode.py (парсинг .torrent)

API интеграции:
  - TMDB API (фильмы/сериалы)
  - Shikimori API (аниме)
  - OpenSubtitles API (субтитры)

5.2. Фронтенд (Next.js)
yaml

Технологии:
  - Next.js 14+ (App Router)
  - TypeScript 5+
  - React 18+ (хуки, Suspense)
  - Tailwind CSS (стилизация)
  - Zustand/Redux Toolkit (стейт-менеджмент)
  - React Query/TanStack Query (кеширование API)

Библиотеки для плеера:
  - video.js (основа плеера)
  - webtorrent (торрент-стриминг)
  - hls.js (HLS потоки)
  - dash.js (DASH потоки)

UI библиотеки:
  - shadcn/ui (компоненты)
  - lucide-react (иконки)
  - framer-motion (анимации)

Оптимизация:
  - SWR (stale-while-revalidate)
  - PWA (Progressive Web App)
  - Service Workers (оффлайн режим)

5.3. База данных
sql

Основная БД: SQLite (начально) → PostgreSQL (при росте)
Кеш: Redis
Схема: См. раздел "Структура базы данных"

Требования к хранению:
  - Все внешние ID (TMDB, Shikimori, IMDB)
  - Метаданные контента
  - Источники видео с тех. характеристиками
  - Торрент-метаданные
  - История и настройки пользователей
  - Кеш поиска и API запросов

6. Структура базы данных (основные таблицы)
6.1. Основные сущности
sql

1. users                    # Пользователи
2. media_items              # Медиа-объекты (фильмы/сериалы/аниме)
3. episodes                 # Эпизоды (для сериалов)
4. video_sources           # Источники видео
5. torrents_info           # Торрент-метаданные
6. watch_history           # История просмотра
7. source_preferences      # Предпочтения источников
8. search_cache            # Кеш поиска
9. genres & media_genres   # Жанры
10. playlists              # Плейлисты пользователей

6.2. Ключевые индексы
sql

-- Для быстрого поиска медиа
CREATE INDEX idx_media_search ON media_items(title, year, media_type);

-- Для поиска источников
CREATE INDEX idx_sources_lookup ON video_sources(media_id, episode_id, quality, is_active);

-- Для истории просмотра
CREATE INDEX idx_user_history ON watch_history(user_id, last_played DESC);

-- Для торрентов
CREATE INDEX idx_torrent_stats ON torrents_info(seeders DESC, last_updated);

7. API спецификация (основные эндпоинты)
7.1. Аутентификация
http

POST   /api/v1/auth/register     # Регистрация
POST   /api/v1/auth/login        # Вход
POST   /api/v1/auth/refresh      # Обновление токена
GET    /api/v1/auth/profile      # Профиль пользователя

7.2. Медиа-поиск
http

GET    /api/v1/media/search      # Поиск по запросу
GET    /api/v1/media/{id}        # Детали медиа
GET    /api/v1/media/{id}/sources # Все источники
GET    /api/v1/media/popular     # Популярное
GET    /api/v1/media/trending    # Тренды

7.3. Источники и плеер
http

POST   /api/v1/player/prepare    # Подготовка источника
GET    /api/v1/player/stream     # Потоковое видео (прокси)
GET    /api/v1/player/subtitles  # Субтитры
POST   /api/v1/player/progress   # Сохранение прогресса

7.4. Пользовательские данные
http

GET    /api/v1/user/history      # История просмотра
GET    /api/v1/user/watchlist    # Закладки
POST   /api/v1/user/preferences  # Настройки
GET    /api/v1/user/playlists    # Плейлисты

7.5. Администрирование
http

GET    /api/v1/admin/sources     # Управление источниками
POST   /api/v1/admin/scan        # Запуск сканирования
GET    /api/v1/admin/stats       # Статистика

8. Процесс агрегации источников
8.1. Алгоритм поиска
python

1. Получаем метаданные из TMDB/Shikimori
2. Генерируем поисковые запросы:
   - Оригинальное название + год
   - Локализованное название
   - IMDB/Shikimori ID
3. Параллельный поиск по источникам:
   - Торрент-трекеры (Rutracker, Nyaa, RARBG)
   - Стриминговые сайты
   - Публичные API агрегаторов
4. Валидация и оценка источников
5. Сохранение в базу с приоритетами

8.2. Критерии оценки источников
python

score = (
    quality_score * 0.3 +      # 1080p > 720p > 480p
    speed_score * 0.25 +       # Скорость загрузки
    availability_score * 0.2 + # Процент доступности
    subtitle_score * 0.15 +    # Наличие субтитров
    audio_score * 0.1          # Аудиодорожки
)

9. Компонент плеера
9.1. Архитектура плеера
typescript

interface UniversalPlayerProps {
  sources: VideoSource[];      // Все доступные источники
  mediaId: number;            // ID медиа
  episodeId?: number;         // ID эпизода (для сериалов)
  autoplay?: boolean;         // Автовоспроизведение
  startTime?: number;         // Время начала (для продолжения)
}

// Основные компоненты:
// 1. SourceSelector - выбор источника и качества
// 2. VideoPlayer - основной видео-плеер
// 3. SubtitleManager - управление субтитрами
// 4. ProgressTracker - отслеживание прогресса
// 5. QualitySwitcher - переключение качества

9.2. Поддержка типов источников
typescript

type VideoSource = {
  type: 'torrent' | 'hls' | 'dash' | 'iframe' | 'direct';
  url: string;
  quality: string;
  codec: string;
  subtitles?: SubtitleTrack[];
  headers?: Record<string, string>; // Для CORS/proxy
};

// Рендер в зависимости от типа:
const renderPlayer = (source: VideoSource) => {
  switch (source.type) {
    case 'torrent':
      return <WebTorrentPlayer magnet={source.url} />;
    case 'hls':
      return <HLSPlayer src={source.url} />;
    case 'iframe':
      return <IFramePlayer src={source.url} headers={source.headers} />;
    default:
      return <VideoJS src={source.url} />;
  }
};

10. Безопасность и производительность
10.1. Меры безопасности

    JWT токены с коротким временем жизни

    HTTPS обязательно в production

    CORS политики для фронтенда

    Rate limiting на API эндпоинты

    SQL injection protection через ORM

    XSS protection на фронтенде

10.2. Оптимизации производительности

    Redis кеш для частых запросов

    CDN для статических ресурсов

    Ленивая загрузка компонентов

    Виртуализация списков для больших каталогов

    Compression для API ответов

    Connection pooling для БД

10.3. Мониторинг

    Логирование всех API запросов

    Метрики производительности

    Health checks для всех сервисов

    Alerting при проблемах с источниками

11. План разработки (MVP)
Фаза 1: Базовый функционал (4-6 недель)

    Настройка проекта (бэкенд + фронтенд)

    Базовая аутентификация

    Интеграция с TMDB API

    Простой поиск медиа

    Базовый плеер (Video.js)

Фаза 2: Агрегация источников (4-6 недель)

    Система парсинга источников

    Торрент-интеграция (WebTorrent)

    Выбор качества и источника

    Сохранение прогресса просмотра

Фаза 3: Пользовательский опыт (4 недели)

    История просмотра

    Закладки и плейлисты

    Персонализация

    Рекомендации

Фаза 4: Оптимизация и масштабирование (2-3 недели)

    Кеширование

    Производительность

    PWA функционал

    Документация

12. Развертывание
12.1. Локальная разработка
bash

# Клонирование репозитория
git clone <repo-url>
cd personal-media-aggregator

# Установка зависимостей
cd backend && pip install -r requirements.txt
cd ../frontend && npm install

# Запуск
docker-compose up -d redis  # Redis для кеша
python backend/app/main.py  # Бэкенд
npm run dev                 # Фронтенд

12.2. Production развертывание
yaml

# docker-compose.prod.yml
version: '3.8'
services:
  backend:
    build: ./backend
    environment:
      - DATABASE_URL=postgresql://...
      - REDIS_URL=redis://redis:6379
    depends_on:
      - postgres
      - redis
  
  frontend:
    build: ./frontend
    environment:
      - NEXT_PUBLIC_API_URL=https://api.yourdomain.com
  
  postgres:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data
  
  redis:
    image: redis:7-alpine
  
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"

13. Тестирование
13.1. Типы тестов

    Unit тесты для бизнес-логики

    Интеграционные тесты для API

    E2E тесты для критических путей

    Нагрузочное тестирование для агрегатора

13.2. Инструменты
yaml

Backend:
  - pytest (unit тесты)
  - pytest-asyncio (асинхронные тесты)
  - httpx (тестирование API)
  - factory_boy (фабрики данных)

Frontend:
  - Jest + React Testing Library
  - Cypress (E2E тесты)
  - MSW (mock API)

14. Документация
14.1. Обязательная документация

    README с инструкцией по установке

    API документация (Swagger/OpenAPI)

    Архитектурные решения (ADR)

    Конфигурационные параметры

    Скрипты развертывания

14.2. Генерация документации
yaml

Backend:
  - FastAPI auto-generated docs (/docs, /redoc)
  - Sphinx для дополнительной документации

Frontend:
  - Storybook для компонентов
  - TypeDoc для TypeScript

15. Примечания и ограничения
15.1. Юридические аспекты

    Проект предназначен только для личного использования

    Не распространять и не коммерциализировать

    Ответственность за использование лежит на пользователе

    Рекомендуется использовать через VPN

15.2. Технические ограничения

    Производительность зависит от доступности источников

    Некоторые источники могут блокировать парсинг

    Торрент-стриминг требует хорошего интернет-соединения

    SQLite подходит для начала, но PostgreSQL рекомендуется для production

15.3. Будущие улучшения

    Поддержка большего количества источников

    Расширенная аналитика просмотров

    Мобильные приложения (React Native)

    Оффлайн-режим с предзагрузкой

    Совместные просмотры (watch parties)

Версия документа: 1.0
