# Examples of `Worker` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)

## Example 1

**Источник**: <https://github.com/microsoft/windows-rs/blob/f850dcbf64b8ee881814f4da70a27408e125c5b9/web/features/src/app.tsx#L151-L166>

```TypeScript
React.useEffect(() => {
    const worker = new Worker(
        new URL('./worker/worker.ts', import.meta.url)
    );
    worker.addEventListener('message', onMessage);
    worker.postMessage({
        name: 'initialize',
        branch
    } as IInitializeMessage);
    setWorker(worker);

    return () => {
        worker.removeEventListener('message', onMessage);
        worker.terminate();
    };
}, [branch]);
```

## Example 2

**Источник**: <https://github.com/triggerdotdev/jsonhero-web/blob/0d781b714a4de9ecb9bcedc0cd6214ba81004c9f/app/hooks/useJsonSearch.tsx#L195-L222>

```TypeScript
const handleWorkerMessage = useCallback(
  (e: MessageEvent<SearchReceiveWorkerEvent>) => dispatch(e.data),
  [dispatch]
);

const workerRef = useRef<Worker | null>();

useEffect(() => {
  if (typeof window === "undefined" || typeof window.Worker === "undefined") {
    return;
  }

  if (workerRef.current) {
    return;
  }

  const worker = new Worker("/entry.worker.js");
  worker.onmessage = handleWorkerMessage;

  workerRef.current = worker;

  workerRef.current.postMessage({
    type: "initialize-index",
    payload: {
      json,
    },
  });
}, [json, workerRef.current]);
```

## Example 3

**Источник**: <https://github.com/allusion-app/Allusion/blob/631cfb5fb9c3bb62677e5fd37be28dbfaf4b8e2f/src/frontend/image/ThumbnailGeneration.tsx#L24-L31>

```TypeScript

// Set up multiple workers for max performance
const NUM_THUMBNAIL_WORKERS = 4;
const workers: Worker[] = [];
for (let i = 0; i < NUM_THUMBNAIL_WORKERS; i++) {
  workers[i] = new Worker(
    new URL('src/frontend/workers/thumbnailGenerator.worker', import.meta.url),
  );
}

// ...
// More related code
// ...

```

## Example 4

**Источник**: <https://github.com/rowyio/rowy/blob/f8e6aa84484ef191c5bfbfc529b76b3302d3b1fa/src/components/fields/Formula/useFormula.tsx#L56-L85>

```TypeScript

useEffect(() => {
  setError(null);
  setLoading(true);

  const worker = new Worker(new URL("./worker.ts", import.meta.url), {
    type: "module",
  });
  worker.onmessage = ({ data: { result, error } }: any) => {
    worker.terminate();
    if (error) {
      setError(error);
    } else {
      setResult(result);
    }
    setLoading(false);
  };

  worker.postMessage(
    JSON.stringify({
      formulaFn,
      row: availableFields,
      ref: serializeRef(ref.path),
    })
  );

  return () => {
    worker.terminate();
  };
  // eslint-disable-next-line react-hooks/exhaustive-deps
}, [useDeepCompareMemoize(listeners), formulaFn]);

```

## Example 5

**Источник**: <https://github.com/canonical/lxd-ui/blob/8b0ee16347e553e0097d1fe11a3ca990b43bae98/src/pages/login/CertificateGenerate.tsx#L37-L59>

```TypeScript
const createCert = (password: string) => {
  closeModal();
  setGenerating(true);


  const worker = new Worker(
    new URL("../../util/certificate?worker", import.meta.url),
    { type: "module" },
  );


  worker.onmessage = (event: MessageEvent<Certs>) => {
    setCerts(event.data);
    setGenerating(false);
    worker.terminate();
  };


  worker.onerror = (error) => {
    console.error("Web Worker error:", error);
    setGenerating(false);
    worker.terminate();
  };


  worker.postMessage(password);
};

```

## Example 6

**Источник**:

```TypeScript
const spawnSearchWorker = memoize(
  (_key: string) => new Worker(new URL('../workers/fuseSearch.worker', import.meta.url)),
);

// ...
// More related code
// ...


```
