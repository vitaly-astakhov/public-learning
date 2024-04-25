# Examples of `SharedWorker` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)
- [Shared state using a shared worker [HTML spec]](https://html.spec.whatwg.org/multipage/workers.html#shared-state-using-a-shared-worker)

## Example 1

**Источник**: <https://github.com/civitai/civitai/blob/de960ca7e2572186ca594293f854531d8c0be2e5/src/components/CivitaiLink/CivitaiLinkProvider.tsx#L152-L213>

```TypeScript

const workerRef = useRef<SharedWorker>();
const workerPromise = useRef<Promise<SharedWorker>>();

const getWorker = () => {
  if (workerPromise.current) return workerPromise.current;
  if (workerRef.current) return Promise.resolve(workerRef.current);
  const worker = new SharedWorker(
    new URL('/src/workers/civitai-link.worker.ts', import.meta.url),
    { name: 'civitai-link' }
  );

  // ...
  // Some code
  // ...

  workerPromise.current = new Promise<SharedWorker>((resolve) => {
    const handleReady = () => {
      workerRef.current = worker;
      resolve(worker);
    };

    worker.port.onmessage = async function ({ data }: { data: WorkerOutgoingMessage }) {
      if (data.type === 'ready') handleReady();
      else if (data.type === 'error') handleError(data.msg);
      else if (data.type === 'message') handleMessage(data.msg);
      else if (data.type === 'instance') handleInstance(data.payload);
      else if (data.type === 'instancesUpdate') setInstances(data.payload);
      else if (data.type === 'resourcesUpdate') setResources(data.payload);
      else if (data.type === 'activitiesUpdate') handleActivities(data.payload);
      else if (data.type === 'commandComplete') handleCommandComplete(data.payload);
      else if (data.type === 'socketConnection') setSocketConnected(data.payload);
    };
  });

  return workerPromise.current;
};


```

## Example 2

**Источник**: <https://github.com/trezor/trezor-suite/blob/c376a54f3952a9f8e2d7b930fb45a0c5e1b1f60b/packages/connect-popup/src/log.tsx#L99-L141>

```TypeScript
const useLogWorker = (setLogs: React.Dispatch<React.SetStateAction<any[]>>) => {
    let logWorker: SharedWorker | undefined;

    try {
        logWorker = new SharedWorker('./workers/shared-logger-worker.js');
    } catch (error) {
        console.warn('Failed to initialize SharedWorker');
    }

    useEffect(() => {
        if (!logWorker) {
            console.warn('SharedWorker is not initialized');
        } else {
            logWorker.port.onmessage = function (event) {
                const { data } = event;
                switch (data.type) {
                    case 'get-logs':
                        logInConsole(data.payload);
                        setLogs(data.payload);
                        break;
                    case 'log-entry':
                        logInConsole([data.payload]);
                        setLogs(prevLogs => {
                            if (prevLogs.length > MAX_ENTRIES) {
                                prevLogs.shift();
                            }

                            return [...prevLogs, data.payload];
                        });
                        break;
                    default:
                }
            };

            logWorker.port.postMessage({ type: 'get-logs' });
            logWorker.port.postMessage({ type: 'subscribe' });
        }

        // eslint-disable-next-line react-hooks/exhaustive-deps
    }, []);

    return logWorker;
};


```

## Example 3

**Источник**: <https://github.com/craftercms/studio-ui/blob/feb81efbf45f7a21eeaaf5aa5337ee40efecc4c8/ui/app/src/state/store.ts#L124-L161>

```TypeScript
function registerSharedWorker(): Observable<ObtainAuthTokenResponse & { worker: SharedWorker }> {
  if ('SharedWorker' in window) {
    const worker = new SharedWorker(`${process.env.PUBLIC_URL}/shared-worker.js`, {
      name: SHARED_WORKER_NAME,
      credentials: 'same-origin'
    });
    worker.port.start();
    worker.port.postMessage(sharedWorkerConnect({ xsrfToken: getXSRFToken() }));
    window.addEventListener('beforeunload', function () {
      worker.port.postMessage(sharedWorkerDisconnect());
    });
    return fromEvent<MessageEvent>(worker.port, 'message').pipe(
      tap((e) => {
        if (e.data?.type === sharedWorkerUnauthenticated.type) {
          const elem = document.createElement('div');
          elem.style.textAlign = 'center';
          elem.style.margin = '20px 0';
          elem.innerHTML = 'User not authenticated.';
          setTimeout(() => {
            window.location.reload();
          }, 800);
          throw new Error('User not authenticated.');
        }
      }),
      filter((e) => e.data?.type === sharedWorkerToken.type),
      take(1),
      map((e) => ({ ...e?.data?.payload, worker }))
    );
  } else {
    return new Observable((observer) => {
      observer.error(
        ['iPad Simulator', 'iPhone Simulator', 'iPod Simulator', 'iPad', 'iPhone', 'iPod'].includes(navigator.platform)
          ? 'iOS is not supported as it lacks essential features. Please use Chrome or Firefox browsers on your desktop.'
          : 'Your browser is not supported as it lacks essential features. Please use Chrome or Firefox.'
      );
    });
  }
}


```

## Example 4

**Источник**: <https://github.com/facebook/sapling/blob/8c7a691727e180945e6e5758560bbf885dae76b3/eden/contrib/reviewstack/src/diffServiceClient.ts#L107-L157>

```TypeScript
/**
 * Client that is paired with an instance of `diffServiceWorker`. Takes
 * responsibility for pairing requests and responses to the Web Worker, making
 * the result available as a Promise to the caller.
 */
class DiffServiceClient {
  private worker: SharedWorker;
  private pendingRequests: Map<number, (result: Result) => void> = new Map();


  constructor(workerName: string) {
    this.worker = new SharedWorker(new URL('./diffServiceWorker.ts', import.meta.url), {
      name: workerName,
    });
    this.worker.port.onmessage = event => this.onmessage(event);
    // eslint-disable-next-line no-console
    this.worker.port.onmessageerror = event => console.error(event);
  }


  private onmessage({data}: {data: Response}) {
    const {id, ok, err} = data;
    const handler = this.pendingRequests.get(id);
    if (handler == null) {
      // eslint-disable-next-line no-console
      console.error(`no handler found for ${id}: multiple responses sent?`);
      return;
    }


    this.pendingRequests.delete(id);
    handler({ok, err});
  }


  private once(id: number, onresponse: (response: Result) => void) {
    this.pendingRequests.set(id, onresponse);
  }


  sendMessage(message: Message): Promise<unknown> {
    const {id} = message;
    const promise = new Promise((resolve, reject) => {
      this.once(id, (result: Result) => {
        const {ok, err} = result;
        if (err != null) {
          reject(err);
        } else {
          resolve(ok);
        }
      });
    });
    this.worker.port.postMessage(message);
    return promise;
  }
}

```

## Example 5

**Источник**: <https://github.com/curdinc/skylar-email/blob/fc2a92db15de2f323cdc03773cf8ca78afc4ee05/packages/web-worker-logic/src/basic-client/gmail-api-worker.ts#L9-L24>

```TypeScript
export const gmailApiWorker = createTRPCClient<GmailWorkerRouterType>({
  transformer: superjson,
  links: [
    loggerLinkConfig,
    workerLink({
      createWorker: () => {
        return new SharedWorker(
          new URL("../gmail-api/worker.ts", import.meta.url),
          {
            name: "gmail-api-worker",
          },
        );
      },
    }),
  ],
});
```

## Example 6

**Источник**: <https://github.com/powersync-ja/powersync-js/blob/405add3251fca01dac34e4a97fb38ddaaf44ae14/packages/web/src/worker/db/open-worker-database.ts#L1-L33>

```TypeScript
import * as Comlink from 'comlink';
import { OpenDB } from './open-db';


/**
 * Opens a shared or dedicated worker which exposes opening of database connections
 */
export function openWorkerDatabasePort(workerIdentifier: string, multipleTabs = true) {
  /**
   *  Webpack V5 can bundle the worker automatically if the full Worker constructor syntax is used
   *  https://webpack.js.org/guides/web-workers/
   *  This enables multi tab support by default, but falls back if SharedWorker is not available
   *  (in the case of Android)
   */
  return multipleTabs
    ? new SharedWorker(new URL('./SharedWASQLiteDB.worker.js', import.meta.url), {
        /* @vite-ignore */
        name: `shared-DB-worker-${workerIdentifier}`,
        type: 'module'
      }).port
    : new Worker(new URL('./WASQLiteDB.worker.js', import.meta.url), {
        /* @vite-ignore */
        name: `DB-worker-${workerIdentifier}`,
        type: 'module'
      });
}


/**
 * @returns A function which allows for opening database connections inside
 * a worker.
 */
export function getWorkerDatabaseOpener(workerIdentifier: string, multipleTabs = true) {
  return Comlink.wrap<OpenDB>(openWorkerDatabasePort(workerIdentifier, multipleTabs));
}
```
