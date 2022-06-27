<h1 align="center"><i>✨ pysilk-cffi ✨ </i></h1>

<h3 align="center">The cffi binding for <a href="https://github.com/kn007/silk-v3-decoder">silk-v3-decoder</a> </h3>

[![pypi](https://img.shields.io/pypi/v/pysilk-cffi.svg)](https://pypi.org/project/pysilk-cffi/)
![python](https://img.shields.io/pypi/pyversions/pysilk-cffi)
![implementation](https://img.shields.io/pypi/implementation/pysilk-cffi)
![wheel](https://img.shields.io/pypi/wheel/pysilk-cffi)
![license](https://img.shields.io/github/license/synodriver/pysilk-cffi.svg)
![action](https://img.shields.io/github/workflow/status/synodriver/pysilk-cffi/build%20wheel)

## 安装
```bash
pip install pysilk-cffi
```


## 使用
- encode
```python
import pysilk

with open("verybiginput.pcm", "rb") as pcm, open("output.silk", "wb") as silk:
    pysilk.encode(pcm, silk, 24000, 24000)
```

- decode

```python
import pysilk

with open("verybiginput.silk", "rb") as silk, open("output.pcm", "wb") as pcm:
    pysilk.decode(silk, pcm, 24000)
```

## 支持功能
- 接受任何二进制的```file-like object```，比如```BytesIO```，可以流式解码大文件
- 包装了silk的全部C接口的参数，当然他们都有合理的默认值

## 公开函数
```python
from typing import BinaryIO

def encode(input: BinaryIO, output: BinaryIO, sample_rate: int, bit_rate: int, max_internal_sample_rate: int = 24000, packet_loss_percentage: int = 0, complexity: int = 2, use_inband_fec: bool = False, use_dtx: bool = False, tencent: bool = True) -> bytes: ...
def decode(input: BinaryIO, output: BinaryIO, sample_rate: int, frame_size: int = 0, frames_per_packet: int = 1, more_internal_decoder_frames: bool = False, in_band_fec_offset: int = 0, loss: bool = False) -> bytes: ...
```

## 公开异常
```python
class SilkError(Exception):
    pass
```