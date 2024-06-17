# Examples of prefers-color-scheme in web manifest

### Example 1

**Источник**: <https://github.com/tomayac/SVGcode/blob/92f837660a556ef169a2f86dccf1973f040dd9d6/src/manifest.json#L52-L57>

```JSON
{
  "theme_colors": [
    { "color": "#131313", "media": "(prefers-color-scheme: dark)" }
  ],
  "background_colors": [
    { "color": "#131313", "media": "(prefers-color-scheme: dark)" }
  ],
}
```

### Example 2

**Источник**: <https://github.com/Valmerax/portfolio/blob/603272ef5bfaa14ef004a4da9504f26d282d6763/public/site.webmanifest#L5-L36>

```JSON
{
  "icons": [
      {
          "media": "(prefers-color-scheme: no-preference)",
          "src": "{{ asset('images/favicons/android-chrome-light-192x192.png') }}",
          "sizes": "192x192"
      },
      {
          "media": "(prefers-color-scheme: no-preference)",
          "src": "{{ asset('images/favicons/android-chrome-light-512x512.png') }}",
          "sizes": "512x512"
      },
      {
          "media": "(prefers-color-scheme: light)",
          "src": "{{ asset('images/favicons/android-chrome-light-192x192.png') }}",
          "sizes": "192x192"
      },
      {
          "media": "(prefers-color-scheme: light)",
          "src": "{{ asset('images/favicons/android-chrome-light-512x512.png') }}",
          "sizes": "512x512"
      },
      {
          "media": "(prefers-color-scheme: dark)",
          "src": "{{ asset('images/favicons/android-chrome-dark-192x192.png') }}",
          "sizes": "192x192"
      },
      {
          "media": "(prefers-color-scheme: dark)",
          "src": "{{ asset('images/favicons/android-chrome-dark-512x512.png') }}",
          "sizes": "512x512"
      }
  ],
}
```

### Example 3

**Источник**: <https://github.com/ilvits/expressJS--weather-app/blob/4f84b4f895e929444f81502330d0f35c3ae3bac5/public/manifest.json#L34-L42>

```JSON
{
  "theme_colors": [
    {
      "color": "#F3F4F7"
    },
    {
      "color": "#131E32",
      "media": "(prefers-color-scheme: dark)"
    }
  ],
}
```

### Example 4

**Источник**: <https://github.com/revcheg/revoPLAYER/blob/54296e2aa58aeb44697d1fe4bc3e6eb107ca3832/source/player.webmanifest#L8-L41>

```JSON
{
  "icons": [
    {
      "src": "img/favicons/favicon.svg",
      "sizes": "any",
      "type": "image/svg+xml"
    },
    {
      "src": "img/favicons/favicon.svg",
      "sizes": "any",
      "media": "(prefers-color-scheme: light)",
      "type": "image/svg+xml"
    },
    {
      "src": "img/favicons/favicon-dark.svg",
      "sizes": "any",
      "media": "(prefers-color-scheme: dark)",
      "type": "image/svg+xml"
    },
    {
      "src": "img/favicons/maskable-icon.svg",
      "sizes": "any",
      "type": "image/svg+xml",
      "purpose": "maskable"
    },
    {
      "src": "img/favicons/android-chrome-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "img/favicons/android-chrome-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

### Example 5

**Источник**: <https://github.com/terratensor/feed-svodd-app/blob/101eda0d82c72ab745b61157a180a933980bd182/src/app/manifest.webmanifest#L16-L27>

```JSON
{
  "color_overrides": [
    {
      "media": "(prefers-color-scheme: dark)",
      "theme_color": "#bfc3c3",
      "background_color": "#1c1c1e"
    },
    {
      "media": "(prefers-color-scheme: light)",
      "theme_color": "#212529",
      "background_color": "#f9f8f6"
    }
  ],
}
```
