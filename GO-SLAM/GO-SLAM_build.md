# GO-SLAM_build

## GO-SLAM

### 基础

#### docker build

（forked，下载到本地，更新后 `push`，服务器再 `pull` 进行更新）`nerf-3dgs-benchmark\GO-SLAM\.devcontainer`：修改部分配置

将所需下载资源提前下载到本地，并通过 **WinSCP** 软件链接到服务器，放于 `nerf-3dgs-benchmark\GO-SLAM`（容器目录 **/workspace** 对应到服务器中的目录）

**clone**（服务器上clone，容器的话是root权限不方便）：

```bash
git clone --recursive https://github.com/iis-esslingen/GO-SLAM.git
```



**vsc+docker插件**：工作空间中build docker

#### GO-SLAM构建

```bash
DISPLAY_EXPORT="export DISPLAY=:0"
```



**conda环境构建**：iis-esslingen版升级了cuda版本，但environment.yaml加入了大量随必要依赖安装的不必显式写出的内容，导致mamba解析缓慢，改版如下：

```bash
name: go-slam
channels:
  - pytorch
  - nvidia
  - conda-forge
  - defaults
dependencies:
  - python=3.9
  - pytorch
  - torchvision
#   - torchaudio
  - pytorch-cuda=12.1
  # - _libgcc_mutex
  # - _openmp_mutex
  # - blas
  # - brotli
  # - brotlipy
  # - bzip2
  # - ca-certificates
  # - certifi
  # - cffi
  # - cryptography
  # - cycler
  # - dbus
  - embree
  # - expat
  # - ffmpeg
  # - fontconfig
  # - fonttools
  # - freetype
  # - giflib
  # - glib
  # - gmp
  # - gnutls
  # - gst-plugins-base
  # - gstreamer
  # - icu
  # - idna
  # - jpeg
  # - kiwisolver
  # - lame
  # - lcms2
  # - ld_impl_linux-64
  # - libffi
  # - libgcc-ng
  # - libiconv
  # - libnsl
  # - libpng
  # - libstdcxx-ng
  # - libtiff
  # - libuuid
  # - libuv
  # - libwebp
  # - libwebp-base
  # - libxcb
  # - libxml2
  # - libzlib
  # - llvm-openmp
  # - lz4-c
  - matplotlib
  # - matplotlib-base
  # - mkl
  # - mkl-service
  # - mkl_fft
  # - mkl_random
  # - munkres
  # - ncurses
  # - nettle
  - ninja
  # - numpy-base
  # - olefile
  # - openh264
  # - openssl
  # - pcre
  - pillow
  - pip
  # - pycparser
  - pyembree
  # - pyopenssl
  # - pyparsing
  # - pyqt
  # - pysocks
  # - python-dateutil
  # - python_abi
  # - pytorch-mutex
  # - qt
  # - readline
  # - requests
  # - setuptools
  # - sip
  # - six
  # - sqlite
  # - tbb
  # - tk
  # - tornado
  # - typing_extensions
  # - wheel
  # - xz
  # - zlib
  # - zstd
  - pip:
    # - addict
    # - anyio
    # - argon2-cffi
    # - argon2-cffi-bindings
    # - argparse
    # - attrs
    # - babel
    # - backcall
    # - beautifulsoup4
    # - bleach
    # - charset-normalizer
    # - cloudpickle
    # - colorama
    # - dask
    # - debugpy
    # - decorator
    # - defusedxml
    # - deprecation
    # - entrypoints
    # - filelock
    # - fsspec
    # - gdown
    # - imageio
    # - imath
    # - importlib-metadata
    # - importlib-resources
    - ipykernel
    # - ipython
    # - ipython-genutils
    # - ipywidgets
    # - jedi
    # - jinja2
    # - joblib
    # - json5
    # - jsonschema
    # - jupyter-client
    # - jupyter-core
    # - jupyter-packaging
    # - jupyter-server
    - jupyterlab
    # - jupyterlab-pygments
    # - jupyterlab-server
    # - jupyterlab-widgets
    # - locket
    # - markupsafe
    # - mathutils
    # - matplotlib-inline
    # - mistune
    # - nbclassic
    # - nbclient
    # - nbconvert
    # - nbformat
    # - nest-asyncio
    # - networkx
    - notebook
    # - notebook-shim
    - numpy<2.0.0
    - torch-scatter
    - open3d
    - opencv-python
    # - openexr
    # - packaging
    - pandas
    # - pandocfilters
    # - parso
    # - partd
    # - pexpect
    # - pickleshare
    # - prometheus-client
    # - prompt-toolkit
    # - psutil
    # - ptyprocess
    # - pygments
    - PyMCubes
    # - pyrsistent
    # - pytz
    # - pywavelets
    - pyyaml
    # - pyzmq
    # - rtree
    - scikit-image
    - scikit-learn
    - scipy
    # - seaborn
    # - send2trash
    # - sniffio
    # - soupsieve
    # - terminado
    # - testpath
    # - threadpoolctl
    # - tifffile
    # - tomlkit
    # - toolz
    - tqdm
    # - traitlets
    - trimesh
    # - urllib3
    # - wcwidth
    # - webencodings
    # - websocket-client
    # - widgetsnbextension
    # - zipp
    - PyOpenGL-accelerate
    - pyrender
```



**创建**：

```bash
cd /workspace/GO-SLAM && \
    mamba env create -f environment.yaml -y && \
    mamba activate go-slam
```



**额外依赖安装**：

```bash
pip install git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
pip install evo --upgrade --no-binary evo
python setup.py install
```



### issues

### custom datasets
