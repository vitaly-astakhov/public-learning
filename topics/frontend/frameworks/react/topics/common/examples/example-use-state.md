# Examples of `useState` hook usage

## Navigation

- [With *initializer function*](#with-initializer-function)
  - [Example 1](#example-1)
  - [Example 2](#example-2)
  - [Example 3](#example-3)
  - [Example 4](#example-4)
  - [Example 5](#example-5)
  - [Example 6](#example-6)
  - [Example 7](#example-7)

## With *initializer function*

### Example 1

**Источник**: <https://github.com/vercel/next.js/blob/35879797e7873b31219e5a212a88d1c2e8b3d0d3/examples/with-slate/pages/index.tsx#L32>

```TypeScript

const [editor] = useState(() => withReact(withHistory(createEditor())));

```

### Example 2

**Источник**: <https://github.com/storybookjs/storybook/blob/479b8e919fccf12d3def4470d455682bb3965c45/code/ui/blocks/src/controls/Color.tsx#L221>

```TypeScript

const [color, setColor] = useState(() => parseValue(value));

```

### Example 3

**Источник**: <https://github.com/prometheus/prometheus/blob/f36915b6b14e3b54132a9cd701835d0255741f96/web/ui/react-app/src/hooks/useLocalStorage.tsx#L4-L6>

```TypeScript

const [value, setValue] = useState(() =>
  JSON.parse(localStorage.getItem(localStorageKey) || JSON.stringify(initialState))
);

```

### Example 4

**Источник**: <https://github.com/excalidraw/excalidraw/blob/530617be90df8d41f93c7c885d3097565c4c7f6d/packages/excalidraw/components/ImageExportDialog.tsx#L363-L370>

```TypeScript


// we need to take a snapshot so that the exported state can't be modified
// while the dialog is open
const [{ appStateSnapshot, elementsSnapshot }] = useState(() => {
  return {
    appStateSnapshot: cloneJSON(appState),
    elementsSnapshot: cloneJSON(elements),
  };
});

```

### Example 5

**Источник**: <https://github.com/plotly/dash/blob/93b513df7f6782e97a7e3277d7aafad7c00714fc/dash/dash-renderer/src/AppProvider.react.tsx#L9>

```TypeScript
const [{store}] = useState(() => new Store());
```

### Example 6

**Источник**: <https://github.com/nextui-org/nextui/blob/4cad622460f0d5a0c5c2a653ec8e910edad1578d/apps/docs/components/cmdk.tsx#L131>

```TypeScript
const [menuNodes] = useState(() => new MultiRef<number, HTMLElement>());
```

### Example 7

**Источник**: <https://github.com/remotion-dev/remotion/blob/a304bac3d59cceacdcbe42960cf8dd9cb7fe5098/packages/three/src/ThreeCanvas.tsx#L37>

```TypeScript
const [waitForCreated] = useState(() =>
  delayRender('Waiting for <ThreeCanvas/> to be created'),
);
```
