## gim - Grid Based Image Merge Library

`gim` is a image merging library that can accept image paths as input, read the image contents, merge them into a grid with the desired size. 

[![GoDoc](https://godoc.org/github.com/ozankasikci/dockerfile-generator?status.svg)](https://godoc.org/github.com/ozankasikci/dockerfile-generator)

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
  * [Installing as an Executable](#installing-as-an-executable)
  * [Installing as a Library](#installing-as-a-library)
- [Getting Started](#getting-started)
  * [Using dfg as an Executable](#using-dfg-as-an-executable)
  * [Using dfg as a Library](#using-dfg-as-a-library)
- [Examples](#examples)
  * [YAML File Example](#yaml-file-example)
  * [Library Usage Example](#library-usage-example)
- [TODO](#todo)

## Overview

`gim` provides an easy way to merge images into a flexible grid system as a GO library.

The main purpose of the library is to help creating image collages programatically.

## Installation

`go get -u github.com/ozankasikci/go-image-merge`

## Getting Started

Import the library and give the image paths and grid size as the minimum required arguments.

Basic usage:

```go
import gim "github.com/ozankasikci/go-image-merge"

// accepts image paths, grid size x, grid size y
// returns an *image.RGBA object
rgba, err := gim.New([]string{ "./cmd/gim/kitten.jpg" }, 2, 1).Merge()

// save the output to jpg or png
file, err := os.Create("file/path.jpg|png")
err = jpeg.Encode(file, rgba, &jpeg.Options{Quality: 80})
err = png.Encode(file, rgba)
```

## Examples

### Grid size - Horizontal
```go
paths := []string{ "./cmd/gim/kitten.jpg", "./cmd/gim/kitten.jpg", "./cmd/gim/kitten.jpg" }
rgba, err := gim.New(paths, 3, 1).Merge()
```

#### Output
![](https://raw.githubusercontent.com/ozankasikci/ozankasikci.github.io/master/gim/grid-size-3-1.jpg)

### Grid size - Vertical
```go
paths := []string{ "./cmd/gim/kitten.jpg", "./cmd/gim/kitten.jpg" }
rgba, err := gim.New(paths, 1, 2).Merge()
```

#### Output
![](https://raw.githubusercontent.com/ozankasikci/ozankasikci.github.io/master/gim/grid-size-1-2.jpg)

### Functional Options - BaseDir
```go
// you can omit the full if you set a base dir
paths := []string{ "kitten.jpg", "kitten.jpg" }
rgba, err := gim.New(paths, 1, 2, gim.OptBaseDir("./cmd/gim")).Merge()
```

### Functional Options - GridSize
```go
// you can resize the grids in pixels
paths := []string{ "kitten.jpg", "kitten.jpg" }
rgba, err := gim.New( paths, 2, 1, gim.OptBaseDir("./cmd/gim"), gim.OptGridSize(200,150)).Merge()
```
#### Output
![](https://raw.githubusercontent.com/ozankasikci/ozankasikci.github.io/master/gim/grid-resize-pixels-200-150.jpg)

## TODO
- [ ] Add colored background support
