# Examples of `queueMicrotask()` usage

## Table of content

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)
- [Example 6](#example-6)
- [Example 7](#example-7)
- [Example 8](#example-8)
- [Example 9](#example-9)

### Example 1

**Источник**: <https://github.com/PostHog/posthog/blob/1df7232441b7b5e3abf79739dd8c7d2193238c6d/frontend/src/scenes/notebooks/Nodes/utils.tsx#L116-L117>

```TypeScript

// NOTE: queueMicrotask protects us from TipTap's flushSync calls, ensuring we never modify the state whilst the flush is happening
queueMicrotask(() => props.updateAttributes(stringifiedAttrs))

```

### Example 2

**Источник**: <https://github.com/ariakit/ariakit/blob/c18f793aed1af7235b8b2a5ed2b3d6db3501dff6/packages/ariakit-react-core/src/form/form-label.tsx#L95-L99C10>

```TypeScript

queueMicrotask(() => {
  const focusableElement = getFirstTabbableIn(fieldElement, true, true);
  focusableElement?.focus();
  focusableElement?.click();
});

```

### Example 3

**Источник**: <https://github.com/tamagui/tamagui/blob/26a448a4e9a2c1a6f2a7a4e8fe5a5663bdd2abf7/packages/use-store/src/observe.tsx#L135-L152C4>

```TypeScript

let isUpdating = false
const onUpdateDebouncedWithoutTracking = () => {
  if (isUpdating) return
  isUpdating = true
  queueMicrotask(() => {
    try {
      for (const storeInfo of storeInfos) {
        storeInfo.disableTracking = true
      }
      onUpdate()
    } finally {
      isUpdating = false
      for (const storeInfo of storeInfos) {
        storeInfo.disableTracking = false
      }
    }
  })
}

```

### Example 4

**Источник**: <https://github.com/artsy/eigen/blob/40fcae75169a79d9286dd51d7e0a46bab64d2e0a/src/app/Scenes/SavedSearchAlert/Components/SavedSearchFilterSize.tsx#L62-L67>

```TypeScript

queueMicrotask(() => {
  addValueToAttributesByKeyAction({
    key: SearchCriteria.sizes,
    value: newValues,
  })
})

```

### Example 5

**Источник**: <https://github.com/apache/superset/blob/1ef839ca6dcc7679aa2c6008add0a5de13707406/superset-frontend/src/explore/components/controls/VizTypeControl/VizTypeGallery.tsx#L465-L475>

```TypeScript

useEffect(() => {
  if (isSelected) {
    // We need to wait for the modal to open and then scroll, so we put it in the microtask queue
    queueMicrotask(() =>
      scrollIntoView(btnRef.current as HTMLButtonElement, {
        behavior: 'smooth',
        scrollMode: 'if-needed',
      }),
    );
  }
}, []);

```

### Example 6

**Источник**: <https://github.com/davidjerleke/embla-carousel/blob/09da7a68fd7629958f1271e5b3c9c04acbce704b/packages/embla-carousel-docs/src/components/Tabs/Tabs.tsx#L121-L133>

```TypeScript

queueMicrotask(() => {
  const focusedTabId = focusedTab.current?.id || ''
  const autoNavigated = !focusedTabId.endsWith(tabsGroupId.current)
  focusedTab.current = null


  if (autoNavigated) return


  const newTabsPosition = getTabsPosition(tabsWrapper.current)
  const diff = getTabsPositionDiff(newTabsPosition, tabsPosition.current)
  if (diff) window.scrollBy({ top: diff })


  tabsPosition.current = getTabsPosition(tabsWrapper.current)
})

```

### Example 7

**Источник**: <https://github.com/atlassian/pragmatic-drag-and-drop/blob/8a20025bd1c9ecbbf87f320546689fdbd11e6780/packages/react-beautiful-dnd-migration/src/droppable/draggable-clone.tsx#L212-L252C15>

```TypeScript

queueMicrotask(() => {
  /**
   * Because this update occurs in a microtask, we need to check
   * that the drag is still happening.
   *
   * If it has ended we should not try to update the preview.
   */
  const dragState = getDragState();
  if (!dragState.isDragging) {
    return;
  }


  /**
   * The placeholder might not exist if its associated
   * draggable unmounts in a virtual list.
   */
  const placeholder = findPlaceholder(contextId);
  const placeholderRect = placeholder
    ? placeholder.getBoundingClientRect()
    : null;


  /**
   * The drop indicator might not exist if the current target
   * is null
   */
  const dropIndicator = findDropIndicator();
  const dropIndicatorRect = dropIndicator
    ? dropIndicator.getBoundingClientRect()
    : null;


  dispatch({
    type: 'UPDATE_KEYBOARD_PREVIEW',
    payload: {
      update,
      draggableDimensions,
      droppable,
      placeholderRect,
      dropIndicatorRect,
    },
  });
});

```

### Example 8

**Источник**: <https://github.com/morethanwords/tweb/blob/b6486ad81d7523284affd4900bcd2663da079e4e/src/components/popups/reassignBoost.tsx#L117-Ls130>

```TypeScript

queueMicrotask(() => {
  for(const element of added) {
    element.animate(keyframes, options);
  }


  const reversedKeyframes = keyframes.slice().reverse();
  const promises: Promise<any>[] = [];
  for(const element of removed) {
    const animation = element.animate(reversedKeyframes, options);
    promises.push(animation.finished);
  }


  Promise.all(promises).then(() => finishRemoved(removed));
});

```

### Example 9

**Источник**: <https://github.com/concrete-utopia/utopia/blob/93cab157058599ca91f986dd8aaa1f1a77f431a7/editor/src/components/editor/editor-component.tsx#L410-L424>

```TypeScript

queueMicrotask(() => {
  let actions: EditorAction[] = []
  const permissions = getPermissions(state)
  if (!permissions.edit && permissions.comment) {
    actions.push(
      EditorActions.switchEditorMode(EditorModes.commentMode(null, 'not-dragging')),
      EditorActions.setRightMenuTab(RightMenuTab.Comments),
      EditorActions.setCodeEditorVisibility(false),
    )
  } else {
    actions.push(EditorActions.setCodeEditorVisibility(true))
  }
  dispatch(actions)
})
},

```
