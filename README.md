# pytmatrixc

A fork of [pytmatrix](https://github.com/jleinonen/pytmatrix)
with modern cross-platform build process and streamlined installation.

## Installation

No compiling or building required. Install with:

```bash
pip install pytmatrixc
```

## Usage

This package should work exactly the same way as the original.
For documentation, see the
[pytmatrix usage guide](https://github.com/jleinonen/pytmatrix/wiki#usage).


```python
# Simple usage
from pytmatrix import tmatrix

scatterer = tmatrix.Scatterer(radius=1.0, wavelength=10.0, m=complex(1.5, 0.5), axis_ratio=1.0/0.6)
scatterer.get_S()

# Run tests
from pytmatrix.test import test_tmatrix
test_tmatrix.run_tests()
```

If something does not work, [create an issue](https://github.com/nikoleskinen/pytmatrixc/issues)
or [contact me by email](mailto:niko.leskinen@fmi.fi?subject=Issue%20with%20pytmatrixc).
