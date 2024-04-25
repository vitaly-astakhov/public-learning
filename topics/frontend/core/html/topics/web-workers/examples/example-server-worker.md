# Examples of `navigation.serverWorker` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)
- [ServiceWorkerProvider [github.com]](https://github.com/ProtonMail/WebClients/blob/d1a23fc2c4ab1e1632118baaee6f2531022ae4cf/applications/pass/src/app/ServiceWorker/ServiceWorkerProvider.tsx)

## Example 1

**Источник**: <https://github.com/tldraw/tldraw/blob/8151e6f586149e4447149d25bd70868a5a4e8838/apps/dotcom/src/main.tsx#L21-L31>

```TypeScript
try {
  // we have a dummy service worker that unregisters itself immediately
  // this was needed to remove the service worker we used to have from the cache
  // we can remove this if we ever need a service worker again, or if enough time passes that
  // anybody returning to tldraw.com should not have a service worker running
  navigator.serviceWorker.register('/sw.js', {
  scope: '/',
  })
} catch (e) {
  // ignore
}

```

## Example 2

**Источник**: <https://github.com/ApolloAuto/apollo/blob/6932e80ec1fcabfeef5a563001b521de2770c7d0/modules/dreamview_plus/frontend/packages/dreamview-web/src/Root.tsx#L9-L23>

```TypeScript

useLayoutEffect(() => {
    if (process.env.NODE_ENV === 'production') {
        logger.info('dreamview-web init');
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker
                .register('/service-worker.js')
                .then((registration) => {
                    logger.info('Dreamview service Worker registered with scope:', registration.scope);
                })
                .catch((error) => {
                    logger.error('Dreamview service Worker registration failed:', error);
                });
        }
    }
}, []);

```

## Example 3

**Источник**: <https://github.com/ProtonMail/WebClients/blob/d1a23fc2c4ab1e1632118baaee6f2531022ae4cf/applications/mail/src/app/MainContainer.tsx#L41-L66>

```TypeScript

// Service Worker registration
// Including a kill switch with a feature flag
useEffect(() => {
    if ('serviceWorker' in navigator && !loadingSw) {
        const unregister = async () => {
            const registrations = await navigator.serviceWorker.getRegistrations();
            registrations.forEach((registration) => {
                if (registration.scope === window.location.origin + '/') {
                    void registration.unregister();
                }
            });
        };

        const register = async () => {
            try {
                await navigator.serviceWorker.register('/service-worker.js');
            } catch {
                console.log('No service worker found');
            }
        };

        const action = featureSw?.Value === true ? register : unregister;

        void action();
    }
}, [featureSw, loadingSw]);

```

## Example 4

**Источник**: <https://github.com/ProtonMail/WebClients/blob/d1a23fc2c4ab1e1632118baaee6f2531022ae4cf/applications/drive/src/app/store/_downloads/fileSaver/download.ts#L31-L51>

```TypeScript
async function wakeUpServiceWorker() {
    const worker = navigator.serviceWorker.controller;


    if (worker) {
        worker.postMessage({ action: 'ping' });
    } else {
        const url = [
            document.location.href.substring(0, document.location.href.indexOf('/')),
            stripLeadingAndTrailingSlash(PUBLIC_PATH),
            'sw/ping',
        ]
            .filter(Boolean)
            .join('/');
        const res = await fetch(url);
        const body = await res.text();
        if (!res.ok || body !== 'pong') {
            throw new Error('Download worker is dead');
        }
    }
    return worker as ServiceWorker;
}
```

## Example 5

**Источник**: <https://github.com/cs01/termpair/blob/543d84af21e2892a8b6f177d1c397b88973b0e98/termpair/frontend_src/src/serviceWorker.ts#L57-L99>

```TypeScript

function registerValidSW(swUrl: any, config: any) {
  navigator.serviceWorker
    .register(swUrl)
    .then(registration => {
      registration.onupdatefound = () => {
        const installingWorker = registration.installing;
        if (installingWorker == null) {
          return;
        }
        installingWorker.onstatechange = () => {
          if (installingWorker.state === 'installed') {
            if (navigator.serviceWorker.controller) {
              // At this point, the updated precached content has been fetched,
              // but the previous service worker will still serve the older
              // content until all client tabs are closed.
              console.log(
                'New content is available and will be used when all ' +
                  'tabs for this page are closed. See https://bit.ly/CRA-PWA.'
              );

              // Execute callback
              if (config && config.onUpdate) {
                config.onUpdate(registration);
              }
            } else {
              // At this point, everything has been precached.
              // It's the perfect time to display a
              // "Content is cached for offline use." message.
              console.log('Content is cached for offline use.');

              // Execute callback
              if (config && config.onSuccess) {
                config.onSuccess(registration);
              }
            }
          }
        };
      };
    })
    .catch(error => {
      console.error('Error during service worker registration:', error);
    });
}

```

## Example 6

**Источник**: <https://github.com/heyxyz/hey/blob/b3cd8de476025fa1259cd6f2577ee6aabcf1f5ec/apps/web/src/lib/pushToImpressions.ts#L21-L27>

```TypeScript
if (IS_MAINNET && id && navigator.serviceWorker?.controller) {
  navigator.serviceWorker.controller.postMessage({
    id,
    type: 'PUBLICATION_VISIBLE',
    viewerId: sessionProfileId || anonymousId
  });
}

```

## Example 7

**Источник**: <https://github.com/outline/outline/blob/bf848f3a2f7d7577b7e33a2b6b15580a331320b6/app/index.tsx#L103-L128>

```TypeScript

if ("serviceWorker" in navigator && env.ENVIRONMENT !== "development") {
  window.addEventListener("load", () => {
    // see: https://bugs.chromium.org/p/chromium/issues/detail?id=1097616
    // In some rare (<0.1% of cases) this call can return `undefined`
    const maybePromise = navigator.serviceWorker.register("/static/sw.js", {
      scope: "/",
    });


    if (maybePromise?.then) {
      maybePromise
        .then((registration) => {
          Logger.debug(
            "lifecycle",
            "[ServiceWorker] Registered.",
            registration
          );
        })
        .catch((registrationError) => {
          Logger.debug(
            "lifecycle",
            "[ServiceWorker] Registration failed.",
            registrationError
          );
        });
    }
  });

```
