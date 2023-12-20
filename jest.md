# Jest

## Mock a fetch which return a blob

Test for a React component which return an `img` tag with `src` encoded in base64.
We mock the fetch request returning a blob, then we assert in the dom for the right `src`.

```typescript
const data =
  'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAIAAAACAgMAAAAP2OW3AAAAIGNIUk0AAHomAACAhAAA+gAAAIDoAAB1MAAA6mAAADqYAAAXcJy6UTwAAAAJUExURZmt2Zaq2P////iwbGMAAAABYktHRAJmC3xkAAAAB3RJTUUH5wwUCjAFf6Xr+QAAAAxJREFUCNdjYGAIAAAAVABRmLpazAAAACV0RVh0ZGF0ZTpjcmVhdGUAMjAyMy0xMi0yMFQxMDo0Nzo0NyswMDowMH7s3zsAAAAldEVYdGRhdGU6bW9kaWZ5ADIwMjMtMTItMjBUMTA6NDc6NDcrMDA6MDAPsWeHAAAAKHRFWHRkYXRlOnRpbWVzdGFtcAAyMDIzLTEyLTIwVDEwOjQ4OjA1KzAwOjAwunoCBgAAAABJRU5ErkJggg=='
const blob = new Blob([data], { type: 'image/png' })

describe('ImagesWithJWT', () => {
  it('should render', async () => {
    jest.spyOn(global, 'fetch').mockImplementationOnce(() =>
      Promise.resolve({
        ok: true,
        blob: () => Promise.resolve(blob),
      } as Response)
    )

    render(component(defaultProps))

    const img = await screen.findByRole('img')

    await waitFor(() => {
      expect(img.getAttribute('src')).toEqual(
        expect.stringMatching(/^data:image\/png;base64,ZGF0/)
      )
      jest.resetAllMocks()
    })
  })
```
