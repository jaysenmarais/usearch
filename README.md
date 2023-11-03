<h1 align="center">USearch</h1>
<h3 align="center">
Smaller & <a href="https://www.unum.cloud/blog/2023-11-07-scaling-vector-search-with-intel">Faster</a> Single-File<br/>
Similarity Search Engine for <a href="https://github.com/ashvardanian/simsimd">Vectors</a> & 🔜 <a href="https://github.com/ashvardanian/stringzilla">Texts</a>
</h3>
<br/>

<p align="center">
<a href="https://discord.gg/A6wxt6dS9j"><img height="25" src="https://github.com/unum-cloud/.github/raw/main/assets/discord.svg" alt="Discord"></a>
&nbsp;&nbsp;&nbsp;
<a href="https://www.linkedin.com/company/unum-cloud/"><img height="25" src="https://github.com/unum-cloud/.github/raw/main/assets/linkedin.svg" alt="LinkedIn"></a>
&nbsp;&nbsp;&nbsp;
<a href="https://twitter.com/unum_cloud"><img height="25" src="https://github.com/unum-cloud/.github/raw/main/assets/twitter.svg" alt="Twitter"></a>
&nbsp;&nbsp;&nbsp;
<a href="https://unum.cloud/post"><img height="25" src="https://github.com/unum-cloud/.github/raw/main/assets/blog.svg" alt="Blog"></a>
&nbsp;&nbsp;&nbsp;
<a href="https://github.com/unum-cloud/usearch"><img height="25" src="https://github.com/unum-cloud/.github/raw/main/assets/github.svg" alt="GitHub"></a>
</p>

<p align="center">
Spatial • Binary • Probabilistic • User-Defined Metrics
<br/>
<a href="https://unum-cloud.github.io/usearch/cpp">C++ 11</a> •
<a href="https://unum-cloud.github.io/usearch/python">Python 3</a> •
<a href="https://unum-cloud.github.io/usearch/javascript">JavaScript</a> •
<a href="https://unum-cloud.github.io/usearch/java">Java</a> •
<a href="https://unum-cloud.github.io/usearch/rust">Rust</a> •
<a href="https://unum-cloud.github.io/usearch/c">C 99</a> •
<a href="https://unum-cloud.github.io/usearch/objective-c">Objective-C</a> •
<a href="https://unum-cloud.github.io/usearch/swift">Swift</a> •
<a href="https://unum-cloud.github.io/usearch/csharp">C#</a> •
<a href="https://unum-cloud.github.io/usearch/golang">GoLang</a> •
<a href="https://unum-cloud.github.io/usearch/wolfram">Wolfram</a>
<br/>
Linux • MacOS • Windows • iOS • WebAssembly
</p>

<div align="center">
<a href="https://pypi.org/project/usearch/"> <img alt="PyPI" src="https://img.shields.io/pypi/dm/usearch?label=PyPi%20pulls"> </a>
<a href="https://www.npmjs.com/package/usearch"> <img alt="NPM" src="https://img.shields.io/npm/dy/usearch?label=NPM%20pulls"> </a>
<a href="https://crates.io/crates/usearch"> <img alt="Crate" src="https://img.shields.io/crates/d/usearch?label=Crate%20pulls"> </a>
<a href="https://www.nuget.org/packages/Cloud.Unum.USearch"> <img alt="NuGet" src="https://img.shields.io/nuget/dt/Cloud.Unum.USearch?label=NuGet%20pulls"> </a>
<a href="https://central.sonatype.com/artifact/cloud.unum/usearch/overview"> <img alt="Maven" src="https://img.shields.io/nexus/r/cloud.unum/usearch?server=https%3A%2F%2Fs01.oss.sonatype.org%2F&label=Maven%20version"> </a>
<a href="https://hub.docker.com/r/unum/usearch"> <img alt="Docker" src="https://img.shields.io/docker/pulls/unum/usearch?label=Docker%20pulls"> </a>
<img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/unum-cloud/usearch?label=Repo%20size">
</div>

---

- ✅ [20x faster than][faster-than-faiss] [FAISS][faiss] implementation of [HNSW algorithm][hnsw-algorithm].
- ✅ Simple and extensible [single C++11 header][usearch-header] implementation.
- ✅ Compatible with a dozen programming languages out of the box.
- ✅ [SIMD][simd]-optimized and [user-defined metrics](#user-defined-functions) with JIT compilation.
- ✅ Hardware-agnostic `f16` & `i8` - [half-precision & quarter-precision support](#memory-efficiency-downcasting-and-quantization).
- ✅ [View large indexes from disk](#serving-index-from-disk) without loading into RAM.
- ✅ Heterogeneous lookups, renaming/relabeling, and on-the-fly deletions.
- ✅ Variable dimensionality vectors for unique applications, including search over compressed data.
- ✅ Binary Tanimoto and Sorensen coefficients for [Genomics and Chemistry applications](#usearch--rdkit--molecular-search).
- ✅ Space-efficient point-clouds with `uint40_t`, accommodating 4B+ size.
- ✅ Compatible with OpenMP and custom "executors" for fine-grained control over CPU utilization.
- ✅ Near-real-time [clustering and sub-clustering](#clustering) for Tens or Millions of clusters.
- ✅ [Semantic Search](#usearch--ai--multi-modal-semantic-search) and [Joins](#joins).

[faiss]: https://github.com/facebookresearch/faiss
[usearch-header]: https://github.com/unum-cloud/usearch/blob/main/include/usearch/index.hpp
[obscure-use-cases]: https://ashvardanian.com/posts/abusing-vector-search
[hnsw-algorithm]: https://arxiv.org/abs/1603.09320
[simd]: https://en.wikipedia.org/wiki/Single_instruction,_multiple_data
[faster-than-faiss]: https://www.unum.cloud/blog/2023-11-07-scaling-vector-search-with-intel

## Comparison with FAISS

FAISS is a widely recognized standard for high-performance vector search engines.
USearch and FAISS both employ the same HNSW algorithm, but they differ significantly in their design principles.
USearch is compact and broadly compatible without sacrificing performance, primarily focusing on user-defined metrics and fewer dependencies.

|                                              |                         FAISS |                        USearch |            Improvement |
| :------------------------------------------- | ----------------------------: | -----------------------------: | ---------------------: |
| Indexing time ⁰                              |                               |                                |                        |
| 100 Million 96d `f32`, `f16`, `i8` vectors   |           2.6 h, 2.6 h, 2.6 h |            0.3 h, 0.2 h, 0.2 h | __9.6x, 10.4x, 10.7x__ |
| 100 Million 1536d `f32`, `f16`, `i8` vectors |           5.0 h, 4.1 h, 3.8 h |            2.1 h, 1.1 h, 0.8 h |    __2.3x 3.6x, 4.4x__ |
|                                              |                               |                                |                        |
| Codebase length ¹                            | 84 K [SLOC][sloc] in `faiss/` | 3 K [SLOC][sloc] in `usearch/` |           maintainable |
| Supported metrics ²                          |               9 fixed metrics |       any user-defined metrics |             extendible |
| Supported languages ³                        |                   C++, Python |                   10 languages |               portable |
| Supported ID types ⁴                         |                32-bit, 64-bit |         32-bit, 40-bit, 64-bit |              efficient |
| Required dependencies ⁵                      |                  BLAS, OpenMP |                              - |           light-weight |
| Bindings ⁶                                   |                          SWIG |                         Native |            low-latency |

[sloc]: https://en.wikipedia.org/wiki/Source_lines_of_code

> ⁰ [Tested][intel-benchmarks] on Intel Sapphire Rapids, with the simplest inner-product distance, equivalent recall, and memory consumption while also providing far superior search speed.
> ¹ A shorter codebase makes the project easier to maintain and audit.
> ² User-defined metrics allow you to customize your search for various applications, from GIS to creating custom metrics for composite embeddings from multiple AI models or hybrid full-text and semantic search.
> ³ With USearch, you can reuse the same preconstructed index in various programming languages.
> ⁴ The 40-bit integer allows you to store 4B+ vectors without allocating 8 bytes for every neighbor reference in the proximity graph.
> ⁵ Lack of obligatory dependencies makes USearch much more portable.
> ⁶ Native bindings introduce lower call latencies than more straightforward approaches.

[intel-benchmarks]: https://www.unum.cloud/blog/2023-11-07-scaling-vector-search-with-intel

Base functionality is identical to FAISS, and the interface must be familiar if you have ever investigated Approximate Nearest Neighbors search:

```py
$ pip install numpy usearch

import numpy as np
from usearch.index import Index

index = Index(ndim=3)

vector = np.array([0.2, 0.6, 0.4])
index.add(42, vector)

matches = index.search(vector, 10)

assert matches[0].key == 42
assert matches[0].distance <= 0.001
assert np.allclose(index[42], vector)
```

More settings are always available, and the API is designed to be as flexible as possible.

```py
index = Index(
    ndim=3, # Define the number of dimensions in input vectors
    metric='cos', # Choose 'l2sq', 'haversine' or other metric, default = 'ip'
    dtype='f32', # Quantize to 'f16' or 'i8' if needed, default = 'f32'
    connectivity=16, # Optional: Limit number of neighbors per graph node
    expansion_add=128, # Optional: Control the recall of indexing
    expansion_search=64, # Optional: Control the quality of the search
)
```

## User-Defined Functions

While most vector search packages concentrate on just a few metrics - "Inner Product distance" and "Euclidean distance," USearch extends this list to include any user-defined metrics.
This flexibility allows you to customize your search for various applications, from computing geospatial coordinates with the rare [Haversine][haversine] distance to creating custom metrics for composite embeddings from multiple AI models.

![USearch: Vector Search Approaches](https://github.com/unum-cloud/usearch/blob/main/assets/usearch-approaches-white.png?raw=true)

Unlike older approaches indexing high-dimensional spaces, like KD-Trees and Locality Sensitive Hashing, HNSW doesn't require vectors to be identical in length.
They only have to be comparable.
So you can apply it in [obscure][obscure] applications, like searching for similar sets or fuzzy text matching, using [GZip][gzip-similarity] as a distance function.

> Read more about [JIT and UDF in USearch Python SDK](https://unum-cloud.github.io/usearch/python#user-defined-metrics-and-jit-in-python).

[haversine]: https://ashvardanian.com/posts/abusing-vector-search#geo-spatial-indexing
[obscure]: https://ashvardanian.com/posts/abusing-vector-search
[gzip-similarity]: https://twitter.com/LukeGessler/status/1679211291292889100?s=20

## Memory Efficiency, Downcasting, and Quantization

Training a quantization model and dimension-reduction is a common approach to accelerate vector search.
Those, however, are only sometimes reliable, can significantly affect the statistical properties of your data, and require regular adjustments if your distribution shifts.

![USearch uint40_t support](https://github.com/unum-cloud/usearch/blob/main/assets/usearch-neighbor-types.png?raw=true)

Instead, we have focused on high-precision arithmetic over low-precision downcasted vectors.
The same index, and `add` and `search` operations will automatically down-cast or up-cast between `f32_t`, `f16_t`, `f64_t`, and `i8_t` representations, even if the hardware doesn't natively support it.
Continuing the topic of memory efficiency, we provide a `uint40_t` to allow collection with over 4B+ vectors without allocating 8 bytes for every neighbor reference in the proximity graph.

## Serialization & Serving `Index` from Disk

USearch supports multiple forms of serialization:

- Into a __file__ defined with a path.
- Into a __stream__ defined with a callback, serializing or reconstructing incrementally.
- Into a __buffer__ of fixed length or a memory-mapped file that supports random access.

The latter allows you to serve indexes from external memory, enabling you to optimize your server choices for indexing speed and serving costs.
This can result in __20x cost reduction__ on AWS and other public clouds.

```py
index.save("index.usearch")

loaded_copy = index.load("index.usearch")
view = Index.restore("index.usearch", view=True)

other_view = Index(ndim=..., metric=CompiledMetric(...))
other_view.view("index.usearch")
```

## Exact vs. Approximate Search

Approximate search methods, such as HNSW, are predominantly used when an exact brute-force search becomes too resource-intensive.
This typically occurs when you have millions of entries in a collection.
For smaller collections, we offer a more direct approach with the `search` method.

```py
from usearch.index import search, MetricKind, Matches, BatchMatches
import numpy as np

# Generate 10'000 random vectors with 1024 dimensions
vectors = np.random.rand(10_000, 1024).astype(np.float32)
vector = np.random.rand(1024).astype(np.float32)

one_in_many: Matches = search(vectors, vector, 50, MetricKind.L2sq, exact=True)
many_in_many: BatchMatches = search(vectors, vectors, 50, MetricKind.L2sq, exact=True)
```

If you pass the `exact=True` argument, the system bypasses indexing altogether and performs a brute-force search through the entire dataset using SIMD-optimized similarity metrics from [SimSIMD](https://github.com/ashvardanian/simsimd).
When compared to FAISS's `IndexFlatL2` in Google Colab, __[USearch may offer up to a 20x performance improvement](https://github.com/unum-cloud/usearch/issues/176#issuecomment-1666650778)__:

- `faiss.IndexFlatL2`: __55.3 ms__.
- `usearch.index.search`: __2.54 ms__.

## `Indexes` for Multi-Index Lookups

For larger workloads targeting billions or even trillions of vectors, parallel multi-index lookups become invaluable.
Instead of constructing one extensive index, you can build multiple smaller ones and view them together.

```py
from usearch.index import Indexes

multi_index = Indexes(
    indexes: Iterable[usearch.index.Index] = [...],
    paths: Iterable[os.PathLike] = [...],
    view: bool = False,
    threads: int = 0,
)
multi_index.search(...)
```

## Clustering

Once the index is constructed, it can cluster entries much faster than using a separate clustering algorithm implementation.
Essentially, the `Index` itself can be seen as a clustering, allowing iterative deepening.

```py
clustering = index.cluster(
    min_count=10, # Optional
    max_count=15, # Optional
    threads=..., # Optional
)

# Get the clusters and their sizes
centroid_keys, sizes = clustering.centroids_popularity

# Use Matplotlib to draw a histogram
clustering.plot_centroids_popularity()

# Export a NetworkX graph of the clusters
g = clustering.network

# Get members of a specific cluster
first_members = clustering.members_of(centroid_keys[0])

# Deepen into that cluster, splitting it into more parts, all the same arguments supported
sub_clustering = clustering.subcluster(min_count=..., max_count=...)
```

The resulting clustering isn't identical to K-Means or other conventional approaches but serves the same purpose.
Alternatively, using Scikit-Learn on a 1 Million point dataset, one may expect queries to take anywhere from minutes to hours, depending on the number of clusters you want to highlight.
For 50'000 clusters, the performance difference between USearch and conventional clustering methods may easily reach 100x.

## Joins, One-to-One, One-to-Many, and Many-to-Many Mappings

One of the big questions these days is how AI will change the world of databases and data management.
Most databases are still struggling to implement high-quality fuzzy search, and the only kind of joins they know are deterministic.
A `join` differs from searching for every entry, requiring a one-to-one mapping banning collisions among separate search results.

| Exact Search | Fuzzy Search | Semantic Search ? |
| :----------: | :----------: | :---------------: |
|  Exact Join  | Fuzzy Join ? | Semantic Join ??  |

Using USearch, one can implement sub-quadratic complexity approximate, fuzzy, and semantic joins.
This can be useful in any fuzzy-matching tasks common to Database Management Software.

```py
men = Index(...)
women = Index(...)
pairs: dict = men.join(women, max_proposals=0, exact=False)
```

> Read more in the post: [Combinatorial Stable Marriages for Semantic Search 💍](https://ashvardanian.com/posts/searching-stable-marriages)

## Functionality

By now, the core functionality is supported across all bindings.
Broader functionality is ported per request.

|                         | C++ 11 | Python 3 | C 99  | Java  | JavaScript | Rust  | GoLang | Swift |
| :---------------------- | :----: | :------: | :---: | :---: | :--------: | :---: | :----: | :---: |
| Add, search             |   ✅    |    ✅     |   ✅   |   ✅   |     ✅      |   ✅   |   ✅    |   ✅   |
| Save, load, view        |   ✅    |    ✅     |   ✅   |   ✅   |     ✅      |   ✅   |   ✅    |   ✅   |
| User-defined metrics    |   ✅    |    ✅     |   ✅   |   ❌   |     ❌      |   ❌   |   ❌    |   ❌   |
| Joins                   |   ✅    |    ✅     |   ❌   |   ❌   |     ❌      |   ❌   |   ❌    |   ❌   |
| Variable-length vectors |   ✅    |    ❌     |   ❌   |   ❌   |     ❌      |   ❌   |   ❌    |   ❌   |
| 4B+ capacities          |   ✅    |    ❌     |   ❌   |   ❌   |     ❌      |   ❌   |   ❌    |   ❌   |

## Application Examples

### USearch + AI = Multi-Modal Semantic Search

[![USearch Semantic Image Search](https://github.com/ashvardanian/usearch-images/raw/main/assets/usearch-images-slow.gif)](https://github.com/ashvardanian/usearch-images)

AI has a growing number of applications, but one of the coolest classic ideas is to use it for Semantic Search.
One can take an encoder model, like the multi-modal [UForm](https://github.com/unum-cloud/uform), and a web-programming framework, like UCall, and build a text-to-image search platform in just 20 lines of Python.

```python
import ucall
import uform
import usearch

import numpy as np
import PIL as pil

server = ucall.Server()
model = uform.get_model('unum-cloud/uform-vl-multilingual')
index = usearch.index.Index(ndim=256)

@server
def add(key: int, photo: pil.Image.Image):
    image = model.preprocess_image(photo)
    vector = model.encode_image(image).detach().numpy()
    index.add(key, vector.flatten(), copy=True)

@server
def search(query: str) -> np.ndarray:
    tokens = model.preprocess_text(query)
    vector = model.encode_text(tokens).detach().numpy()
    matches = index.search(vector.flatten(), 3)
    return matches.keys

server.run()
```

A more complete [demo with Streamlit is available on GitHub](https://github.com/ashvardanian/usearch-images).
We have pre-processed some commonly used datasets, cleaned the images, produced the vectors, and pre-built the index.

| Dataset                             |            Modalities | Images |                              Download |
| :---------------------------------- | --------------------: | -----: | ------------------------------------: |
| [Unsplash][unsplash-25k-origin]     | Images & Descriptions |   25 K | [HuggingFace / Unum][unsplash-25k-hf] |
| [Conceptual Captions][cc-3m-origin] | Images & Descriptions |    3 M |        [HuggingFace / Unum][cc-3m-hf] |
| [Arxiv][arxiv-2m-origin]            |    Titles & Abstracts |    2 M |     [HuggingFace / Unum][arxiv-2m-hf] |

[unsplash-25k-origin]: https://github.com/unsplash/datasets
[cc-3m-origin]: https://huggingface.co/datasets/conceptual_captions
[arxiv-2m-origin]: https://www.kaggle.com/datasets/Cornell-University/arxiv

[unsplash-25k-hf]: https://huggingface.co/datasets/unum-cloud/ann-unsplash-25k
[cc-3m-hf]: https://huggingface.co/datasets/unum-cloud/ann-cc-3m
[arxiv-2m-hf]: https://huggingface.co/datasets/unum-cloud/ann-arxiv-2m

### USearch + RDKit = Molecular Search

Comparing molecule graphs and searching for similar structures is expensive and slow.
It can be seen as a special case of the NP-Complete Subgraph Isomorphism problem.
Luckily, domain-specific approximate methods exist.
The one commonly used in Chemistry is to generate structures from [SMILES][smiles] and later hash them into binary fingerprints.
The latter are searchable with binary similarity metrics, like the Tanimoto coefficient.
Below is an example using the RDKit package.

```python
from usearch.index import Index, MetricKind
from rdkit import Chem
from rdkit.Chem import AllChem

import numpy as np

molecules = [Chem.MolFromSmiles('CCOC'), Chem.MolFromSmiles('CCO')]
encoder = AllChem.GetRDKitFPGenerator()

fingerprints = np.vstack([encoder.GetFingerprint(x) for x in molecules])
fingerprints = np.packbits(fingerprints, axis=1)

index = Index(ndim=2048, metric=MetricKind.Tanimoto)
keys = np.arange(len(molecules))

index.add(keys, fingerprints)
matches = index.search(fingerprints, 10)
```

[smiles]: https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system
[rdkit-fingerprints]: https://www.rdkit.org/docs/RDKit_Book.html#additional-information-about-the-fingerprints

### USearch + POI Coordinates = GIS Applications... on iOS?

[![USearch Maps with SwiftUI](https://github.com/ashvardanian/SwiftVectorSearch/raw/main/USearch+SwiftUI.gif)](https://github.com/ashvardanian/SwiftVectorSearch)

With Objective-C and Swift iOS bindings, USearch can be easily used in mobile applications.
The [SwiftVectorSearch](https://github.com/ashvardanian/SwiftVectorSearch) project illustrates how to build a dynamic, real-time search system on iOS.
In this example, we use 2-dimensional vectors—encoded as latitude and longitude—to find the closest Points of Interest (POIs) on a map.
The search is based on the Haversine distance metric but can easily be extended to support high-dimensional vectors.

## Integrations

- [x] GPTCache: [Python](https://github.com/zilliztech/GPTCache/releases/tag/0.1.29).
- [x] LangChain: [Python](https://github.com/langchain-ai/langchain/releases/tag/v0.0.257) and [JavaScript](https://github.com/hwchase17/langchainjs/releases/tag/0.0.125).
- [x] ClickHouse: [C++](https://github.com/ClickHouse/ClickHouse/pull/53447).
- [x] Microsoft Semantic Kernel: [Python](https://github.com/microsoft/semantic-kernel/releases/tag/python-0.3.9.dev) and C#.
- [x] LanternDB: [C++](https://github.com/lanterndata/lantern) and [Rust](https://github.com/lanterndata/lantern_extras).

## Citations

```txt
@software{Vardanian_USearch_2023,
doi = {10.5281/zenodo.7949416},
author = {Vardanian, Ash},
title = {{USearch by Unum Cloud}},
url = {https://github.com/unum-cloud/usearch},
version = {2.8.6},
year = {2023},
month = oct,
}
```
