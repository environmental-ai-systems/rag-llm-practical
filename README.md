# Machine learning: a hands-on practical

A small set of browser based teaching demos for a one day practical: image recognition in the morning, language models and retrieval in the afternoon. Everything runs client side in a single HTML file each. There is no build step, no server, and nothing a student loads or types leaves their browser.

**Live site:** https://environmental-ai-systems.github.io/rag-llm-practical/

## The demos

### Morning: seeing

1. **Image Classifier** (`image-classifier.html`). Show a real convolutional neural network (ResNet-50) a photo (hot-air balloon, airliner, geyser, plus atmospheric scenes: a snow-covered volcano, cloud, aurora, Earth from space) and watch it turn the pixels into a ranked spread of probabilities over its 1,000 everyday labels rather than a single answer. It confidently recognises the ordinary objects, but has no label for the out-of-domain atmospheric scenes (and even fumbles the snowy volcano, which looks nothing like its training photos), which is the point. Students can blur, rotate, flip, greyscale or pixelate the picture, adjust how many labels to show, or drop in their own image, and watch the guess move. Teaches: pixels to labels, convolutional networks, probability distributions and confidence, a fixed label vocabulary, why domain-specific models need domain-specific training, and robustness to changes in the input. Pairs with a lecture on CNNs.

2. **Build a Filter by Hand** (`convolution.html`). A hands-on coding exercise that opens up the classifier. A CNN is built from one repeated operation, sliding a small filter over the image, and here students edit the actual JavaScript convolution loop and the nine numbers in a 3x3 filter, then watch the resulting feature map render live. Preset filters (edge, sharpen, blur, Sobel, emboss) show classic kernels; the equivalent NumPy Python is shown read-only alongside. No model download, pure browser JavaScript. Teaches: convolution, filters/kernels, feature maps, and how hand-picked filters relate to the ones a CNN learns. Reinforces the CNN lecture with real code.

### Afternoon: language and retrieval

3. **Next-Token Predictor** (`next-word.html`). Type a few words and watch a real, small language model (distilGPT-2) predict what comes next as a spread of probabilities rather than a single answer. Adjust the temperature, sample or take the most likely token, and let it write one token at a time. Teaches: tokens, probability distributions, temperature, and autoregressive generation. Echoes the morning: same "predict a distribution" idea, now over words instead of labels.

4. **RAG Playground** (`rag-playground.html`). Split a document into chunks, then ask a question and see which passages a system retrieves, by keyword (TF-IDF), by meaning (embeddings), and across a metadata tagged repository. Includes a live token inspector and switchable source documents. Teaches: chunking and overlap, keyword vs semantic retrieval, relevance scores, and metadata filtering.

The landing page (`index.html`) links to all four and is the intended starting point.

## Running it

Open `index.html` in any modern browser, or host the whole folder as static files (GitHub Pages works well and is free). To publish with GitHub Pages: repository Settings, then Pages, set Source to "Deploy from a branch", Branch to `main`, folder `/ (root)`, and Save.

Keep `index.html` at the top level of the repository so it loads at the bare URL.

## What needs the internet

The sample photos and image transforms in Demo 1, and the keyword and metadata repository search in Demo 3, run fully offline. The image classifier, the next token predictor, the semantic search, the token inspector, and the web fonts each fetch something from a public CDN the first time they are used, then cache it for later. Plan for that first download on shared classroom wifi, or pre-load before the session.

## More detail

See `TOOLS.md` for the full list of libraries, models, fonts, hosting, and licences.
