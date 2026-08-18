# Large files in a pull request

Do not commit experimental arrays, generated HTML, or notebook widget state. Those belong on public data hosting or in a generated documentation build.

## Arrays and data files

Upload the data to [bobleesj/quantem-data](https://huggingface.co/datasets/bobleesj/quantem-data) and load it from the tutorial helper at run time. That keeps the repository and the wheel small enough for a microscope PC to clone and install.

Upload steps, bucket layout, and `meta.json` sidecars: [I/O guide](https://electronmicroscopy.github.io/quantem.widget/api/io.html).

## Generated HTML

Documentation builds already generate the examples. Keep generated HTML out of the repository. Export a shareable page locally with `quantem html` or `widget.export_html(...)`.

Protocol: [HTML export](https://electronmicroscopy.github.io/quantem.widget/api/html-export.html).

## Notebooks

Keep widgets at `save_state=False` so Jupyter does not embed the pixel buffers. For a GitHub-readable copy, write a separate notebook without widget state:

```bash
quantem github tutorial_github.ipynb --no-execute
```

That command replaces live widgets with a compressed image of the UI. Do not run it in place on the canonical tutorial notebook.

Commands: [CLI](https://electronmicroscopy.github.io/quantem.widget/cli.html).
Sharing paths: [notebook sharing](https://electronmicroscopy.github.io/quantem.widget/api/html-export.html).
