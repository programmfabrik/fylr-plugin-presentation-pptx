# fylr-plugin-presentation-pptx

Export plugin for **fylr**: downloads the objects of a collection as a PowerPoint presentation (PPTX).

## How it works

The plugin extends the presentation download managers in the webfrontend with a "Powerpoint..." entry, which offers a template (black/white, 16:9 or 4:3) and an image quality.

The export itself runs in two passes through the same `export/create_pptx` callback in [server/presentation_pptx_fylr.py](server/presentation_pptx_fylr.py):

1. Without a `plugin_action`, it hides the exported files and announces the `.pptx` file it is going to produce.
2. Called back with `plugin_action: produce?create_pptx`, it downloads the exported images from the export API, builds the deck with [python-pptx](https://python-pptx.readthedocs.io) and writes it to stdout.

Assets with no usable image version are rendered as a placeholder image ([placeholders/](placeholders/)) captioned with the asset info.

### Server requirements

The `python3` exec service must have `python-pptx`, `Pillow` and `requests` available.

