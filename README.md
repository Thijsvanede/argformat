# argformat
Provides a more structured formatter for python's argparse module.

## Installation
```
pip install argformat
```

## Formatter
Argformat provides the `argformat.StructuredFormatter` class that can be set as `formatter_class` of `ArgumentParser`.
The `StructuredFormatter` changes the output format in the following ways:
 1. It adds `(default = <value>)` to the `-h/--help` output if a default value is given.
 2. It outputs the help message in column format.
 3. It ignores the default width of 80 characters for the `-h/--help` output (warning: output may be distorted on smaller terminals).

### Example
Below we provide the difference in output for the project ([DeepCASE](https://github.com/Thijsvanede/DeepCASE/)) that uses the argformat library.

### Default formatter
```
usage: deepcase.py [-h] [--offset OFFSET] [--time TIME] [--all] [--breach] [--incident] [--ignore] [-f FEATURES] [-i DIM_INPUT]
                   [-o DIM_OUTPUT] [-m MAX_SEQUENCES] [-n MAX_EVENTS] [-c COMPLEXITY] [-b BATCH_SIZE] [-d DEVICE] [-e EPOCHS] [-r]
                   [-s] [--train TRAIN] [--epsilon EPSILON] [--min-samples MIN_SAMPLES] [--threshold THRESHOLD]
                   [--load-context LOAD_CONTEXT] [--load-interpreter LOAD_INTERPRETER] [--save-context SAVE_CONTEXT]
                   [--save-interpreter SAVE_INTERPRETER]
                   file [test] [malicious]

DeepCASE: providing contextual analysis of security alerts

optional arguments:
  -h, --help            show this help message and exit

Input:
  file                  read preprocessed input file
  test                  read preprocessed test file
  malicious             read preprocessed malicious file
  --offset OFFSET       offset for items to load
  --time TIME           max time length of input sequence
  --all                 perform experiment on all data
  --breach              read breaches
  --incident            read incidents
  --ignore              ignore incident and breach info

ContextBuilder:
  -f FEATURES, --features FEATURES
                        maximum number of expected features
  -i DIM_INPUT, --dim-input DIM_INPUT
                        length of input sequence
  -o DIM_OUTPUT, --dim-output DIM_OUTPUT
                        length of output sequence
  -m MAX_SEQUENCES, --max-sequences MAX_SEQUENCES
                        maximum number of sequences ro read from input
  -n MAX_EVENTS, --max-events MAX_EVENTS
                        maximum number of events to read from input
  -c COMPLEXITY, --complexity COMPLEXITY
                        complexity of the model

ContextBuilder training:
  -b BATCH_SIZE, --batch-size BATCH_SIZE
                        batch size
  -d DEVICE, --device DEVICE
                        train using given device (cpu|cuda|auto)
  -e EPOCHS, --epochs EPOCHS
                        number of epochs to train with
  -r, --random          train with random selection
  -s, --silent          supress printing progress
  --train TRAIN         training samples to use (or ratio of if 0 <= TRAIN <= 1)

Interpreter:
  --epsilon EPSILON     interpreter epsilon for clustering
  --min-samples MIN_SAMPLES
                        interpreter min_samples for clustering
  --threshold THRESHOLD
                        interpreter confidence threshold for fingerprinting

Model I/O parameters:
  --load-context LOAD_CONTEXT
                        load context builder from LOAD file
  --load-interpreter LOAD_INTERPRETER
                        load interpreter from LOAD file
  --save-context SAVE_CONTEXT
                        save context builder to SAVE file
  --save-interpreter SAVE_INTERPRETER
                        save interpreter to SAVE file
```

### `argformat.StructuredFormatter`
```
usage: deepcase.py [-h] [--offset OFFSET] [--time TIME] [--all] [--breach] [--incident] [--ignore] [-f FEATURES] [-i DIM_INPUT]
                   [-o DIM_OUTPUT] [-m MAX_SEQUENCES] [-n MAX_EVENTS] [-c COMPLEXITY] [-b BATCH_SIZE] [-d DEVICE] [-e EPOCHS] [-r] [-s]
                   [--train TRAIN] [--epsilon EPSILON] [--min-samples MIN_SAMPLES] [--threshold THRESHOLD]
                   [--load-context LOAD_CONTEXT] [--load-interpreter LOAD_INTERPRETER] [--save-context SAVE_CONTEXT]
                   [--save-interpreter SAVE_INTERPRETER]
                   file [test] [malicious]

DeepCASE: providing contextual analysis of security alerts

optional arguments:
  -h, --help                            show this help message and exit

Input:
  file                                  read preprocessed input     file
  test                                  read preprocessed test      file                         (optional)
  malicious                             read preprocessed malicious file                         (optional)
  --offset            OFFSET            offset for items to load
  --time              TIME              max time length of input sequence                        (default = 86400)
  --all                                 perform experiment on all data
  --breach                              read breaches
  --incident                            read incidents
  --ignore                              ignore incident and breach info

ContextBuilder:
  -f, --features      FEATURES          maximum number of expected features                      (default =   280)
  -i, --dim-input     DIM_INPUT         length of input sequence                                 (default =    10)
  -o, --dim-output    DIM_OUTPUT        length of output sequence                                (default =     1)
  -m, --max-sequences MAX_SEQUENCES     maximum number of sequences ro read from input           (default =   inf)
  -n, --max-events    MAX_EVENTS        maximum number of events to read from input              (default =   inf)
  -c, --complexity    COMPLEXITY        complexity of the model                                  (default =   128)

ContextBuilder training:
  -b, --batch-size    BATCH_SIZE        batch size                                               (default =   128)
  -d, --device        DEVICE            train using given device (cpu|cuda|auto)                 (default =  auto)
  -e, --epochs        EPOCHS            number of epochs to train with                           (default =    10)
  -r, --random                          train with random selection
  -s, --silent                          supress printing progress
  --train             TRAIN             training samples to use (or ratio of if 0 <= TRAIN <= 1) (default =   0.5)

Interpreter:
  --epsilon           EPSILON           interpreter epsilon     for clustering                   (default =   0.1)
  --min-samples       MIN_SAMPLES       interpreter min_samples for clustering                   (default =     5)
  --threshold         THRESHOLD         interpreter confidence threshold for fingerprinting      (default =   0.2)

Model I/O parameters:
  --load-context      LOAD_CONTEXT      load context builder from LOAD file
  --load-interpreter  LOAD_INTERPRETER  load interpreter     from LOAD file
  --save-context      SAVE_CONTEXT      save context builder to   SAVE file
  --save-interpreter  SAVE_INTERPRETER  save interpreter     to   SAVE file
```

## Usage
Simply import the `StructuredFormatter` and set it as the argparse `formatter_class`:

### Example
```python
import argparse
from argformat import StructuredFormatter

# Parse arguments
parser = argparse.ArgumentParser(
    prog            = <Your program>,
    description     = <Your description>,
    formatter_class = StructuredFormatter,
)

# Add your arguments normally...
```
