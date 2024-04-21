# Examples of `EventSource` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)

## Example 1

**Источник**: <https://github.com/BloopAI/bloop/blob/c09196506d9946bd75d7997c4149d6c75032595b/client/src/CommandBar/steps/items/DocItem.tsx#L68-L96>

```TypeScript

const startEventSource = useCallback(() => {
  setIsIndexingFinished(false);
  eventSourceRef.current?.close();
  eventSourceRef.current = new EventSource(
    `${API_BASE_URL}/docs/${doc.id}/status`,
  );
  eventSourceRef.current.onmessage = (ev) => {
    try {
      const data = JSON.parse(ev.data);
      console.log(data);
      if (data.Ok.Done) {
        eventSourceRef.current?.close();
        eventSourceRef.current = null;
        setIsIndexingFinished(true);
        refetchDoc();
        return;
      }
    } catch (err) {
      console.log(err);
      eventSourceRef.current?.close();
      eventSourceRef.current = null;
    }
  };
  eventSourceRef.current.onerror = (err) => {
    console.log(err);
    eventSourceRef.current?.close();
    eventSourceRef.current = null;
  };
}, [doc.id]);

```

## Example 2

**Источник**: <https://github.com/umijs/umi/blob/9d160fc2bc9236b3df06e349412bbe0a6b2df451/examples/with-no-compress-for-sse/pages/index.tsx#L16-L29>

```TypeScript

useEffect(() => {
  console.log('开始请求');
  const eventSource = new EventSource('/events/number');
  let startEvent = new Event('开始请求');
  setEvents((prev) => [...prev, startEvent]);
  eventSource.onmessage = function (e: any) {
    let item = new Event(e.data);
    setEvents((prev) => [...prev, item]);
  };
  eventSource.onerror = (e) => {
    console.log('EventSource failed:', e);
    eventSource.close();
  };
}, []);

```

## Example 3

**Источник**: <https://github.com/emsesp/EMS-ESP32/blob/1487f30c433e6fc87ecbba42c04f9f9ea483dd4f/interface/src/framework/system/SystemLog.tsx#L120-L131>

```TypeScript

useEffect(() => {
  const es = new EventSource(addAccessTokenParameter(LOG_EVENTSOURCE_URL));
  es.onmessage = onMessage;
  es.onerror = () => {
    es.close();
    toast.error('EventSource failed');
  };

  return () => {
    es.close();
  };
});

```

## Example 4

**Источник**: <https://github.com/marcopeocchi/yt-dlp-web-ui/blob/a73b8d362ecb268a2eecb9509ebd60003e8d4b9d/frontend/src/components/LogTerminal.tsx#L18-L37C20>

```TypeScript

  const eventSource = useMemo(
    () => new EventSource(`${serverAddr}/log/sse?token=${token}`),
    [serverAddr]
  )

  useEffect(() => {
    eventSource.addEventListener('log', event => {
      const msg: string[] = JSON.parse(event.data)
      setLogBuffer(buff => [...buff, ...msg].slice(-500))

      boxRef.current?.scrollTo(0, boxRef.current.scrollHeight)
    })

    // TODO: in dev mode it breaks sse
    return () => eventSource.close()
  }, [eventSource])

  useEffect(() => {
    eventSource.onopen = () => setIsConnecting(false)
  }, [eventSource]);

```

## Example 5

**Источник**: <https://github.com/grafana/xk6-dashboard/blob/3d00fafadf4bac90c0e16b84a5abb02b5b3f5715/dashboard/assets/packages/ui/src/store/digest.tsx#L20-L31>

```TypeScript

useEffect(() => {
  const source = new EventSource(endpoint)

  const listener = (event: MessageEvent) => {
    digest.handleEvent(event)
    setDigest(new Digest(digest))
  }

  for (const type in EventType) {
    source.addEventListener(type, listener)
  }
}, [])

```

## Example 6

**Источник**: <https://github.com/thoughtworks/metrik/blob/def6a52cb7339f6a422451710083177b9c79689a/frontend/src/pages/dashboard/context/DashboardContext.tsx#L186-L208C4>

```TypeScript

const syncBuildsWithProgress = () => {
  setSyncInProgress(true);

  const eventsource = new EventSource(`/api/project/${projectId}/sse-sync`);
  eventsource.addEventListener("PROGRESS_UPDATE_EVENT", e => {
    // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    // @ts-ignore
    const progressUpdate: ProgressUpdateEvt = JSON.parse(e.data);
    setProgressSummary(prevState => ({
      ...prevState,
      [progressUpdate.pipelineId]: progressUpdate,
    }));
  });
  eventsource.addEventListener("COMPLETE_STREAM_EVENT", () => {
    eventsource.close();
    setSyncInProgress(false);
    setProgressSummary({});

    getLastSyncTime();
    setPipelineStages([]);
    getPipelineStagesRequest({ projectId });
  });
};

```
