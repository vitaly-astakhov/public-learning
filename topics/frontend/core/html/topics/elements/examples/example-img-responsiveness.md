# Examples of declarative `<img>` responsiveness

## Table of content

- [Device-pixel-ratio-based selection](#device-pixel-ratio-based-selection)
  - [Example 1](#example-1)
  - [Example 2](#example-2)
    - [Example 3](#example-3)

### Device-pixel-ratio-based selection

#### Example 1

**Источник**: <https://github.com/denoland/fresh/blob/0e5962ce376e784329e0135a19dbd2db5f88d6e4/www/components/Projects.tsx#L24-L33>

```TypeScript

<img
  loading="lazy"
  src={`/showcase/${project.image}1x.jpg`}
  srcset={`/showcase/${project.image}2x.jpg 2x, /showcase/${project.image}1x.jpg 1x`}
  alt={project.title}
  width={600}
  height={337}
  style={{ aspectRatio: "16/9" }}
  class="object-cover shadow-lg group-hover:shadow-xl group-hover:opacity-70 rounded-lg"
/>

```

#### Example 2

**Источник**: <https://github.com/gitpod-io/gitpod/blob/e84ffc693252242c49b00751b3cde805b986c65a/components/dashboard/src/login/SetupPending.tsx#L32-L41>

```TypeScript
<img
    className="mb-8"
    src={isDark ? cubicleDarkImg : cubicleImg}
    srcSet={`${isDark ? cubicleDarkImg : cubicleImg} 1x, ${
        isDark ? cubicleDarkImg2x : cubicleImg2x
    } 2x`}
    alt="cubical illustration"
    width="240"
    height="251"
/>

```

#### Example 3

**Источник**: <https://html.spec.whatwg.org/multipage/images.html#introduction-3:device-pixel-ratio-2>

### Viewport-based selection
