# Examples of `<dl>` element usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [The figure element [HTML Spec]](https://html.spec.whatwg.org/multipage/grouping-content.html#the-dl-element)

### Example 1

**Источник**: <https://developer.mozilla.org/en-US/docs/Web/HTML>

```html
<dl>
  <dt id="html_introduction"><a href="#html_introduction">HTML Introduction</a></dt>
  <dd>
    <p>If you're new to web development, be sure to read our <a href="/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics">HTML Basics</a> article to learn what HTML is and how to use it.</p>
  </dd>
  <dt id="html_tutorials"><a href="#html_tutorials">HTML Tutorials</a></dt>
  <dd>
    <p>For articles about how to use HTML, as well as tutorials and complete examples, check out our <a href="/en-US/docs/Learn/HTML">HTML Learning Area</a>.</p>
  </dd>
  <dt id="html_reference"><a href="#html_reference">HTML Reference</a></dt>
  <dd>
    <p>In our extensive <a href="/en-US/docs/Web/HTML/Reference">HTML reference</a> section, you'll find the details about every element and attribute in HTML.</p>
  </dd>
</dl>

```

### Example 2

**Источник**: <https://html.spec.whatwg.org/multipage/links.html#introduction-2>

```html

<dl>
  <dt>
    <dfn
      id="external-resource-link"
      data-lt="external resource link"
      data-export=""
    >
      Links to external resources
    </dfn>
  </dt>
  <dd>
    <p>
      These are links to resources that are to be used to augment the current
      document, generally automatically processed by the user agent. All{" "}
      <a
        href="#external-resource-link"
        id="introduction-2:external-resource-link"
      >
        external resource links
      </a>{" "}
      have a{" "}
      <a
        id="introduction-2:fetch-and-process-the-linked-resource"
        href="semantics.html#fetch-and-process-the-linked-resource"
      >
        fetch and process the linked resource
      </a>
      algorithm which describes how the resource is obtained.
    </p>
  </dd>
  <dt>
    <dfn id="hyperlink" data-lt="hyperlink" data-export="">
      Hyperlinks
    </dfn>
  </dt>
  <dd>
    <p>
      These are links to other resources that are generally exposed to the user
      by the user agent so that the user can cause the user agent to{" "}
      <a id="introduction-2:navigate" href="browsing-the-web.html#navigate">
        navigate
      </a>{" "}
      to those resources, e.g. to visit them in a browser or download them.
    </p>
  </dd>
  <dt>
    <dfn id="internal-resource-link" data-export="">
      Internal resource links
    </dfn>
  </dt>
  <dd>
    <p>
      These are links to resources within the current document, used to give
      those resources special meaning or behavior.
    </p>
  </dd>
</dl>;


```
