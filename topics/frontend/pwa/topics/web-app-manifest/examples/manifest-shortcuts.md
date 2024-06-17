# Examples of `shortcuts` member in web manifest

### Example 1

**Источник**: <https://github.com/siyuan-note/siyuan/blob/cfec6bc600894e2b99a3f07310a2a4b65390e335/app/stage/manifest.webmanifest#L30-L55>

```JSON
{
  "shortcuts": [
      {
          "name": "SiYuan Desktop",
          "description": "Desktop web side for SiYuan",
          "url": "/stage/build/desktop/",
          "icons": [
              {
                  "src": "favicon.ico",
                  "type": "image/png",
                  "sizes": "512x512"
              }
          ]
      },
      {
          "name": "SiYuan Mobile",
          "description": "Mobile web side for SiYuan",
          "url": "/stage/build/mobile/",
          "icons": [
              {
                  "src": "favicon.ico",
                  "type": "image/png",
                  "sizes": "512x512"
              }
          ]
      }
  ],
}
```

### Example 2

**Источник**: <https://github.com/OpenArCloud/sparcl/blob/2d6b7a345be74ae42a42997fcf3ca1c8c2df3326/public/sparcl.webmanifest#L69C3-L88C6>

```JSON
{
  "shortcuts": [
    {
      "name": "Open Dashboard",
      "short_name": "Dashboard",
      "description": "View the dashboard for internal state and settings",
      "url": "/?dashboard"
    },
    {
      "name": "Use Creation Mode",
      "short_name": "Creation Mode",
      "description": "Use content from server on local network",
      "url": "/?create"
    },
    {
      "name": "Use Development Mode",
      "short_name": "Development",
      "description": "Use content record stored locally",
      "url": "/?develop"
    }
  ]
}
```

### Example 3

**Источник**: <https://github.com/devrev-morocco/devrev-morocco/blob/3c76b5c1798c44b467cb7f943278f3403ace36e3/public/manifest.webmanifest#L35-L44>

```JSON
{
  "shortcuts": [{
    "name": "DevRev season 1",
    "url": "playlist/1/devrev-1",
    "icons": [{
        "src": "/static/favicons/favicon-192x192.png",
        "sizes": "192x192",
        "type": "image/png"
    }],
    "description": "A weekly live show featuring conversations with great tech minds"
  }]
}
```
