# Large files in a pull request

Do not commit real arrays, baked HTML, or notebook widget state. Those belong on public data hosting or in a generated docs build.

## Arrays and data files

Upload the data to [bobleesj/quantem-data](https://huggingface.co/datasets/bobleesj/quantem-data) and load it from the tutorial helper at run time. Keep the repo and the wheel small so a microscope PC can clone and install.

Upload steps, bucket layout, and `meta.json` sidecars: [I/O guide](https://electronmicroscopy.github.io/quantem.widget/api/io.html).

## Baked HTML

Docs already bake examples at build time. Keep generated HTML out of the repository. Export a shareable page locally with `quantem html` or `widget.export_html(...)`.

Protocol: [HTML export](https://electronmicroscopy.github.io/quantem.widget/api/html-export.html).

## Notebooks

Keep widgets at `save_state=False` so Jupyter does not embed the pixel buffers. For a GitHub-readable copy, write a separate stripped notebook:

```bash
quantem github tutorial_github.ipynb --no-execute
```

That command replaces live widgets with a compressed picture of the UI. Do not run it in place on the canonical tutorial notebook.

Commands: [CLI](https://electronmicroscopy.github.io/quantem.widget/cli.html).
Sharing paths: [notebook sharing](https://electronmicroscopy.github.io/quantem.widget/api/html-export.html).
