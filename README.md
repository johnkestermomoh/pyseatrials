pyseatrials
================

<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

The library `pyseatrials` is a collection of functions, written in
`Python`, that are useful for estimating ship performance from sea
trials data. The library is based on ITTC [Preparation, Conduct and
Analysis of Speed/Power Trials.
7.5-04-01-01.1](https://www.ittc.info/media/8370/75-04-01-011.pdf) and
is designed to make the process of estimating ships peformance easier,
faster and more reliable by packaging all the equations into a clearly
documented python library with examples and code testing for all
functions.

There full documentation is available at
https://jonnob.github.io/pyseatrials/

The library uses nbdev by fastdotai and most functions depend solely on
numpy.

<div>

> **Important**
>
> This project is in early development. Function names and library
> structure may have breaking changes at anytime

</div>

## Install

``` sh
python -m pip install git+https://github.com/JonnoB/pyseatrials 
```

## How to use

As an example consider the problem of calculating resistance experienced
by the ship from waves.

``` python
from pyseatrials.wave import *
import numpy as np
```

To calculate the wave resistance experienced by a ship you can call the
STAWAVE-1 function `stawave1`

``` python
stawave1_fn(beam = 20, wave_height =  3, length = 5)
```

    23085.0

STAWAVE-1 like almost all functions in `pyseatrials` are vectorised.
This means if an array of values is used the function will return an
array for all values entered. The example below shows the resistance in
Newtons for a range of wave heights.

``` python
stawave1_fn(20, np.linspace(1, 3, 4), 5)
```

    array([ 2565.,  7125., 13965., 23085.])

<div>

> **Note**
>
> Using an array follows standard Python broadcasting rules. So if you
> enter an arrays in different arguments the arrays must have the same
> length and the $i$th element of each array should refer to the same
> vessel/state/etc

</div>

All functions are have documentation, in addition there is in depth
documentation online
([STAWAVE-1](https://jonnob.github.io/pyseatrials/wave_resistance.html#stawave1_fn)).

``` python
stawave1_fn?
```

    Signature:
    stawave1_fn(
        beam: float,
        wave_height: float,
        length: float,
        water_density: float = 1026,
        gravity: float = 9.81,
    ) -> float
    Docstring: STAWAVE-1 finds the resistance caused by bow waves for ships experiencing low heave and pitch
    File:      /usr/local/lib/python3.9/dist-packages/pyseatrials/wave.py
    Type:      function

# Notes

- The library attempts to use descriptive naming of the variables,
  however, this is not always possible
- The library refers to ‘ITTC’ throughout, this always refers to
  ‘7.5-04-01-01.1 Preparation, Conduct and Analysis of Speed/Power
  Trials’
- Where the equations are directly from ITTC they are marked **ITTC
  equations**: x
- The library focuses on the equations needed to accurately measure
  performance during sea trials. However, many of these equations can be
  applied at other stages of measuring ship performance, e.g. model
  performance in the a tank test.

## Some useful definations

- Tank test: a test performed at a marine testing facilty on a scale
  model of the vessel. This is used to obtain valuable performance data
  which can be scaled to better understand the real performance of the
  ship during seatrials.

# To be done

The following parts of ITTC need to be implemented

- STAWAVE-2
- Example ship data
- Images
  - Wind
  - law of cosines
  - STAWAVE-1
- test for errors, such as divide by 0

# Licence

The library is a python implementation of the ITTC library and is free
to use under an Apache 2.0 licence
