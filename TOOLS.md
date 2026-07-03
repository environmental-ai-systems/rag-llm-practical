# Tools and credits

This repository is a small set of browser based teaching demos for a one day practical on machine learning: image recognition in the morning, language models and retrieval in the afternoon. This document lists everything the demos rely on, so anyone reading the code (or the class) knows what is doing the work.

## How it is built

Every demo is a single, self contained HTML file. There is no build step, no bundler, and no framework. Each page is plain HTML, CSS, and vanilla JavaScript, which means you can open any file directly in a browser or host the whole folder as static files.

Files in the repository:

- `index.html`: the landing page that links to each demo.
- `image-classifier.html`: Demo 1 (morning), the image classifier (a convolutional network labelling a photo, with live image transforms).
- `convolution.html`: Demo 2 (morning), "Build a Filter by Hand" (an editable 3x3 filter and convolution loop, with a live feature-map canvas).
- `next-word.html`: Demo 3 (afternoon), the next token predictor (a small language model running in the browser).
- `rag-playground.html`: Demo 4 (afternoon), the retrieval playground (chunking, keyword and semantic search, and a metadata filtered repository search).

## Libraries

**Transformers.js** (`@huggingface/transformers`, version 4.2.0) is the only external code library. It runs machine learning models directly in the browser using ONNX Runtime compiled to WebAssembly. It is loaded straight from the jsDelivr CDN as an ES module, so there is nothing to install. It powers the image classification, the next word predictions, the sentence embeddings, and the tokenizers.

Everything else is written from scratch in the page, with no library:

- Live image transforms (brightness, blur, pixelate, rotate, flip, greyscale) drawn with the HTML canvas (Demo 1).
- The 3x3 convolution itself, run on the pixel brightness with the HTML canvas, including live execution of the student's own edited JavaScript (Demo 2). This demo needs no model and no library at all.
- Fixed size chunking with adjustable overlap (Demo 4).
- Keyword relevance using TF-IDF vectors compared by cosine similarity (Demo 4).
- The softmax, top-k selection, and temperature sampling used to turn the model's raw scores into next token predictions (Demo 3).

## Models

These are downloaded from the Hugging Face CDN the first time a feature that needs them is used, then cached by the browser for later visits. None of them run on a server; they run on the student's own machine.

| Model | Used in | Job | Rough size |
| --- | --- | --- | --- |
| `Xenova/resnet-50` | Demo 1 | Labels a photo with one of 1,000 ImageNet classes | about 25 MB |
| `Xenova/distilgpt2` | Demo 3 | Predicts the next token | about 50 MB |
| `Xenova/all-MiniLM-L6-v2` | Demo 4, semantic mode | Turns text into meaning vectors (embeddings) | about 25 MB |
| `Xenova/gpt-4` (tokenizer only) | Demo 4, token inspector | Splits text into GPT-4 style tokens | very small |

ResNet-50 is a classic 50 layer convolutional neural network, trained on the ImageNet dataset (about 1.2 million photos across 1,000 categories). It is a natural companion to a lecture on CNNs. distilGPT-2 is a compact, distilled version of GPT-2 (82 million parameters), deliberately small and dated so its mistakes are easy to see and discuss. all-MiniLM-L6-v2 is a widely used sentence embedding model that produces a 384 number vector per passage.

The seven sample photos in Demo 1 mix everyday objects the model knows well (a hot-air balloon, an Airbus A380 airliner, an erupting geyser) with atmospheric-science scenes it has no label for (a snow-covered volcano, a cumulonimbus cloud, an aurora, Earth from space), so students can see it succeed confidently on the former and flounder on the latter. Sources are Wikimedia Commons and NASA: Mount St. Helens (USGS), Old Faithful, and the cloud, aurora and "Blue Marble" Earth images (NASA / US public domain); the hot-air balloon and Airbus A380 are from Wikimedia Commons (see each file page for its specific licence). All are embedded directly in the HTML as base64, so the demo needs no network for the pictures themselves, only for the model on first use.

## Fonts

Three typefaces are loaded from Google Fonts:

- **Space Grotesk** for headings.
- **IBM Plex Sans** for body text.
- **IBM Plex Mono** for code, tokens, and numbers.

## Hosting

The site is designed for **GitHub Pages**, which serves the static files for free. Because there is no backend, it will run just as happily from any static host, or from a file opened directly on a laptop.

## What needs the internet, and what does not

- The whole convolution playground (Demo 2) runs offline with no network at all. So do the sample photos and image transforms in Demo 1, and the keyword and metadata repository search in Demo 4.
- The image classifier model (Demo 1), the next token predictor (Demo 3), the semantic search and token inspector (Demo 4), and the web fonts all fetch something from a CDN the first time they are used. After that first load, the models and fonts are cached and work offline.

## Privacy

Nothing a student types is sent anywhere. All model inference happens locally in the browser. The only network traffic is the one time download of the libraries, models, and fonts from their public CDNs.

## Licences

Each third party asset is provided under its own licence by its original authors:

- Transformers.js: Apache 2.0 (Hugging Face).
- ResNet-50, distilGPT-2 and all-MiniLM-L6-v2: see their model cards on the Hugging Face Hub for the applicable licences.
- Sample photos (Demo 1): from Wikimedia Commons and NASA (USGS, NPS, NASA public-domain images, plus the hot-air balloon and Airbus A380 from Commons under their own licences). See each file's page on Wikimedia Commons for the specific licence.
- Space Grotesk and IBM Plex: SIL Open Font License.

This list is a convenience, not legal advice. Check each source for the current terms before reusing anything beyond the classroom.
