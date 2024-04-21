
# Examples of `useReducer` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [With *initializer function*](#with-initializer-function)
  - [Example 5](#example-5)
  - [Example 6](#example-6)
  - [Example 7](#example-7)

### Example 1

**Источник**: <https://github.com/aws-samples/websocket-api-cognito-auth-sample/blob/a7fe9ef8bab59c4639b7b9cd72d6af9bcb480ad0/frontend/src/components/echo.tsx#L16>

```TypeScript

const [closed, forceClose] = useReducer(() => true, false);

```

### Example 2

**Источник**: <https://github.com/immutable-js/immutable-js/blob/d7664bf9d3539da8ea095f2ed08bbe1cd0d46071/website/src/TypeDocumentation.tsx#L44-L45>

```TypeScript

const [showInherited, toggleShowInherited] = useReducer(toggle, true);
const [showInGroups, toggleShowInGroups] = useReducer(toggle, true);

```

### Example 3

**Источник**: <https://github.com/realm/realm-js/blob/6269081d4e58c116ea7800bdd18c59dc0ffd9c80/packages/realm-react/src/UserProvider.tsx#L60>

```TypeScript

const [, forceUpdate] = useReducer((x) => x + 1, 0);

```

### Example 4

**Источник**: <https://github.com/mui/material-ui/blob/657705633bbcf85019aa8bbf16d143a0d304edfe/docs/src/modules/components/JoyThemeBuilder.tsx#L1004-L1010C6>

```TypeScript

const [states, setStates] = React.useReducer<
  StateReducer<{ hover: boolean; active: boolean; disabled: boolean }>
>((prevState, action) => ({ ...prevState, ...action }), {
  hover: false,
  active: false,
  disabled: false,
});

```

## With *initializer function*

### Example 5

**Источник**: <https://github.com/RocketChat/Rocket.Chat/blob/d134a4d714d202bcfc40ee6cf210f0016d7b64fb/packages/mock-providers/src/MockedAppRootBuilder.tsx#L393C4-L393C113>

```TypeScript

const [translation, updateTranslation] = useReducer(reduceTranslation, undefined, () => reduceTranslation());

```

### Example 6

**Источник**: <https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/ad8a43f1e3a263b5228e6d09575be48910ff57ca/lib/msal-react/src/MsalProvider.tsx#L134-L140>

```TypeScript

const [state, updateState] = useReducer(reducer, undefined, () => {
    // Lazy initialization of the initial state
    return {
        inProgress: InteractionStatus.Startup,
        accounts: instance.getAllAccounts(),
    };
});

```

### Example 7

**Источник**: <https://github.com/liqvidjs/liqvid/blob/6448c2def3dd7efdfe0c0983bfc66ca034f19e1b/packages/recording/src/Control.tsx#L148-L152>

```TypeScript

const [state, dispatch] = useReducer(reducer, null, () => ({
    start: isMac() ? "Alt+Meta+2" : "Ctrl+Alt+2",
    pause: isMac() ? "Alt+Meta+3" : "Ctrl+Alt+3",
    discard: isMac() ? "Alt+Meta+4" : "Ctrl+Alt+4",
}));

```
