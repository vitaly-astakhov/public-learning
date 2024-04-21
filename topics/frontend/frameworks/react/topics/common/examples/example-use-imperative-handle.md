# Examples of `useImperativeHandle` hook usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)

### Example 1

**Источник**: <https://github.com/getsentry/sentry/blob/01fab312db63fd1a5b5c391d0f132f0d3ed5c6e6/static/app/components/autoSelectText.tsx#L22-L33>

```TypeScript

// We need to expose a selectText method to parent components
// and need an imperative ref handle.
useImperativeHandle(forwardedRef, () => ({
  selectText: () => handleClick(),
}));

function handleClick() {
  if (!element.current) {
    return;
  }
  selectText(element.current);
}

```

### Example 2

**Источник**: <https://github.com/getsentry/sentry/blob/01fab312db63fd1a5b5c391d0f132f0d3ed5c6e6/static/app/components/slider/index.tsx#L173-L184>

```TypeScript

const nThumbs = state.values.length;
const refs = useRef<Array<HTMLInputElement>>([]);
useImperativeHandle(
  forwardedRef,
  () => {
    if (nThumbs > 1) {
      return refs.current;
    }
    return refs.current[0];
  },
  [nThumbs]
);

```

### Example 3

**Источник**: <https://github.com/excalidraw/excalidraw/blob/530617be90df8d41f93c7c885d3097565c4c7f6d/packages/excalidraw/components/TextField.tsx#L44-L52C26>

```TypeScript

const innerRef = useRef<HTMLInputElement | null>(null);

useImperativeHandle(ref, () => innerRef.current!);

useLayoutEffect(() => {
  if (selectOnRender) {
    innerRef.current?.select();
  }
}, [selectOnRender]);

```

### Example 4

**Источник**: <https://github.com/clash-verge-rev/clash-verge-rev/blob/f6aacbc31d7e7e80932c7297f2b2daa839214f2a/src/components/setting/mods/web-ui-viewer.tsx#L17-L23C7>

```TypeScript

const [open, setOpen] = useState(false);

useImperativeHandle(ref, () => ({
  open: () => setOpen(true),
  close: () => setOpen(false),
}));

```

### Example 5

**Источник**: <https://github.com/elastic/kibana/blob/654c0dc467784d0c71d7c20e409136c9e10a1e3c/src/plugins/presentation_panel/public/mocks.tsx#L34-L46>

```TypeScript

export const getMockPresentationPanelCompatibleComponent = <
  ApiType extends DefaultPresentationPanelApi = DefaultPresentationPanelApi
>(
  api?: ApiType
): Promise<PanelCompatibleComponent> =>
  Promise.resolve(
    React.forwardRef((_, apiRef) => {
      useImperativeHandle(apiRef, () => api ?? { uuid: 'test' });
      return (
        <div data-test-subj="testPresentationPanelInternalComponent">This is a test component</div>
      );
    })
  );

```

### Example 6

**Источник**: <https://github.com/pinpoint-apm/pinpoint/blob/d1dd51d10d662f5fb64b284bae6c05f014ada3be/web-frontend/src/main/v3/packages/ui/src/components/ScatterChart/core/ScatterChartCore.tsx#L92-L125>

```TypeScript

React.useImperativeHandle(
  ref,
  () => {
    return {
      isMounted: () => {
        return !!scatterRef.current;
      },
      getChartSize: () => {
        return getChartSize();
      },
      startRealtime: (duration: number) => {
        scatterRef.current?.startRealtime(duration);
      },
      stopRealtime: () => {
        scatterRef.current?.stopRealtime();
      },
      isRealtime: () => {
        return !!scatterRef.current?.isRealtime;
      },
      render: (data: ScatterDataType[]) => {
        scatterRef.current?.render(data, { append: true });
      },
      clear: () => {
        scatterRef.current?.clear();
      },
      setAxisOption: (option: Partial<ScatterChartOption['axis']>) => {
        scatterRef.current?.setOption({
          axis: option,
        });
      },
    };
  },
  [scatterRef.current],
);

```
