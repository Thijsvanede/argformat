# argformat
Provides a more structured formatter for python's argparse module.

## Installation
```
pip install argformat
```

## Usage
Simply import the `StructuredFormatter` and set it as the argparse `formatter_class`:

### Example
```python
import argparse
from argformat import StructuredFormatter

# Parse arguments
parser = argparse.ArgumentParser(
    prog        = <Your program>,
    description = <Your description>,
    formatter_class=StructuredFormatter
)

# Add your arguments normally...
```
