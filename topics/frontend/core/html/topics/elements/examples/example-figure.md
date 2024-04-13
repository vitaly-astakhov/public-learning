# Examples of figure element usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [The figure element [HTML Spec]](https://html.spec.whatwg.org/multipage/grouping-content.html#the-figure-element)

### Example 1

```html
<figure>
  <div>
    <a
      style="--aspect-ratio: 16/9"
      href="/video/213479/Life-on-the-Plains-Illinois-Frank-Sadorus-photography"
    >
      <img
        src="https://cdn.britannica.com/79/213479-138-CA2C079A/Life-on-the-Plains-Illinois-Frank-Sadorus-photography.jpg?w=800&h=450&c=crop"
        alt="Frank Sadorus: Photographing life on the Illinois plains"
        loading="lazy"
      />
      <div style="top: 50%; transform: translateY(-50%)">
        <em data-icon="play_arrow"></em>
      </div>
    </a>
  </div>
  <figcaption>
    <div>Frank Sadorus: Photographing life on the Illinois plains</div>
    <div>
      <span>
        Learn more about life on the plains with the photography of Frank
        Sadorus.
      </span>
      <button aria-label="Toggle more/less fact data">
        <span>(more)</span>
      </button>
    </div>
    <a href="/technology/photography/images-videos">
      See all videos for this article
    </a>
  </figcaption>
</figure>

```

### Example 2

**Источник**: <https://unsplash.com/s/photos/photography>

```html

<figure itemprop="image" itemscope="" itemtype="https://schema.org/ImageObject">
  <div>
    <div>
      <div>
        <div>
          <a
            itemprop="contentUrl"
            title="a woman is taking a picture of a potted plant"
            href="/photos/a-woman-is-taking-a-picture-of-a-potted-plant-Yo35RIcZRgU"
          >
            <div>
              <div style="background-color:#EFEFEF"></div>
              <div>
                <img
                  alt="a woman is taking a picture of a potted plant"
                  srcset="https://plus.unsplash.com/premium_photo-1668383207771-dcf6e2d520f5?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8cGhvdG9ncmFwaHl8ZW58MHx8MHx8fDA%3D 800w"
                  src="https://plus.unsplash.com/premium_photo-1668383207771-dcf6e2d520f5?q=80&w=1000&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8cGhvdG9ncmFwaHl8ZW58MHx8MHx8fDA%3D"
                  sizes="(min-width: 1335px) 410.6666666666667px, (min-width: 992px) calc(calc(100vw - 88px) / 3), (min-width: 768px) calc(calc(100vw - 64px) / 2), 100vw"
                  itemprop="thumbnailUrl"
                  style="aspect-ratio:4000 / 5333"
                />
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
    <div>
      <div>
        <a title="behind the scenes images" href="/s/photos/behind-the-scenes">
          behind the scenes
        </a>
        <a title="photostudio images" href="/s/photos/photostudio">
          photostudio
        </a>
        <a title="photo shoot images" href="/s/photos/photo-shoot">
          photo shoot
        </a>
      </div>
    </div>
  </div>
</figure>

```

### Example 3

**Источник**: <https://www.nationalgeographic.com/photography/article/story-behind-images-photographer>

```html

<figure>
  <div>
    <div>
      <div>
        <picture>
          <source
            media="(max-width: 374px)"
            srcset="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=374&h=249, https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=748&h=498 2x"
          />
          <source
            media="(min-width: 375px) and (max-width: 413px)"
            srcset="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=413&h=275, https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=826&h=550 2x"
          />
          <source
            media="(min-width: 414px) and (max-width: 767px)"
            srcset="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=718&h=479, https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=1436&h=958 2x"
          />
          <source
            media="(min-width: 768px) and (max-width: 1024px)"
            srcset="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=718&h=479, https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=1436&h=958 2x"
          />
          <source
            media="(min-width: 1025px)"
            srcset="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=1280&h=853, https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg?w=2560&h=1706 2x"
          />
          <img
            alt="Storm towers over a farm grain elevator."
            src="https://i.natgeofe.com/n/0714edbd-b27e-4e8e-8b55-54e36950711c/STOCK_MM10170_KrystleWrightHeartExplosions_103_Archive_Photographer_05_3x2.jpg"
          />
        </picture>
      </div>
    </div>
  </div>
  <figcaption>Photograph by Krystle Wright</figcaption>
</figure>;


```

### Example 4

**Источник**: <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre>

```html

<figure>
  <table>
    <tbody>
      <tr>
        <th scope="row"><a href="/en-US/docs/Web/HTML/Content_categories">Content categories</a></th>
        <td><a href="/en-US/docs/Web/HTML/Content_categories#flow_content">Flow content</a>, palpable content.</td>
      </tr>
      <tr>
        <th scope="row">Permitted content</th>
        <td><a href="/en-US/docs/Web/HTML/Content_categories#phrasing_content">Phrasing content</a>.</td>
      </tr>
      <tr>
        <th scope="row">Tag omission</th>
        <td>None, both the starting and ending tag are mandatory.</td>
      </tr>
      <tr>
        <th scope="row">Permitted parents</th>
        <td>
          Any element that accepts
          <a href="/en-US/docs/Web/HTML/Content_categories#flow_content">flow content</a>.
        </td>
      </tr>
      <tr>
        <th scope="row">Implicit ARIA role</th>
        <td><code><a href="/en-US/docs/Web/Accessibility/ARIA/Roles/generic_role">generic</a></code></td>
      </tr>
      <tr>
        <th scope="row">Permitted ARIA roles</th>
        <td>Any</td>
      </tr>
      <tr>
        <th scope="row">DOM interface</th>
        <td><a href="/en-US/docs/Web/API/HTMLPreElement"><code>HTMLPreElement</code></a></td>
      </tr>
    </tbody>
  </table>
</figure>


```
