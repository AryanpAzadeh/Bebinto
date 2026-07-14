<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## API Endpoints

Base paths:
- `GET /api/v1/*` for v1 endpoints
- `POST /api/chat` legacy chat endpoint (same payload/response as `/api/v1/chat`)

### GET /api/v1/movies/new
Returns the newest movies (paginated).
- Query params: `page` (optional)
- Sample response:
```json
{
  "data": [
    {
      "id": 31801,
      "title": "Hidden Blade",
      "type": "movie",
      "year": 2024,
      "imdb": 7.2,
      "image": "https://example.com/poster.jpg",
      "cover": "https://example.com/cover.jpg"
    }
  ],
  "links": { "first": "...", "last": "...", "prev": null, "next": "..." },
  "meta": { "current_page": 1, "per_page": 20, "total": 120 }
}
```

### GET /api/v1/movies/top-rated
Returns top-rated movies (paginated).
- Query params: `page` (optional)
- Sample response: same shape as `/api/v1/movies/new`

### GET /api/v1/series/new
Returns the newest series (paginated).
- Query params: `page` (optional)
- Sample response: same shape as `/api/v1/movies/new`

### GET /api/v1/series/top-rated
Returns top-rated series (paginated).
- Query params: `page` (optional)
- Sample response: same shape as `/api/v1/movies/new`

### GET /api/v1/series/updated
Returns recently updated series (paginated).
- Query params: `page` (optional)
- Sample response: same shape as `/api/v1/movies/new`

### GET /api/v1/series/best
Returns best series by internal/imdb rating (paginated).
- Query params: `page` (optional)
- Sample response: same shape as `/api/v1/movies/new`

### GET /api/v1/details
Returns a single poster (movie or series).
- Query params: `id` (required, poster api_id), `type` (required, `movie` or `series`)
- Sample response:
```json
{
  "data": {
    "id": 31801,
    "title": "Hidden Blade",
    "type": "movie",
    "year": 2024,
    "imdb": 7.2,
    "image": "https://example.com/poster.jpg",
    "cover": "https://example.com/cover.jpg",
    "description": "Sample description",
    "rating": 4.5,
    "duration": "132 min",
    "classification": "PG-13",
    "comment": true,
    "ai_summary": null,
    "fun_facts": [],
    "country": [{ "title": "Iran" }],
    "genres": [{ "title": "Action" }],
    "sources": [
      {
        "id": 55123,
        "quality": "1080",
        "type": "mkv",
        "url": "https://example.com/movie-1080.mkv"
      }
    ],
    "seasons": []
  }
}
```

### GET /api/v1/seasons/{poster}
Returns seasons for a series. The `{poster}` route param is the poster `api_id`.
- Sample response:
```json
{
  "data": [
    {
      "id": 1,
      "title": "Season One",
      "episodes": [
        {
          "id": 1,
          "title": "Episode 1",
          "description": "Episode description",
          "duration": "45 min",
          "sources": [
            { "id": 1, "quality": "720", "type": "mkv", "url": "https://example.com/episode-1-720.mkv" }
          ]
        }
      ]
    }
  ]
}
```

### GET /api/v1/search
Search posters by title, description, genres, or countries.
- Query params: `q` (required)
- Sample response:
```json
{
  "channels": [],
  "posters": [
    {
      "id": 31801,
      "title": "Hidden Blade",
      "type": "movie",
      "year": 2024,
      "imdb": 7.2,
      "image": "https://example.com/poster.jpg",
      "cover": "https://example.com/cover.jpg"
    }
  ]
}
```

### POST /api/v1/chat
Chat suggestions based on a user message.
- Body:
```json
{ "message": "I want action movies from 2024" }
```
- Sample response:
```json
{
  "sender": "bot",
  "text": "These could be good choices:",
  "results": [
    {
      "id": 31801,
      "title": "Hidden Blade",
      "type": "movie",
      "year": 2024,
      "rating": 7.2,
      "image": "https://example.com/poster.jpg",
      "countries": [{ "title": "Iran" }],
      "playlists": [
        { "name": "Best 2024 Movies", "slug": "best-2024-movies" }
      ],
      "fun_facts": []
    }
  ],
  "playlists": [
    { "id": 1, "name": "Best 2024 Movies", "slug": "best-2024-movies", "posters_count": 12 }
  ]
}
```

### POST /api/chat
Legacy chat endpoint.
- Body and response: same as `/api/v1/chat`

### GET /api/v1/playlists
Returns playlists with their posters (paginated).
- Query params: `page` (optional)
- Sample response:
```json
{
  "data": [
    {
      "id": 1,
      "name": "Sci Fi Picks",
      "slug": "sci-fi-picks",
      "posters": [
        {
          "id": 31801,
          "title": "Hidden Blade",
          "type": "movie",
          "year": 2024,
          "imdb": 7.2,
          "image": "https://example.com/poster.jpg",
          "cover": "https://example.com/cover.jpg"
        }
      ]
    }
  ],
  "links": { "first": "...", "last": "...", "prev": null, "next": "..." },
  "meta": { "current_page": 1, "per_page": 20, "total": 12 }
}
```

### GET /api/v1/playlists/{playlist}
Returns a single playlist by `slug`, including its posters.
- Sample response:
```json
{
  "data": {
    "id": 1,
    "name": "Sci Fi Picks",
    "slug": "sci-fi-picks",
    "description": "<p>description</p>",
    "posters": [
      {
        "id": 31801,
        "title": "Hidden Blade",
        "type": "movie",
        "year": 2024,
        "imdb": 7.2,
        "image": "https://example.com/poster.jpg",
        "cover": "https://example.com/cover.jpg"
      }
    ]
  }
}
```

### POST /api/v1/playlists
Create a playlist.
- Body:
```json
{
  "name": "Sci Fi Picks",
  "slug": "sci-fi-picks",
  "poster_ids": [31801, 40001]
}
```
- Sample response (201 Created):
```json
{
  "data": {
    "id": 1,
    "name": "Sci Fi Picks",
    "slug": "sci-fi-picks",
    "posters": [
      {
        "id": 31801,
        "title": "Hidden Blade",
        "type": "movie",
        "year": 2024,
        "imdb": 7.2,
        "image": "https://example.com/poster.jpg",
        "cover": "https://example.com/cover.jpg"
      }
    ]
  }
}
```

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework. You can also check out [Laravel Learn](https://laravel.com/learn), where you will be guided through building a modern Laravel application.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains thousands of video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the [Laravel Partners program](https://partners.laravel.com).

### Premium Partners

- **[Vehikl](https://vehikl.com)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel)**
- **[DevSquad](https://devsquad.com/hire-laravel-developers)**
- **[Redberry](https://redberry.international/laravel-development)**
- **[Active Logic](https://activelogic.com)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
