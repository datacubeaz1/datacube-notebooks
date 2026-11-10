# DataCube notebooks

Starter notebooks and datasets for the DataCube courses and bootcamps. The
platform opens them inside the lesson page (JupyterLite, Python in the
browser) and offers "Open in Colab" as a backup.

## Layout

```
content/
  <lesson>.ipynb        one notebook per task or project, at this level
  datasets/*.csv        datasets, read as  pd.read_csv("datasets/<file>.csv")
```

- Keep notebooks flat in `content/` so `datasets/...` works the same on the
  site and in Colab. A lesson in the admin panel only stores the notebook's
  file name, e.g. `modul11-tarif.ipynb`.
- The first code cell of every notebook picks the data location
  (`sys.platform == "emscripten"` on the site, GitHub raw URL in Colab) —
  copy it from `modul11-tarif.ipynb`.
- This repository is public: never commit solutions or answer keys.
- Files on GitHub are limited to 100 MB; keep datasets small.

## Build locally

```bash
pip install -r requirements.txt
jupyter lite build --contents content --output-dir dist
python -m http.server --directory dist 8100   # http://localhost:8100/lab/
```

## Publishing (Cloudflare Pages)

Create a Pages project from this repository with:

| Setting | Value |
|---|---|
| Build command | `pip install -r requirements.txt && jupyter lite build --contents content --output-dir dist` |
| Build output directory | `dist` |
| Environment variable | `PYTHON_VERSION` = `3.12` |

Every push to `main` rebuilds the lab. The platform's `NEXT_PUBLIC_LAB_URL`
points at the Pages (or custom-domain) address.
