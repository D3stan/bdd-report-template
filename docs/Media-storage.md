**Media storage** is a feature that ensures all the required files are present in the output directory when a Quarkdown project is exported.

Here's what it does:

1. Keeps track of the external files (*media*) referenced in a Quarkdown document in **image** and **reference image** nodes;
2. Each media is copied to the output directory as `media/<symbolic name>`;
3. The image nodes update their source path to the newly created file.

> #### Example:
> Source:
> ```markdown
> ![Image](../my-img.png)
> ```
> Result:
> ```html
> <img src="media/my-img@HASH.png" alt="Image" />
> ```

The media storage is enabled by default and can be turned off via the `--no-media-storage` flag.

## Why
Take HTML as an example: images from remote URLs are loaded effortlessly, while *local* ones (e.g. `../my-img.png`) require the image file to be present on the server at the exact same location.

Imagine writing a Quarkdown document, typing `![Image](my-img.png)`, with `my-img.png` located in the same directory as your Quarkdown source. You'd be sure it'll work, but as soon you compile the project and open your HTML artifact you notice the file cannot be found by the browser, simply because it's not there.

Thanks to the media storage system, all the media files are carried around.

## Options
The storage is able to handle **both local and remote files**. The rules that determine which types are allowed in the storage are set by the active renderer.

- When rendering to HTML, it is enabled for local files only.  
- On the other hand LaTeX, which isn't yet supported but might be in the future, also requires remote media to be downloaded locally.

Overriding these rules is supported, although currently unavailable via CLI.