When running Quarkdown's [compiler](cli%3A-compiler) via `quarkdown c`, specifying the **`--pdf`** flag generates a PDF file.

- The content of the PDF matches 1:1 with what the HTML output would render in the Chrome browser.
- All document types and features supported by the HTML target are also supported.

## Requirements 

In order to generate PDF files from HTML, the following dependencies are required:
- Node.js
- npm (usually bundled with Node.js)
- [Puppeteer](https://pptr.dev) (`npm install puppeteer --prefix <quarkdown_dir>/lib`)

Dependencies are already taken care of by package managers and install scripts.

## Additional options

- `--node-path <path>`: sets the path to the Node.js executable. Defaults to `node`.

- `--npm-path <path>`: sets the path to the npm executable. Defaults to `npm`.

- `--pdf-no-sandbox`: disables Chrome sandbox during PDF generation.
  This is potentially unsafe and should be used only when strictly needed. For instance, some Linux distributions don't support headless sandbox.

## Environment variables

- `QD_NPM_PREFIX`: directory where `node_modules` should be found. Defaults to `lib` if Quarkdown was installed via a package manager or install script.

- `PUPPETEER_EXECUTABLE_PATH`: path to the Chrome/Chromium/Firefox executable. By default it is automatically searched in (in order):
  - Linux: `command -v {google-chrome, chromium-browser, chromium, firefox}`
  - macOS: `/Applications/{Google Chrome, Chromium, Firefox}.app/Contents/MacOS/{Google Chrome, Chromium, Firefox}`
  - Windows:
    - `{%ProgramFiles%, %ProgramFiles(x86)%}\{Google\Chrome, Chromium}\Application\chrome.exe`
    - `{%ProgramFiles%, %ProgramFiles(x86)%}\Mozilla Firefox\firefox.exe`

- `PUPPETEER_BROWSER`: `chrome`/`firefox`. Defaults to the automatically found browser.

## Exporting manually (legacy way)

An HTML artifact can be exported to PDF via the **in-browser print** feature (`CTRL/CMD + P`). 

While `paged` (and `plain`) documents are print-ready, you'll need a few additional steps to save your `slides` document as PDF.  
Please refer to [Reveal's instructions](https://revealjs.com/pdf-export/#instructions) to learn how to do so.