========================================================
JSON-XML
========================================================





JSON-C implements a reference counting object model that allows you to easily construct JSON objects
in C, output them as JSON formatted strings and parse JSON formatted strings back into the
Crepresentation of JSON objects. It aims to conform to RFC 7159.

JSON-C provides a set of processing API that is json-formatted. The Quectel module integrates with open
source JSON-C, which can be used directly by users when developing application programs. Related
head file needs to be included and also it needs to link libjson-c library.



JSON-C API Introduction
----------------------------------

.. code-block:: c

    Enumeration:
    typedef enum json_type {
       json_type_null,
       json_type_boolean,
       json_type_double,
       json_type_int,
       json_type_object,
       json_type_array,
       json_type_string,
    } json_type;





