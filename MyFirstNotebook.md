```python
import pandas as pd
```


```python
df = pd.read_csv('http://bit.ly/autompg.csv')
df.head()
```


    ---------------------------------------------------------------------------

    HTTPError                                 Traceback (most recent call last)

    <ipython-input-8-436b563ed83e> in <module>
    ----> 1 df = pd.read_csv('http://bit.ly/autompg.csv')
          2 df.head()
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, squeeze, prefix, mangle_dupe_cols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, dialect, error_bad_lines, warn_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options)
        608     kwds.update(kwds_defaults)
        609 
    --> 610     return _read(filepath_or_buffer, kwds)
        611 
        612 
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in _read(filepath_or_buffer, kwds)
        460 
        461     # Create the parser.
    --> 462     parser = TextFileReader(filepath_or_buffer, **kwds)
        463 
        464     if chunksize or iterator:
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in __init__(self, f, engine, **kwds)
        817             self.options["has_index_names"] = kwds["has_index_names"]
        818 
    --> 819         self._engine = self._make_engine(self.engine)
        820 
        821     def close(self):
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in _make_engine(self, engine)
       1048             )
       1049         # error: Too many arguments for "ParserBase"
    -> 1050         return mapping[engine](self.f, **self.options)  # type: ignore[call-arg]
       1051 
       1052     def _failover_to_python(self):
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in __init__(self, src, **kwds)
       1865 
       1866         # open handles
    -> 1867         self._open_handles(src, kwds)
       1868         assert self.handles is not None
       1869         for key in ("storage_options", "encoding", "memory_map", "compression"):
    

    ~\anaconda3\lib\site-packages\pandas\io\parsers.py in _open_handles(self, src, kwds)
       1360         Let the readers open IOHanldes after they are done with their potential raises.
       1361         """
    -> 1362         self.handles = get_handle(
       1363             src,
       1364             "r",
    

    ~\anaconda3\lib\site-packages\pandas\io\common.py in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        556 
        557     # open URLs
    --> 558     ioargs = _get_filepath_or_buffer(
        559         path_or_buf,
        560         encoding=encoding,
    

    ~\anaconda3\lib\site-packages\pandas\io\common.py in _get_filepath_or_buffer(filepath_or_buffer, encoding, compression, mode, storage_options)
        287                 "storage_options passed with file object or non-fsspec file path"
        288             )
    --> 289         req = urlopen(filepath_or_buffer)
        290         content_encoding = req.headers.get("Content-Encoding", None)
        291         if content_encoding == "gzip":
    

    ~\anaconda3\lib\site-packages\pandas\io\common.py in urlopen(*args, **kwargs)
        193     import urllib.request
        194 
    --> 195     return urllib.request.urlopen(*args, **kwargs)
        196 
        197 
    

    ~\anaconda3\lib\urllib\request.py in urlopen(url, data, timeout, cafile, capath, cadefault, context)
        220     else:
        221         opener = _opener
    --> 222     return opener.open(url, data, timeout)
        223 
        224 def install_opener(opener):
    

    ~\anaconda3\lib\urllib\request.py in open(self, fullurl, data, timeout)
        529         for processor in self.process_response.get(protocol, []):
        530             meth = getattr(processor, meth_name)
    --> 531             response = meth(req, response)
        532 
        533         return response
    

    ~\anaconda3\lib\urllib\request.py in http_response(self, request, response)
        638         # request was successfully received, understood, and accepted.
        639         if not (200 <= code < 300):
    --> 640             response = self.parent.error(
        641                 'http', request, response, code, msg, hdrs)
        642 
    

    ~\anaconda3\lib\urllib\request.py in error(self, proto, *args)
        561             http_err = 0
        562         args = (dict, proto, meth_name) + args
    --> 563         result = self._call_chain(*args)
        564         if result:
        565             return result
    

    ~\anaconda3\lib\urllib\request.py in _call_chain(self, chain, kind, meth_name, *args)
        500         for handler in handlers:
        501             func = getattr(handler, meth_name)
    --> 502             result = func(*args)
        503             if result is not None:
        504                 return result
    

    ~\anaconda3\lib\urllib\request.py in http_error_302(self, req, fp, code, msg, headers)
        753         fp.close()
        754 
    --> 755         return self.parent.open(new, timeout=req.timeout)
        756 
        757     http_error_301 = http_error_303 = http_error_307 = http_error_302
    

    ~\anaconda3\lib\urllib\request.py in open(self, fullurl, data, timeout)
        529         for processor in self.process_response.get(protocol, []):
        530             meth = getattr(processor, meth_name)
    --> 531             response = meth(req, response)
        532 
        533         return response
    

    ~\anaconda3\lib\urllib\request.py in http_response(self, request, response)
        638         # request was successfully received, understood, and accepted.
        639         if not (200 <= code < 300):
    --> 640             response = self.parent.error(
        641                 'http', request, response, code, msg, hdrs)
        642 
    

    ~\anaconda3\lib\urllib\request.py in error(self, proto, *args)
        567         if http_err:
        568             args = (dict, 'default', 'http_error_default') + orig_args
    --> 569             return self._call_chain(*args)
        570 
        571 # XXX probably also want an abstract factory that knows when it makes
    

    ~\anaconda3\lib\urllib\request.py in _call_chain(self, chain, kind, meth_name, *args)
        500         for handler in handlers:
        501             func = getattr(handler, meth_name)
    --> 502             result = func(*args)
        503             if result is not None:
        504                 return result
    

    ~\anaconda3\lib\urllib\request.py in http_error_default(self, req, fp, code, msg, hdrs)
        647 class HTTPDefaultErrorHandler(BaseHandler):
        648     def http_error_default(self, req, fp, code, msg, hdrs):
    --> 649         raise HTTPError(req.full_url, code, msg, hdrs, fp)
        650 
        651 class HTTPRedirectHandler(BaseHandler):
    

    HTTPError: HTTP Error 404: Not Found



```python
%matplotlib inline
df.plot.scatter(x='hp' , y ='mpg')
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-9-daa948cc0769> in <module>
          1 get_ipython().run_line_magic('matplotlib', 'inline')
    ----> 2 df.plot.scatter(x='hp' , y ='mpg')
    

    NameError: name 'df' is not defined



```python
import sys
```


```python
print(sys.version)
```

    3.8.8 (default, Apr 13 2021, 15:08:03) [MSC v.1916 64 bit (AMD64)]
    


```python
import platform
```


```python
platform.python_version()
```




    '3.8.8'




```python
#A hello world example
print('hello world')
```

    hello world
    


```python
3+5

```




    8




```python
8*4
```




    32




```python
x=3
type(x)
```




    int




```python
y=2.1
type(y)
```




    float




```python
z = 'test'
type(z)
```




    str




```python
first_string_variable = 'test'
first_int_variable = 123
```


```python
print(first_string_variable)
```

    test
    


```python
first_tuple = (12, 'Jack', 56.3, "new" , (3,2), "test")
```


```python

```


```python
first_tuple
```




    (12, 'Jack', 56.3, 'new', (3, 2), 'test')




```python
first_tuple[1]
```




    'Jack'




```python
first_tuple[1:4]
```




    ('Jack', 56.3, 'new')




```python
first_tuple[1:-1]
```




    ('Jack', 56.3, 'new', (3, 2))




```python
first_list = [1,'Mark',2.3, 'test', None, 11]
```


```python
first_list
```




    [1, 'Mark', 'new', 'test', None, 11]




```python

```


```python

```


```python

```


```python
first_list.append(2)
```


```python
first_list.remove(2)
```


```python
first_list.pop(2)
```




    2.3




```python
first_list.insert(2, 'new')
```


```python
fname= 'George'
```


```python
lname= 'Washington'
```


```python
full_name = fname +lname
```


```python
full_name = 'fname'+'lname'
```


```python
fname
```




    'George'




```python
lname
```




    'Washington'




```python
full = fname + lname

```


```python
full = fname + '' + lname
```


```python
fname = 'Aliya'
```


```python
lname = 'Shaikh'
```


```python
full = fname + lname
```


```python
full
```




    'AliyaShaikh'




```python
full = fname +' '+lname
```


```python
full
```




    'Aliya Shaikh'




```python
def add_two_numbers(num1, num2):return num1+num2
```


```python
number1 = 23
number2 = 23
```


```python
result = add_two_numbers(number1, number2)
```


```python
result
```




    46.6




```python
number2 = 23.6
```


```python
def profile():
```


      File "<ipython-input-40-0926e88b7197>", line 1
        def profile():
                      ^
    SyntaxError: unexpected EOF while parsing
    



```python
def profile():
    age = 23
    height = 5.5
    weight = 130
    return age, height, weight
```


```python
print profile()
```


      File "<ipython-input-42-705bc29da96f>", line 1
        print profile()
              ^
    SyntaxError: invalid syntax
    



```python
profile()
```




    (23, 5.5, 130)




```python
newresult = profile()
```


```python
newresult
```




    (23, 5.5, 130)




```python
print newresult
```


      File "<ipython-input-46-c4a394f2b6f7>", line 1
        print newresult
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(newresult)?
    



```python
print (newresult)
```

    (23, 5.5, 130)
    


```python
print(profile())
```

    (23, 5.5, 130)
    


```python
print age
```


      File "<ipython-input-49-8aa35324a0f2>", line 1
        print age
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age)?
    



```python
print(age)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-50-5f7a7c5b2c60> in <module>
    ----> 1 print(age)
    

    NameError: name 'age' is not defined



```python
print age, height, weight
```


      File "<ipython-input-51-1ece668ff2de>", line 1
        print age, height, weight
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age, height, weight)?
    



```python
age, height, weight = profile()
```


```python
print age, height, weight
```


      File "<ipython-input-57-1ece668ff2de>", line 1
        print age, height, weight
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age, height, weight)?
    



```python
def profile():
    age = 23
    height = 5.5
    weight = 130
    return age, height, weight
```


```python
age, height, weight = profile()
```


```python
print age, height, weight
```


      File "<ipython-input-60-1ece668ff2de>", line 1
        print age, height, weight
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age, height, weight)?
    



```python
def profile():
    age = 23
    height = 5.5
    weight = 130
    return age, height, weight
age, height, weight = profile()
```


```python
print age, height, weight
```


      File "<ipython-input-62-1ece668ff2de>", line 1
        print age, height, weight
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age, height, weight)?
    



```python
def profile():
    age = 21
    height = 5.5
    weight = 130
    return age, height, weight

age, height, weight = profile()
```


```python
print age, height, weight
```


      File "<ipython-input-64-1ece668ff2de>", line 1
        print age, height, weight
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(age, height, weight)?
    



```python
print (age, height, weight)
```

    21 5.5 130
    


```python
profile()
```




    (21, 5.5, 130)




```python
print(profile())
```

    (21, 5.5, 130)
    


```python
store_list = ['Wendys', 'Chipotle', 'Starbucks', 'Dunkin', 'Taco Bell']
```


```python
for position, name in enumerate(store_list):
    print position, name
```


      File "<ipython-input-69-775ead449f37>", line 2
        print position, name
              ^
    SyntaxError: Missing parentheses in call to 'print'. Did you mean print(position, name)?
    



```python
for position, name in enumerate(store_list):
    print(position,name)

```

    0 Wendys
    1 Chipotle
    2 Starbucks
    3 Dunkin
    4 Taco Bell
    


```python
store_map = dict((name,position) for position, name in enumerate(store_list))
```


```python
store_map
```




    {'Wendys': 0, 'Chipotle': 1, 'Starbucks': 2, 'Dunkin': 3, 'Taco Bell': 4}




```python
num_list = range(15)
```


```python
num_list
```




    range(0, 15)




```python
list(num_list)

```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]




```python

reversed(list(num_list))
```




    <list_reverseiterator at 0x193e0854be0>




```python
list(reversed(num_list))
```




    [14, 13, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]




```python
subjects = ['math', 'stats', 'algebra']

```


```python
subject_count = ['one', 'two', 'three']
```


```python
total_subjects = zip(subjects, subject_count)
total_subjects
```




    <zip at 0x193e08512c0>




```python

```


```python
total_subjects
```




    <zip at 0x193e0845b40>




```python
sub = ['math', 'algebra', 'stats']
```


```python
sub_count = ['one', 'two', 'three']
```


```python
total_sub = zip(sub, sub_count)
```


```python
total_sub
```




    <zip at 0x193e0855680>




```python
a = (1, 2, 3)
b = ("Jenny", "Christy", "Monica")
```


```python
c = zip(a,b)
```


```python
c
```




    <zip at 0x193e0876980>




```python
zip( ['math', 'algebra', 'stats'], ['one', 'two', 'three'])
```




    <zip at 0x193e0785bc0>




```python
for i in zip([1,2,3],['a','b','c']):
    print(i)
```

    (1, 'a')
    (2, 'b')
    (3, 'c')
    


```python
p = zip([1,2,3],['a','b','c'])
```


```python
p
```




    <zip at 0x193e069eec0>




```python
z = zip([1,2,3],['a','b','c'])
```


```python
z
```




    <zip at 0x193e08454c0>




```python
print(z)
```

    <zip object at 0x00000193E08454C0>
    


```python
a = ['aliya', 'adnan', 'zoyu']
```


```python
b = [1,2,3]
```


```python
for i in zip(a,b):
    print(i)

```

    ('aliya', 1)
    ('adnan', 2)
    ('zoyu', 3)
    


```python
type(i)
```




    tuple




```python
new = i
```


```python
new
```




    ('zoyu', 3)




```python
x = (1,2,3)
y = (4,5,6)

```


```python
z=zip(x,y)
```


```python
z
```




    <zip at 0x193e084e8c0>




```python
age = 16
```


```python
if age<18:
    print ('minor')
else:
    print ('adult')
```

    minor
    


```python
word = "Encyclopedia"
```


```python
't' in word
```




    False




```python
test_score1 = 23,25,54

```


```python

test_score2 = 27, 65
```


```python
test_score = test_score1 + test_score2
```


```python
test_score
```




    (23, 25, 54, 27, 65)




```python
fname = 'George'
```


```python
lname = 'Washington'
```


```python
name = fname + lname 
```




```python
name
```




    'GeorgeWashington'




```python
print(name)
```

    GeorgeWashington
    


```python
print(fname)
```

    George
    


```python
name = friend*3
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-31-59df34afd723> in <module>
    ----> 1 name = friend*3
    

    NameError: name 'friend' is not defined



```python
name = 'friend' * 3
```


```python
name
```




    'friendfriendfriend'




```python
def my_first_function(name) : return(name)
```


```python
print my_first_function('Jack')
```


      File "<ipython-input-39-ad1bcb38437d>", line 1
        print my_first_function('Jack')
              ^
    SyntaxError: invalid syntax
    



```python
def add_two_numbers(num1, num2) : return num1 + num2
```


```python
number1 = 23
```


```python
number2 = 46
```


```python
result = add_two_numbers(number1, number2)
```


```python
result
```




    69




```python
print(result)
```

    69
    


```python
def profile():
    age = 21
    height = 5.6
    weight = 123
    return age, height, weight
```


```python
profile()
```




    (21, 5.6, 123)




```python
print(age, height, weight)
```

    21 5.6 123
    


```python
age, height, weight = profile()
```


```python
#enumerate takes care of the indices or positions
store_list = ['Dunkin', 'Taco Bell', 'Wendys', 'Chipotle', 'Dunkin']
```


```python
store_list
```




    ['Dunkin', 'Taco Bell', 'Wendys', 'Chipotle', 'Dunkin']




```python
enumerate(store_list)
```




    <enumerate at 0x1e8a2b52b80>




```python
for position, name in enumerate (store_list):
    print (position, name)
```

    0 Dunkin
    1 Taco Bell
    2 Wendys
    3 Chipotle
    4 Dunkin
    


```python
store_map = dict((name, position) for position, name in enumerate (store_list)):
    print(position, name)
```


      File "<ipython-input-56-9d37a5dd7d47>", line 1
        store_map = dict((name, position) for position, name in enumerate (store_list)):
                                                                                       ^
    SyntaxError: invalid syntax
    



```python
store_map = dict((name, position) for position, name in enumerate (store_list))
print(position, name)
```

    4 Dunkin
    


```python
store_map
```




    {'Dunkin': 4, 'Taco Bell': 1, 'Wendys': 2, 'Chipotle': 3}




```python
sorted([24,65,2,4,69])
```




    [2, 4, 24, 65, 69]




```python
sorted("Data Science")
```




    [' ', 'D', 'S', 'a', 'a', 'c', 'c', 'e', 'e', 'i', 'n', 't']




```python
num_list = range(15)
```


```python
num_list
```




    range(0, 15)




```python
list(reversed(num_list))
```




    [14, 13, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]




```python
list(reversed(reversed(num_list)))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-65-2b12d4a176dc> in <module>
    ----> 1 list(reversed(reversed(num_list)))
    

    TypeError: 'range_iterator' object is not reversible



```python
list1 = ['1','2','3']
```


```python
list2 = ['4','5','6']
```


```python
list = zip(list1, list2)
```


```python
list
```




    <zip at 0x1e8a2a946c0>




```python
for a in list1 , list2 zip(list1, list2):
    print(list)
```


      File "<ipython-input-70-c9f6a965a67b>", line 1
        for a in list1 , list2 zip(list1, list2):
                               ^
    SyntaxError: invalid syntax
    



```python
marks = 81
```


```python
if marks>90:
    print('Grade A')
elif 80<marks<90:
    print('Grade B')
elif 70<marks<80:
    print('Grade C')
else:
    print('Grade D')
    
```

    Grade B
    


```python
temperature = 100
while temperature > 95:
    print(temperature)
    temperature = temperature - 1
```

    100
    99
    98
    97
    96
    


```python
def test_float(number):
    return float(number)
```


```python
test_float(3.2)
```




    3.2




```python
test_float('test_float')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-76-eff7b377201b> in <module>
    ----> 1 test_float('test_float')
    

    <ipython-input-74-4c0f8e1b61a5> in test_float(number)
          1 def test_float(number):
    ----> 2     return float(number)
    

    ValueError: could not convert string to float: 'test_float'



```python
import numpy as np
```


```python
distance = [10,15,17,21]
```


```python
time = [.30 , .47 , .54 , 1.23]
```


```python
np_distance = np.array(distance)
np_time = np.array(time)
speed = np_distance/np_time
```


```python
speed
```




    array([33.33333333, 31.91489362, 31.48148148, 17.07317073])




```python
first_numpy_array = np.array([1,2,3,4,5,6])
```


```python
first_numpy_array
```




    array([1, 2, 3, 4, 5, 6])




```python
print(first_numpy_array)
```

    [1 2 3 4 5 6]
    


```python
array_with_zeros = np.zeros((3,5))
```


```python
array_with_zeros
```




    array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])




```python
array_with_empty = np.empty((5,3))
```


```python
array_with_empty
```




    array([[0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.],
           [0., 0., 0.]])




```python
np.empty((2,3))
```




    array([[0., 0., 0.],
           [0., 0., 0.]])




```python
np.random
```




    <module 'numpy.random' from 'C:\\Users\\aliya\\anaconda3\\lib\\site-packages\\numpy\\random\\__init__.py'>




```python
np.random((2,3))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-99-cf9c37e80811> in <module>
    ----> 1 np.random((2,3))
    

    TypeError: 'module' object is not callable



```python
np.random.seed(3)
```


```python
np.empty((2,3))
```




    array([[0., 0., 0.],
           [0., 0., 0.]])




```python
np_arange=np.arange(12)
```


```python
np_arange
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])




```python
np_arange.reshape(2,6)
```




    array([[ 0,  1,  2,  3,  4,  5],
           [ 6,  7,  8,  9, 10, 11]])




```python
np_linspc = np.linspace(1,10,6)
```


```python
np_linspc
```




    array([ 1. ,  2.8,  4.6,  6.4,  8.2, 10. ])




```python
np_ls = np.linspace(1,20,5)
```


```python
np_ls
```




    array([ 1.  ,  5.75, 10.5 , 15.25, 20.  ])




```python
print(np_ls)
```

    [ 1.    5.75 10.5  15.25 20.  ]
    


```python
oneD_array = np.arange(15)
```


```python
oneD_array
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14])




```python
print(oneD_array)
```

    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14]
    


```python
twoD_array = oneD_array.reshape(3,5)
```


```python
twoD_array
```




    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14]])




```python
threeD_array = np.arange(27).reshape(3,3,3)
```


```python
threeD_array
```




    array([[[ 0,  1,  2],
            [ 3,  4,  5],
            [ 6,  7,  8]],
    
           [[ 9, 10, 11],
            [12, 13, 14],
            [15, 16, 17]],
    
           [[18, 19, 20],
            [21, 22, 23],
            [24, 25, 26]]])




```python
oneD_array.ndims
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-125-525267368bb6> in <module>
    ----> 1 oneD_array.ndims
    

    AttributeError: 'numpy.ndarray' object has no attribute 'ndims'



```python
oneD_array.ndim
```




    1




```python
twoD_array.ndim
```




    2




```python
oneD_array.shape
```




    (15,)




```python
twoD_array.shape
```




    (3, 5)




```python
threeD_array.shape
```




    (3, 3, 3)




```python
threeD_array.size
```




    27




```python
twoD_array.size
```




    15




```python
oneD_array.size
```




    15




```python
oneD_array.dtype
```




    dtype('int32')




```python
twoD_array.dtype
```




    dtype('int32')




```python
threeD_array.dtype
```




    dtype('int32')




```python
np.add(45,20)
```




    65




```python
np.subtract(3,5)
```




    -2




```python
np_daily_wage = np.array([7,19,56,46,31])*15
```


```python
np_daily_wage
```




    array([105, 285, 840, 690, 465])




```python
print(np_daily_wage)
```

    [105 285 840 690 465]
    


```python
sum(np_daily_wage)
```




    2385




```python
np.logical_and(np_weekly_hours>20, np_weekly_hours<65)
```




    array([ True,  True,  True, False,  True])




```python
np_weekly_hours = np.array([23,45,50,20,55])
```


```python

```
