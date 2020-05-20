# StructuredFormatter
A more structured formatter for python's argparse module.

## Installation
```
pip install TODO
```

## Usage
Simply set the StructuredFormatter as the argparse `formatter_class`:

```python
import argparse
from TODO import StructuredFormatter

# Parse arguments
parser = argparse.ArgumentParser(
    prog        = <Your program>,
    description = <Your description>,
    formatter_class=StructuredFormatter
)

# Add your arguments normally...
```
