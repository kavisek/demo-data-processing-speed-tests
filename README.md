# Demo Data Processing Speed Test   

Numpy vs Pandas

Here are the results from running 300 iterations of the same data processing task using Numpy and Pandas. Feel free to change the data processing functions to see how the results change with your wokrload.

![Plot](./app/images/plot.png)


### Numpy vs Pure Python List

NumPy arrays occupy less space compared to Python lists. For instance, a Python list of lists might require around 20 MB, but a NumPy 3D array with single-precision floating-point numbers could be accommodated within just 4 MB. Moreover, NumPy enhances both reading and writing speeds for accessing elements.

### Numpy vs Pandas

Numpy is faster than Pandas for data processing. This is because Pandas is built on top of Numpy and adds additional overhead. Numpy is also more memory efficient than Pandas. Numpy is a better choice for data processing when speed and memory efficiency are important. Pandas is a better choice when data is already in a tabular format and you need to do some analysis on it. Pandas is better option by default for data analysis, use Numpy when you need to optimize for speed or memory.

Numpy uses contiguous memory. This means that all of the data is stored in one place. Pandas data structures (like DataFrame) are built upon Numpy arrays, which use contiguous memory. The overhead comes from additional features in Pandas, not necessarily non-contiguous memory storage. This is why Numpy is more memory efficient than Pandas.

Pandas Can be less memory efficient, especially when dealing with very large data sets, because of the overhead associated with its rich indexing functionality.

Numpy Offers high performance for operations on arrays, particularly for large datasets, because of its underlying implementation in C.

## Numpy Multiprocessing

Numpy is multiprocessed by default. Pandas is not. This means that Numpy can take advantage of multiple cores on your machine. Pandas can be multiprocessed by using the `swifter` library.

NumPy can still be bottlenecked by the Global Interpreter Lock (GIL) in Python. The GIL is a mutex that protects access to Python objects, preventing multiple native threads from executing Python bytecodes at once. This means that threads cannot be used for parallelizing Python code that works with Python objects, including NumPy operations.

However, it's important to note that NumPy often releases the GIL for the duration of computationally intensive operations. This is because NumPy, under the hood, uses optimized libraries written in languages like C or Fortran for heavy computations, which can run in parallel and are not subject to the GIL. Therefore, for many of NumPy's numerical operations, the GIL is not a limiting factor.

That being said, the GIL can still be a bottleneck in scenarios where you are doing operations in Python that involve a lot of object manipulation or where the operations cannot release the GIL. In these cases, using multiprocessing (which uses separate processes instead of threads and thus bypasses the GIL) or switching to implementations like NumPy with Dask (which enables parallel computing) can be beneficial to improve performance.

## Numpy vs Spark 

Spark is faster than Numpy for data processing. This is because Spark is distributed and can take advantage of multiple machines. Numpy is not distributed and can only take advantage of one machine. Spark is also more memory efficient than Numpy. Spark is a better choice for data processing when speed and memory efficiency are important. Numpy is a better choice when data is already in a tabular format and you need to do some analysis on it. Spark is better option by default for data analysis, use Numpy when you need to optimize for speed or memory.

I normally recommend spark when your datasets are larger than 1GB. If your datasets are smaller than 1GB, then you can use Numpy (i.e ~5 million rows).

This repo does not include a Spark example. I will add a separate repo for Spark later.

## Setup

```bash
cd app
pyenv install 3.10.8
poetry env use $HOME/.pyenv/versions/3.10.8/bin/python
poetry install

make jupyter
```

You can now run the notebook to view the results.