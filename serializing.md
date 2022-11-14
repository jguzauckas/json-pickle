# Using `jsonpickle`

`jsonpickle` is going to be used as an intermediate step in our JSON serializing/deserializing (encoding/decoding) process. It will help turn our objects into something that JSON can serialize/deserialize.

All of the sample code provided in this file is in the serializing.py Python file for you to run, modify, and otherwise investigate, as well as the person.json file!

---

## `json` and `jsonpickle` Workflow

To move an object from one program to another using a `.json` file, we have a certain workflow. Assuming you already have the object ready to go, here is the general flow:

Writing program:
`object` -> `jsonpickle` -> `json`

Reading program:
`json` -> `jsonpickle` -> `object`

You'll notice that these are the same flow, but reversed from one-another.

---

## Serializing Objects

`jsonpickle` has similar methods to `json`, except that we exclusively work with strings, and we let `json` continue to handle the actual files. Our first step is to `import` our modules:

```python
import json
import jsonpickle
```

In order to work with `jsonpickle` (for serializing **or** deserializing), we need a custom class to work with! Here is a basic Person class:

```python
class Person:
    def __init__(self, name:str, age:int) -> None:
        self._name = name
        self._age = age

    def __str__(self) -> str:
        return f"{self._name} is {self._age} years old."
```

We'll also need an object made from this class to serialize:

```python
p1 = Person("Mr. G", 24)
```

Now we are ready to serialize! If we went with our typical method using `json`, we wouldn't even be able to serialize it into a `str`. For example if you tried:

```python
dump_str = json.dumps(p1)
```

We'd get the following error:

```
TypeError: Object of type Person is not JSON serializable
```

This is where `jsonpickle` comes in. We need to save a translated string as an intermediate before we hand it off to JSON to serialize. To do this, we use the `jsonpickle.dumps` method:

```python
dump_str = jsonpickle.dumps(p1)
```

Now `jsonpickle` has converted the information into a `str` that has the form of a Python dictionary, which `json` will play much nicer with. So we can continue and use our typical `json.dump` method to turn this into a `.json` file:

```python
with open("person.json", "w") as my_file:
    json.dump(dump_str, my_file)
```

For those interested, we could have written this without an intermediate variable by nesting our functions. This is by means required, but is considered more efficient:

```python
with open("person.json", "w") as my_file:
    json.dump(jsonpickle.dumps(p1), my_file)
```

Note that while this works, it does become a little bit harder to read.

---

## Deserializing Objects

Given a `.json` file with some `jsonpickle.dumps` encoded objects, we can deserialize them by using `json` and `jsonpickle` in tandem. This time we are going to reverse the order from our encoding. First step is to pull the

## Installing `jsonpickle`

This is our first module that is not already included in our install of Python, which means we need to tell the computer to add it so that we can `import` and use it.

To install a module, we use the **p**ackage **i**nstaller for **p**ython, which is shortened to `pip`.

`pip` is an option to select when installing Python, but even if it was not selected, Python comes with the means to enable it afterwards.

To start, you can test if you have `pip` enabled, in git bash try the following command:

```bash
pip install jsonpickle
```

If this goes through and walks through a few steps, `pip` is enabled and you are good to go. If this produces the following error:

```
pip: command not found
```

then we are going to have to enable `pip` ourselves.

First step to enabling `pip` is to make sure Python has downloaded and updated `pip` to the latest version. To do this, we use two separate commands in git bash:

```bash
py -m ensurepip --upgrade
```

and then:

```bash
py -m pip install --upgrade pip
```

Now we are ready tell Windows how to find `pip`, via the `path`. First step is to open the Windows Run dialogue by either searching "run" or hitting Windows + R. Once the dialogue is open, type `sysdm.cpl` and hit enter or click "OK".

This should open up the `System Properties` window, where we'll want to go to the `Advanced` tab at the top.

At the bottom right of the `Advanced` section, there should be a button titled `Environment Variables...`. Click on it.

In the new window titled `Environment Variables`, there are two main sections that have boxes drawn around them: `User variables for ____` and `System Variables`. Regardless of your access on your computer, we will be working with the first section titled `User variables for ____`.

Click on the variable labeled `Path`, which should highlight the whole row blue. Now hit the `Edit...` button, which should open yet another window titled `Edit environment variable`.

Along the right side, hit the `New` button. In the area to write that becomes highlighted, paste the following, two different times:

```
%USERDPROFILE%\AppData\Roaming\Python\Python310\Scripts
```

```
%USERPROFILE%\AppData\Local\Programs\Python\Python310\Scripts
```

On each subsequent window, hit the "OK" button until all of the `System Properties`-related windows are closed.

Now in `git bash`, you should be able to enter the following command without any issues:

```
pip install jsonpickle
```

If you are still having issues please reach out to Mr. Guzauckas.

---

## `import`

As this is a module, we will want to import it alongside our normal `json` module, so the top of your program should look like this:

```python
import json
import jsonpickle
```
