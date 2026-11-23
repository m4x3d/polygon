# Polygon

Turns pictures into low-poly polygon art, entirely in the browser. One HTML file, no dependencies, no build step. Images never leave your machine.

## Use

Open `index.html` in a browser, or serve the folder with any static file server. Pick, drop or paste an image, then:

- **Detail** sets the number of triangles
- **Edge focus** sets how strongly triangles cluster along edges
- **Shuffle** gives a new random arrangement
- **Save PNG** exports at source resolution (2048 to 4096 px on the long side)
- **Save SVG** exports the triangles as vectors

## How it works

1. Edge map: Sobel over RGB (WebGPU compute)
2. Points: variable-radius Poisson-disc sampling, denser on edges and snapped to edge ridges (CPU)
3. Delaunay triangulation (CPU)
4. Mean colour per triangle, averaged in linear light (WebGPU compute)
5. Rendering with 4x MSAA (WebGPU)

Browsers without WebGPU run steps 1, 4 and 5 on the CPU and Canvas 2D instead.
