# Examples of `BroadcastChannel` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [HTML Spec example](https://html.spec.whatwg.org/multipage/web-messaging.html#:~:text=Suppose%20a%20page%20wants%20to)

## Example 1

**Источник**: <https://github.com/nextauthjs/next-auth/blob/24ef3f4212f42d92d275c4666126f3b559597782/packages/next-auth/src/react.tsx#L72-L81>

```TypeScript

function broadcast() {
  if (typeof BroadcastChannel !== "undefined") {
    return new BroadcastChannel("next-auth")
  }
  return {
    postMessage: () => {},
    addEventListener: () => {},
    removeEventListener: () => {},
  }
}

// ...
// Some code
// ...

broadcast().postMessage({ event: "session", data: { trigger: "signout" } })

```

## Example 2

**Источник**: <https://github.com/backstage/backstage/blob/122d0d44665de382579c4211dc9a3589c866727a/plugins/auth-react/src/hooks/useCookieAuthRefresh/useCookieAuthRefresh.tsx#L45-L49>

```TypeScript
const channel = useMemo(() => {
  return 'BroadcastChannel' in window
    ? new BroadcastChannel(`${pluginId}-auth-cookie-expires-at`)
    : null;
}, [pluginId]);

// ...
// Some code
// ...

useEffect(() => {
  // Only schedule a refresh if we have a successful response
  if (state.status !== 'success' || !state.result) {
    return () => {};
  }
  channel?.postMessage({
    action: 'COOKIE_REFRESH_SUCCESS',
    payload: state.result,
  });
  let cancel = refresh(state.result);
  const listener = (
    event: MessageEvent<{ action: string; payload: { expiresAt: string } }>,
  ) => {
    const { action, payload } = event.data;
    if (action === 'COOKIE_REFRESH_SUCCESS') {
      cancel();
      cancel = refresh(payload);
    }
  };
  channel?.addEventListener('message', listener);
  return () => {
    cancel();
    channel?.removeEventListener('message', listener);
  };
}, [state, refresh, channel]);
```

## Example 3

**Источник**: <https://github.com/cognetwork-dev/Metallic/blob/82fd0c8f801332b1e6f871b0b637532048b1dfc0/src/components/head.tsx#L73-L82>

```TypeScript

useEffect(() => {
    const titleChannel = new BroadcastChannel("metallic/title");

    titleChannel.onmessage = (e) => {
        setTitle(String(e.data))
    }

    localStorage.setItem("metallic/title", title);
    titleChannel.postMessage(title)
}, [title]);

```

## Example 4

**Источник**: <https://github.com/mage-ai/mage-ai/blob/5967eca1e3fdbbfba09f701c25dea02a9a0ee2cd/mage_ai/frontend/pages/pipelines/%5Bpipeline%5D/edit.tsx#L567-L586>

```TypeScript
useEffect(() => {
  const channel = new BroadcastChannel(`${pipelineUUID}_pipeline_editor_tabs`);
  channel.addEventListener('message', (event) => {
    if (event.data === 'new_tab_same_page_opened') {
      setMultipleTabsOpen(true);
    }
  });
  /*
    * Send message to this pipeline’s broadcast channel when the component mounts
    * so that we can detect if there are multiple tabs open for the same pipeline,
    * which could cause issues with the pipeline's block files being overwritten
    * unexpectedly.
    */
  channel.postMessage('new_tab_same_page_opened');


  return () => {
    channel.close();
  };
// eslint-disable-next-line react-hooks/exhaustive-deps
}, []);

```
