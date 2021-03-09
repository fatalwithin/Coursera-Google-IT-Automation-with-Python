## Course Introduction

------

Hello, and welcome to the last course of this program!

Throughout this program, you've had the opportunity to learn and practice lots of different tools and techniques for creating and maintaining automation. You've learned how to write programs in Python, how to interact with files and processes from your Python scripts, how to track the history of your changes using Git, how to understand what's happening when the automation doesn't work as expected, and how to automate your infrastructure by using tools like Puppet. Phew, that’s a lot!

This last course will give you the opportunity to put all this new knowledge in action. You'll be given a bunch of small projects based on real-life scenarios, and you'll use Python to write the automation that will solve the challenges.

Working on these projects will give you the opportunity to start building your programming portfolio. When you’re done with each of them, you can upload the code you write to GitHub to show off your skills!

Since this course builds on top of everything taught in the other courses, you need to have working knowledge of the main concepts we covered: coding in Python, interacting with files and processes, using Git, using the Linux command line, troubleshooting problems, and working with Cloud infrastructure.

Throughout the course, we'll give you an introduction to the tools and techniques necessary for solving each of the projects. We recommend that you follow along by coding on your own computer. Coming up with your own exercises and practicing using the tools that you learn is the best way to master them.

One final note. As you probably noticed, this is a reading and not a video. :) This course is composed of readings that guide you along the path of using Python to solve real-life problems, along with labs that let you put that knowledge in action. We hope you enjoy the challenges and the new skills you gain along the way.

# Module 1: Manipulating Images

------

## Built-In Libraries vs. External Libraries

------

As we covered in an earlier course, the Python Standard Library comes as part of the Python installation and includes modules for the most common tasks you can do with Python. But there's tons of other things you might want to do in your scripts, and not all of them are in the standard library. This is where external modules come into play. When developers write a Python module that they think others might find useful, they publish it in **PyPI** *--* also known as the **Python Package Index** ([https://pypi.org](https://pypi.org/))*.* We can browse this repository of Python modules to find the module we need. It includes thousands of projects, which are classified by different categories, like topic, development status, and intended audience.

In this module, we’re going to be **transforming** and **converting** images. To do that, we'll be using a popular library for image manipulation: the **Python Imaging Library (PIL)**. The original PIL library [hasn't been updated since 2009](http://www.pythonware.com/products/pil/) and does not support Python 3. Fortunately, there's a current *fork* of PIL called [**Pillow**](https://pypi.org/project/Pillow/), that properly supports Python 3 and is kept up-to-date. The Pillow library is packaged with the name **pillow**, but the module name in Python is still **PIL**.

If you try to import the PIL module on a computer that doesn't have pillow (or PIL) installed, you might get an error like this:

```python
>>> import PIL
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'PIL'
 
```

Okay, looks like I don't have that module yet! As we covered in an [earlier course](https://www.coursera.org/learn/python-operating-system/lecture/NxUXx/getting-your-computer-ready-for-python), there are several ways to add external modules to your Python environment. PIL is a pretty common library, and on Linux it’s usually available as a native package. For example:

```bash
user@ubuntu:~$ sudo apt install python3-pil
Reading package lists... Done
Building dependency tree     
(...)
Unpacking python3-pil:amd64 (4.3.0-2) ...
Setting up python3-pil:amd64 (4.3.0-2) ...
 
```

For other environments, you should use Python's package installer, **pip3**. Like this:

```bash
$ pip3 install pillow
Collecting pillow
  Downloading https://files.pythonhosted.org/packages/85/28/2c72ba965b52884a0bd71e419761fc162763dc2e5d9bec2f3b1949f7272a/Pillow-6.2.1-cp37-cp37m-macosx_10_6_intel.whl (3.9MB)
     |████████████████████████████████| 3.9MB 1.7MB/s
Installing collected packages: pillow
Successfully installed pillow-6.2.1
 
```

Once we've done that, we can try to import the module again. And this time it should succeed with no errors:

```python
>>> import PIL
```

That's better!

Now, how do you learn to use a library that you’ve never worked with before? It's time to get familiar with the library's **Application Programming Interface (API)**! 

## What is an API?

------

Application Programming Interfaces (APIs) help different pieces of software talk to each other. When you write a program, you typically use a bunch of existing libraries for the programming language of your choice. These libraries provide APIs in the form of **external** or **public** functions, classes, and methods that other code can use to get their job done without having to create a lot of repeated code.

And not only that, APIs can also be used by other pieces of software, even if they were written in a completely different programming language. For example, Cloud services use APIs that your programs can communicate with by making web calls. What’s special about an API? What makes it different to any other function that you would write in your own code?

If you look at the library's code, you’ll find it has many functions that we're not meant to use directly from our code. These **internal** or **private** functions, classes, and methods do important work, but they’re there to support the functions that are published by the library. You probably don't have time to dig in to understand every little bit of how the code works, but you need to know how to interact with the library to do useful work. An API is sort of like a promise. Even if the library's internal code changes, you expect the function to keep accepting the same parameters and returning the same results. That provides a stable **interface** to write your code with. That's an API!

Library authors are free to make improvements and changes to the code *behind* the interface, but they shouldn't make changes to the way the functions are called or the results they provide. Because this would break the code that depends on that library. When a library author needs to make a **breaking change** to an API, then they need to have a plan in place for communicating that change to their users. That's why [breaking changes *should* be saved for major version increments of a library](https://semver.org/#summary).

When you choose a certain library to use with your code, the first step is to get familiar with its API. You'll need to look at how the functions are called, what inputs they expect, and what outputs they'll return.

## How to Make Sense of an API?

------

How do you learn to use a library or an API that you’ve never worked with before? It might take you a bit of time to familiarize yourself with how the library operates, but that's okay. It's worth spending some time understanding the way the functions are organized, the inputs and outputs, and the general expectations of the library.

In general, a good API should be descriptive. You should be able to look at a function's name and have a pretty good idea of what it will do. A well-designed API will follow patterns and **naming conventions**. That means that the functions, classes and methods should have names that help you understand what to expect from them. And when the name isn’t enough, you should have access to the documentation for each of the functions that will help you figure out what they do.

For example, when we visit the [reference page for the Image object](https://pillow.readthedocs.io/en/stable/reference/Image.html) in Pillow, we see this piece of example code:

```python
from PIL import Image
im = Image.open("bride.jpg")
im.rotate(45).show()
```

This piece of code is pretty straightforward. Even without having seen this library before, you can probably guess that it opens an image called bride.jpg, rotates it 45 degrees, and then shows it on the screen.

But how can we know for sure? We can look up each of the functions in the documentation and check what they’re supposed to do. When dealing with open-source libraries, we can even check out how the function is implemented to see if it matches our expectations. For a web service API or a closed-source library, you might not have access to the underlying code, but you should have access to the documentation that’s generated by the code.

For a Python library like PIL, the code is documented using **docstrings**. If you remember from waaaay back in our first course, docstrings are documentation that lives alongside the code. You've been using them ever since! When you use “**help()**” to describe a function, or read a description of what a Python function does in your IDE, what you’re reading comes from docstrings in the code.

For example, let's take a look at the documentation for PIL:

```python
 >>> help(PIL)

Help on package PIL:

NAME
    PIL - Pillow (Fork of the Python Imaging Library)

DESCRIPTION
    Pillow is the friendly PIL fork by Alex Clark and Contributors.
        https://github.com/python-pillow/Pillow/

    Pillow is forked from PIL 1.1.7.

    PIL is the Python Imaging Library by Fredrik Lundh and Contributors.
    Copyright (c) 1999 by Secret Labs AB.

    Use PIL.__version__ for this Pillow version.
    PIL.VERSION is the old PIL version and will be removed in the future.

    ;-)

PACKAGE CONTENTS
    BdfFontFile
    BlpImagePlugin
    BmpImagePlugin
    BufrStubImagePlugin
    ContainerIO
    CurImagePlugin
    DcxImagePlugin
    DdsImagePlugin
    EpsImagePlugin
...
```

Lots of Python modules also publish their documentation online. Pillow's full documentation is published [here](https://pillow.readthedocs.io/). There, the docstrings have been compiled into a browsable reference, and they’ve also written [a handbook](https://pillow.readthedocs.io/en/stable/handbook/index.html) [with tutorials](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html) for you to get familiar with the library's API. Woohoo!

## How to Use PIL for Working With Images

------

As we've mentioned, for the project in this module, you'll use the Python Imaging Library to process a bunch of images. So, how does that work?

When using PIL, we typically create **Image** objects that hold the data associated with the images that we want to process. On these objects, we operate by calling different methods that either return a new image object or modify the data in the image, and then end up saving the result in a different file.

For example, if we wanted to resize an image and save the new image with a new name, we could do it with:

```python
from PIL import Image
im = Image("example.jpg")
new_im = im.resize((640,480))
new_im.save("example_resized.jpg")
```

In this case, we're using the resize method that returns a new image with the new size, and then we save it into a different file. Or, if we want to rotate an image, we can use code like this:

```python
from PIL import Image
im = Image("example.jpg")
new_im = im.rotate(90)
new_im.save("example_rotated.jpg")
```

This method also returns a new image that we can then use to create the new rotated file. Because the methods return a new object, we can even combine these operations into just one line that rotates, resizes, and saves:

```python
from PIL import Image
im = Image("example.jpg")
im.rotate(180).resize((640,480)).save("flipped_and_resized.jpg")
```

There's a ton more that you can do with the PIL library. Have a look at [the docs](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html) and try it on your computer! 

## Project Problem Statement

------

To complete this module, you'll need to write a script that processes a bunch of images. It turns out that your company is in the process of updating its website, and a design contractor has been hired to create some new icon graphics for the site. However, the contractor has delivered the final designs and they’re in the wrong format, rotated 90° and too large. You’re unable to get in contact with the designers and your own deadline is approaching fast. You’ll need to use Python to get these images ready for launch!

So, how will you do this? You'll need to go through a folder full of images and operate with each of them. On each image, you'll use PIL methods like the ones we saw in the examples, and then write the new images in the right place.

If this sounds tricky, don't panic! You've already seen everything you need to do this, and now it's time to put it into practice.

As in the previous courses, the assessment will be done on a Virtual Machine running in the Cloud, thanks to the Qwiklabs infrastructure. You'll only have access to the VM for a limited amount of time, so we recommend that you write the script locally in your computer first, and only start the lab once your script is working correctly.

Good luck, you've got this!

## Download the file

Your design contractor sent you the zipped file through his team drive. Download the file from the drive using the following CURL request:

```
curl -c ./cookie -s -L "https://drive.google.com/uc?export=download&id=$11hg55-dKdHN63yJP20dMLAgPJ5oiTOHF" > /dev/null | curl -Lb ./cookie "https://drive.google.com/uc?export=download&confirm=`awk '/download/ {print $NF}' ./cookie`&id=11hg55-dKdHN63yJP20dMLAgPJ5oiTOHF" -o images.zip && sudo rm -rf cookie
```

Output:

![5fe50f874fc9b1f9.png](https://cdn.qwiklabs.com/kj85%2Bf6VDnhdjRDmtzSiaU5D9vk8WNVJWiNeKKtWJ5U%3D)

List files using the command:

```
ls
```

Output:

![bfeaf6a7d282dcf5.png](https://cdn.qwiklabs.com/NW9Sum4yd4TkL7LXwNCw4lExYVhY6bEZ%2BFbknotqsnM%3D)

Unzip the file using the following command:

```
unzip images.zip
```

To list images from the `images` folder use the following command:

```
ls ~/images
```

The images received are in the wrong format:

- .tiff format
- Image resolution 192x192 pixel (too large)
- Rotated 90° anti-clockwise

The images required for the launch should be in this format:

- .jpeg format
- Image resolution 128x128 pixel
- Should be straight

## Install Pillow

We should change the format and size of these pictures, and rotate them by 90° clockwise. To do this, we'll use Python Imaging Library (PIL). Install `pillow` library using the following command:

```
pip3 install pillow
```

Python Imaging Library (known as Pillow in newer versions) is a library in Python that adds support for opening, manipulating, and saving lots of different image file formats.

Pillow offers several standard procedures for image manipulation. These include:

- Per-pixel manipulations
- Masking and transparency handling
- Image filtering, such as blurring, contouring, smoothing, or edge finding
- Image enhancing, like sharpening and adjusting brightness, contrast or color
- Adding text to images (and much more!)

## Write a Python script

This is the challenge section of the lab where you'll write a script that uses PIL to perform the following operations:

- Iterate through each file in the folder
- For each file:
  - Rotate the image 90° clockwise
  - Resize the image from 192x192 to 128x128
  - Save the image to a new folder in .jpeg format

Use a nano editor for this purpose. You can name the file however you'd like. And make sure to save the updated images in the folder: `/opt/icons/`

You'll use lots of methods from PIL to complete this exercise. You can refer to [Pillow](https://pillow.readthedocs.io/en/stable/reference/index.html) for detailed explanations and have a look at the [tutorials](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html) to help you build the script and complete the task.

To save the file after editing, press Ctrl-O, Enter, and Ctrl-x.

Once your script is ready, grant executable permission to the script file.

```
chmod +x <script_name>.py
```

Replace <script_name> with the name of your script.

Now, run the file.

```
./<script_name>.py
```

Replace <script_name> with the name of your script.

On a successful run, this should produce images in the right format within the directory: `/opt/icons/`

To view the updated images use the following command:

```
ls /opt/icons
```

Output:

![ea9afeff1183c231.png](https://cdn.qwiklabs.com/nugr9eMy2HgOEUdhu%2B%2FjxldxZ4kh%2BeTDLLhwRD%2FGTsk%3D)

To check image properties, use the Python interpreter:

```
python3
```

Once the interactive shell opens, import the Image module from PIL:

```
from PIL import Image
```

Open any image from the folder, or you can use the following image:

```
img = Image.open("/opt/icons/ic_edit_location_black_48dp")
```

To view the format and size of the image:

```
img.format, img.size
```

Output:

![b3a2965a9c783ec9.png](https://cdn.qwiklabs.com/o1Bb%2Fm7Rt%2Fz3Vns5Ja3RUGD7%2BvgOW2%2FGN74SAL0fwcQ%3D)

Type `exit()` to exit from the Python interpreter.

# Module 2: Web Applications and Services

------

Congratulations on making it through the first lab in this course!

Remember that putting your Python skills to practice with exercises like this one is the way to getting the hang of it all. By practicing solving complex challenges, you'll become a lot more confident in your programming abilities, and you'll be able to achieve a lot more.

In this module, we'll look into a bunch of different tools that can be really useful in today's IT world. You'll first learn how you can use different text formats to store data in text files, retrieve it, and even transmit it over the internet.

Later on, we'll look into how we can get our code to interact with services running on different computers using a module called Python Requests.

We'll see a bunch of different examples and give you pointers to more information. Don't forget that the best way to get comfortable with all these modules and libraries is to come up with your own examples and practice writing scripts on your local computer!

## Web Applications and Services

------

A ***web application*** is an application that you interact with over HTTP. Most of the time when you’re using a website on the Internet, you’re interacting with a web application. So, how does this look behind the scenes?

Your web browser sends an HTTP request to a web server. Then, the web server passes the request along to the web application in charge of deciding what information to show you. The application then generates the website content (in HTML format). The application is also in charge of serving images and any other necessary data so that your web browser can render the website on your computer.

Lots of web applications also have APIs that you can use from your scripts! Web applications that have an API are also known as **web services**. Instead of browsing to a web page to type and click around, you can use your program to send a message known as an **API call** to the web service. The part of the program that listens on the network for API calls is called an **API endpoint**.

When you interact with a web service like this, you don't even care what language the other application is using. You interact with it using a specified protocol, and the only important constraint is that both the service and your program know how to use this protocol.

So, how does that work? That's coming up!

## Data Serialization

------

If you have two programs that need to communicate with each other, how do you get that data from one place to another? We're going to talk about two aspects of that problem: what to send, and how to send it.

First, what do you send? When you have a conversation with another person, you don't send thoughts and memories directly between your brains. At least not yet! You first have to convert your thoughts into language, and then transmit that language to another person. They take that language, and convert it back into thoughts. It’s the same with programs running in different places, or at different times.

In a previous course, we took a list of lists in memory and wrote it to disk as a **Comma-Separated Value (CSV)** file. This is one example of a technique called **data serialization**. Data serialization is the process of taking an in-memory data structure, like a Python object, and turning it into something that can be stored on disk or transmitted across a network. Later, the file can be read, or the network transmission can be received by another program and turned back into an object again. Turning the serialized object back into an in-memory object is called **deserialization**.

Data serialization is extremely useful for communicating with web services. A web service's **API endpoint** takes messages in a specific format, containing specific data. By the end of this module, we'll be sending messages to web services, but for now let's concentrate on how to serialize Python objects into some common formats.

Let's start with the contact information from one of our CSV examples. We'll keep just two entries to keep our examples short, but there's no limit to how long these can be.

```
name,username,phone,department,role
Sabrina Green,sgreen,802-867-5309,IT Infrastructure,System Administrator
Eli Jones,ejones,684-3481127,IT Infrastructure,IT specialist
```

Instead of having a list of lists, we could turn this information into a list of dictionaries. In each of these dictionaries, the key will be the name of the column, and the value will be the corresponding information in each row. It could look something like this: 

```python
people = [
    {
        "name": "Sabrina Green",
        "username": "sgreen",
        "phone": "802-867-5309",
        "department": "IT Infrastructure",
        "role": "Systems Administrator"
    },
    {
        "name": "Eli Jones",
        "username": "ejones",
        "phone": "684-348-1127",
        "department": "IT Infrastructure",
        "role": "IT Specialist"
    },
]

```

Using a structure like this lets us do interesting things with our information that’s much harder to do with CSV files. For example, let's say we want to record more than one phone number for each person. Instead of using a single string for "phone", we could represent that data in another dictionary, like this:  

```python
people = [
    {
        "name": "Sabrina Green",
        "username": "sgreen",
        "phone": {
            "office": "802-867-5309",
            "cell": "802-867-5310"
        },
        "department": "IT Infrastructure",
        "role": "Systems Administrator"
    },
    {
        "name": "Eli Jones",
        "username": "ejones",
        "phone": {
            "office": "684-348-1127"
        },
        "department": "IT Infrastructure",
        "role": "IT Specialist"
    },
]

```

Now, we can record multiple phone numbers per person, and give them descriptive names like "office" and "cell". This would be hard to store in a CSV file, because the data is not *flat*. To help us with that, there's a bunch of different formats that we can use to store our data when the structure isn't flat.

Up next, we'll look into a few of the most common ones.

## Data Serialization Formats

------

There are lots and lots of ways to serialize data. In this course, we'll cover a couple of the most common ones and we'll look into how you can use them from Python. Once you get the hang of how this works, it's super easy to use a different format if needed.

[**JSON (JavaScript Object Notation)**](https://json.org/) is the serialization format that we'll use the most in this course. We'll go into some details later but, for now, let's just use the **json** module to convert our **people** list of dictionaries into JSON format.  

```python
import json

with open('people.json', 'w') as people_json:
    json.dump(people, people_json, indent=2)
```

This code uses the **json.dump()** function to serialize the **people** object into a JSON file. The contents of the file will look something like this:  

```json
[
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },
  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  },
]
```

[**YAML (Yet Another Markup Language)**](https://yaml.org/) has a lot in common with JSON. They’re both formats that can be easily understood by a human when looking at the contents. In this example, we’re using the **yaml.safe_dump()** method to serialize our object into YAML:  

```python
import yaml

with open('people.yaml', 'w') as people_yaml:
    yaml.safe_dump(people, people_yaml)
```

That code will generate a **people.yaml** file that looks like this:  

```yaml
- department: IT Infrastructure
  name: Sabrina Green
  phone:
    cell: 802-867-5310
    office: 802-867-5309
  role: Systems Administrator
  username: sgreen
- department: IT Infrastructure
  name: Eli Jones
  phone:
    office: 684-348-1127
  role: IT Specialist
  username: ejones
```

While this doesn't look exactly like the JSON example above, both formats list the names of the fields as part of the format, so that both the programs *parsing* the data and the humans looking at it can make sense out of it. The main difference is how these formats are used. JSON is used frequently for transmitting data between web services, while YAML is used the most for storing configuration values.

These are just a couple of the most common data serialization formats. We've left out some other pretty common ones like [**Python pickle**](https://docs.python.org/3/library/pickle.html), [**Protocol Buffers**](https://developers.google.com/protocol-buffers), or the [**eXtensible Markup Language (XML)**](https://www.w3.org/XML/). Each of them is useful in a specific context, although not the focus of this course. You can read more about them by following those links.  

## More About JSON

------

Alright, we've seen a couple of different serialization formats. Let's now dive into more details about [**JSON (JavaScript Object Notation)**](https://json.org/), which you'll be using in the lab at the end of this module.

As we mentioned before, JSON is **human-readable**, which means it’s encoded using printable characters, and formatted in a way that a human can understand. This doesn't necessarily mean that you *will* understand it when you look at it, but you *can*.

Lots of web services send messages back and forth using JSON. In this module, and in future ones, you’ll serialize JSON messages to send to a web service.

JSON supports a few **elements** of different data types. These are very basic data types; they represent the most common basic data types supported by any programming language that you might use.

JSON has **strings,** which are enclosed in quotes.  

```json
"Sabrina Green"
```

It also has **numbers,** which are not.  

```json
1002
```

JSON has **objects**, which are key-value pair structures like Python dictionaries.  

```json
{
  "name": "Sabrina Green",
  "username": "sgreen",
  "uid": 1002
}
```

And a key-value pair can contain another object as a value.  

```json
{
  "name": "Sabrina Green",
  "username": "sgreen",
  "uid": 1002,
  "phone": {
    "office": "802-867-5309",
    "cell": "802-867-5310"
  }
}
```

JSON has **arrays**, which are equivalent to Python lists. Arrays can contain strings, numbers, objects, or other arrays.  

```json
[
  "apple",
  "banana",
  12345,
  67890,
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  }
]
```

And as you’ve probably noticed, JSON elements are always **comma-delimited**. With these basics under your belt, you could create valid JSON by hand, and edit examples of JSON that you encounter. Except we don't really want to do that, since it's clunky and we’re bound to make a ton of errors! Instead, let’s use the **json** library that does all the heavy lifting for us.  

```python
import json
```

The **json** library will help us turn Python objects into JSON, and turn JSON strings into Python objects! The **dump()** method serializes basic Python objects, writing them to a file. Like in this example:  

```python
import json
 
people = [
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },
  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  }
]
 
with open('people.json', 'w') as people_json:
    json.dump(people, people_json)
```

That gives us a file with a single line that looks like this:  

```json
[{"name": "Sabrina Green", "username": "sgreen", "phone": {"office": "802-867-5309", "cell": "802-867-5310"}, "department": "IT Infrastructure", "role": "Systems Administrator"}, {"name": "Eli Jones", "username": "ejones", "phone": {"office": "684-348-1127"}, "department": "IT Infrastructure", "role": "IT Specialist"}]
```

JSON doesn't *need* to contain multiple lines, but it sure can be hard to read the result if it's formatted this way! Let's use the **indent** parameter for **json.dump()** to make it a bit easier to read.  

```python
with open('people.json', 'w') as people_json:
    json.dump(people, people_json, indent=2)
```

The resulting file should look like this:  

```json
[
  {
    "name": "Sabrina Green",
    "username": "sgreen",
    "phone": {
      "office": "802-867-5309",
      "cell": "802-867-5310"
    },
    "department": "IT Infrastructure",
    "role": "Systems Administrator"
  },
  {
    "name": "Eli Jones",
    "username": "ejones",
    "phone": {
      "office": "684-348-1127"
    },
    "department": "IT Infrastructure",
    "role": "IT Specialist"
  }
]
```

Now it’s much easier to follow! In fact, it looks very similar to how you’d write out the object in Python. Cool!

Another option is to use the **dumps()** method, which also serializes Python objects, but returns a string instead of writing directly to a file.  

```python
>>> import json
>>> 
>>> people = [
...   {
...     "name": "Sabrina Green",
...     "username": "sgreen",
...     "phone": {
...       "office": "802-867-5309",
...       "cell": "802-867-5310"
...     },
...     "department": "IT Infrastructure",
...     "role": "Systems Administrator"
...   },
...   {
...     "name": "Eli Jones",
...     "username": "ejones",
...     "phone": {
...       "office": "684-348-1127"
...     },
...     "department": "IT Infrastructure",
...     "role": "IT Specialist"
...   }
... ]
>>> people_json = json.dumps(people)
>>> print(people_json)
[{"name": "Sabrina Green", "username": "sgreen", "phone": {"office": "802-867-5309", "cell": "802-867-5310"}, "department": "IT Infrastructure", "role": "Systems Administrator"}, {"name": "Eli Jones", "username": "ejones", "phone": {"office": "684-348-1127"}, "department": "IT Infrastructure", "role": "IT Specialist"}]
```

The **load()** method does the inverse of the **dump()** method. It deserializes JSON from a file into basic Python objects. The **loads()** method also deserializes JSON into basic Python objects, but parses a string instead of a file.  

```python
>>> import json
>>> with open('people.json', 'r') as people_json:
...     people = json.load(people_json)
... 
>>> print(people)
[{'name': 'Sabrina Green', 'username': 'sgreen', 'phone': {'office': '802-867-5309', 'cell': '802-867-5310'}, 'department': 'IT Infrastructure', 'role': 'Systems Administrator'}, {'name': 'Eli Jones', 'username': 'ejones', 'phone': {'office': '684-348-1127'}, 'department': 'IT Infrastructure', 'role': 'IT Specialist'}, {'name': 'Melody Daniels', 'username': 'mdaniels', 'phone': {'cell': '846-687-7436'}, 'department': 'User Experience Research', 'role': 'Programmer'}, {'name': 'Charlie Rivera', 'username': 'riverac', 'phone': {'office': '698-746-3357'}, 'department': 'Development', 'role': 'Web Developer'}]
```

Remember that JSON elements can only represent simple data types. If you have complex Python objects, you won’t be able to automatically serialize them as JSON. Take a look at [this table](https://docs.python.org/3/library/json.html#py-to-json-table) to see in detail how Python objects are converted into JSON elements:

| Python                                 | JSON   |
| :------------------------------------- | :----- |
| dict                                   | object |
| list, tuple                            | array  |
| str                                    | string |
| int, float, int- & float-derived Enums | number |
| True                                   | true   |
| False                                  | false  |
| None                                   | null   |

## The Python Requests Library

------

Up to now, we've seen how we can serialize the data that we have in our programs and turn it into a format that we can store on disk. Once the data is stored, another process can open up those files, de-serialize them, and go from there.

This works, but only if the other process has access to the same filesystem you used to store your data. What if you wanted to send a message to another computer on another network? HTTP to the rescue!

Remember that **HTTP (HyperText Transfer Protocol)** is the protocol of the world-wide web. When you visit a webpage with your web browser, the browser is making a series of **HTTP requests** to web servers somewhere out on the Internet. Those servers will answer with **HTTP responses**. This is also how we’re going to send and receive messages with web applications from our code.

The [Python Requests library](https://requests.readthedocs.io/) makes it super easy to write programs that send and receive HTTP. Instead of having to understand the HTTP protocol in great detail, you can just make very simple HTTP connections using Python objects, and then send and receive messages using the methods of those objects. Let's look at an example:  

```python
>>> import requests
>>> response = requests.get('https://www.google.com')
```

That's it! That was a basic request for a web page! We used the Requests library to make a **HTTP GET** request for a specific **URL, or Uniform Resource Locator**. The URL tells the Requests library the name of the resource (**www.google.com**) and what protocol to use to get the resource (**https://**). The result we get is an object of type [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response).

Alright, now what did the web server respond with? Let's take a look at the first 300 characters of the [Response.text](https://requests.readthedocs.io/en/master/api/#requests.Response.text):  

```python
>>> print(response.text[:300])
<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="de"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="dZfbIAn803LDGXS9
 
```

Now, it might be hard for you to read the [HTML (HyperText Markup Language)](https://html.spec.whatwg.org/multipage/) that was returned in this response, but your web browser knows just how to turn that into a familiar-looking web page.

Even with this simple example, the Requests module has done a whole lot of work for us! We didn't have to write any code to find the web server, make a network connection, construct an HTTP message, wait for a response, or decode the response. Not that HTML can't be messy enough on its own, but let's look at the first bytes of the [**raw**](https://requests.readthedocs.io/en/master/api/#requests.Response.raw) message that we received from the server:  

```python
>>> response = requests.get('https://www.google.com', stream=True)
>>> print(response.raw.read()[:100])
b'\x1f\x8b\x08\x00\x00\x00\x00\x00\x02\xff\xc5Z\xdbz\x9b\xc8\x96\xbe\xcfS`\xf2\xb5-\xc6X\x02$t\xc28\xe3v\xdc\xdd\xee\xce\xa9\xb7\xdd;\xe9\x9d\xce\xf6W@\t\x88\x11`@>D\xd6\x9b\xce\xe5<\xc3\\\xcd\xc5\xfc\xab8\x08\xc9Nz\x1f.&\x8e1U\xb5j\xd5:\xfc\xb5jU\x15\x87;^\xe2\x16\xf7)\x97\x82b\x1e\x1d\x1d\xd2S'
```

What's all that? The response was **compressed** with [**gzip**](https://www.gzip.org/), so it had to be **decompressed** before we could even read the text of the HTML. One more thing that the Requests library handled for us!

The [requests.Response](https://requests.readthedocs.io/en/master/api/#requests.Response) object also contains the exact request that was created for us. We can check out the headers stored in our object to see that the Requests module told the web server that it was okay to compress the content:  

```python
>>> response.request.headers['Accept-Encoding']
'gzip, deflate'
```

And then the server told us that the content had actually been compressed.  

```python
>>> response.headers['Content-Encoding']
'gzip'
```

And all this happened by default, without us having to do anything special to make it work. Amazing, right?

## Useful Operations for Python Requests

------

There's a ton of things that we can do with Python Requests. We'll cover some of the most important features here and give you pointers for more information at the end.

First, how do we know if a request we made got a successful response? You can check out the value of [**Response.ok**](https://requests.readthedocs.io/en/master/api/#requests.Response.ok), which will be **True** if the response was good, and **False** if it wasn't.  

```python
>>> response.ok
True
```

Now, keep in mind that this will only tell you if the web server says that the response successfully fulfilled the request. The response module can’t determine if that data that you got back is the kind of data that you were expecting. You'll need to do your own checking for that!

If the boolean isn’t specific enough for your needs, you can get the [HTTP response code](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml) that was returned by looking at [Response.status_code](https://requests.readthedocs.io/en/master/api/#requests.Response.ok):  

```python
200
>>> response.status_code
```

Excellent! To write maintainable, stable code, you’ll always want to check your responses to make sure they succeeded before trying to process them further. For example, you could do something like this:  

```python
response = requests.get(url)
if not response.ok:
    raise Exception("GET failed with status code {}".format(response.status_code))
```

But you don't really need to do that. Requests has us covered here, too! We can use the [Response.raise_for_status()](https://requests.readthedocs.io/en/master/api/#requests.Response.raise_for_status) method, which will raise an **HTTPError** exception *only if* the response wasn’t successful.  

```python
response = requests.get(url)
response.raise_for_status()
```

Up next, we'll look into the different types of HTTP request methods that we can make using this handy requests module.  

## HTTP GET and POST Methods

------

HTTP supports several [**HTTP methods**](https://tools.ietf.org/html/rfc7231#section-4.3), like GET, POST, PUT, and DELETE. We're going to spend time on the two most common HTTP requests: GET and POST.

The [**HTTP GET method**](https://tools.ietf.org/html/rfc7231#section-4.3.1), of course, retrieves or **gets** the resource specified in the URL. By sending a GET request to the web server, you’re asking for the server to GET the resource for you. When you’re browsing the web, most of what you’re doing is using your web browser to issue a whole bunch of GET requests for the text, images, videos, and so forth that your browser will display to you.

A GET request can have **parameters**. Have you ever seen a URL that looked like this?  

```
https://example.com/path/to/api/cat_pictures?search=grey+kitten&max_results=15
```

The question mark separates the URL resource from the resource's parameters. These parameters are one or more key-value pairs, formatted as a [**query string**](https://en.wikipedia.org/wiki/Query_string). In the example above, the **search** parameter is set to "grey+kitten", and the **max_results** parameter is set to 15.

But you don't have to write your own code to create an URL like that one. With [requests.get()](https://requests.readthedocs.io/en/master/api/#requests.get), you can provide a dictionary of parameters, and the Requests module will construct the correct URL for you!  

```python
>>> p = {"search": "grey kitten",
...      "max_results": 15}
>>> response = requests.get("https://example.com/path/to/api", params=p)
>>> response.request.url
'https://example.com/path/to/api?search=grey+kitten&max_results=15'
 
```

You might notice that using parameters in Requests is yet another form of data serialization. Query strings are handy when we want to send small bits of information, but as our data becomes more complex, it can get hard to represent it using query strings. 

An alternative in that case is using the [**HTTP POST method**](https://tools.ietf.org/html/rfc7231#section-4.3.3). This method sends, or **posts**, data to a web service. Whenever you fill a web form and press a button to submit, you're using the POST method to send that data back to the web server. This method tends to be used when there's a bunch of data to transmit.

In our scripts, a POST request looks very similar to a GET request. Instead of setting the **params** attribute, which gets turned into a query string and appended to the URL, we use the **data** attribute, which contains the data that will be sent as part of the POST request.  

```python
>>> p = {"description": "white kitten",
...      "name": "Snowball",
...      "age_months": 6}
>>> response = requests.post("https://example.com/path/to/api", data=p)
```

Let's check out the generated URL for this request:  

```python
>>> response.request.url
'https://example.com/path/to/api'
```

See how much simpler the URL is on this POST now? Where did all of the parameters go? They’re part of the **body** of the HTTP message. We can see them by checking out the **body** attribute.  

```python
>>> response.request.body
'description=white+kitten&name=Snowball&age_months=6'
```

Ah, ha! There they are!

So, if we need to send and receive data from a web service, we can turn our data into dictionaries and then pass that as the **data** attribute of a POST request.

Today, it's super common to send and receive data specifically in JSON format, so the Requests module can do the conversion directly for us, using the **json** parameter.  

```python
>>> response = requests.post("https://example.com/path/to/api", json=p)
>>> response.request.url
'https://example.com/path/to/api'
>>> response.request.body
b'{"description": "white kitten", "name": "Snowball", "age_months": 6}' 
```

And that's it for our brief introduction to the Requests module. If you want to learn more, feel free to work through the [Requests Quickstart](https://requests.readthedocs.io/en/master/user/quickstart/).

In the project at the end of this module, you’ll use the Requests module to interact with a web application. This simple application was created using the Django web framework. So, what's that, exactly? Read on to learn more!



## What is Django?

------

The lab project at the end of this module will feature a very simple web application created using [**Django**](https://djangoproject.com/). Django is a **full-stack web framework** written in Python. For this project, you'll only need to interact with it through HTTP requests, but it's still a good idea to understand what it is, and when it would be a good tool for you to use.

A full-stack web framework handles a bunch of different components that are typical when creating a web application. It contains libraries that help you handle each of the pieces: writing your application's code, storing and retrieving data, receiving web requests, and responding to them. If you need to build an application that has a web frontend, using a web framework like Django can save you a lot of time and effort, because a lot of challenges are already solved for you.

Web frameworks are commonly split into three basic components: 

- (1) the application code, where you'll add all of your application's logic; 
- (2) the data storage, where you'll configure what data you want to store and how you're storing it; and 
- (3) the web server, where you'll state which pages are served by which logic.

Splitting your code like that helps you write more modular code, promotes code reuse, and allows for flexibility when viewing and accessing data. For example, you could have a simple web page where users of the system can access the information already stored in it, and a separate programmatic interface that can be used by other scripts or applications to transmit data to the system.

When you’re writing a web application, there's a ton of little decisions to make. Relying on a framework like Django is similar to using external libraries for your code. There are a lot of features, which you can use very easily, instead of writing everything from scratch and re-making all of the same mistakes that we all make when writing a web application for the first time.

Django has a ton of useful components for building websites. In the lab project, Django will be used for serving the company website, including customer reviews. It does this by taking the request for a URL and parsing it using the **urlresolver** module. This is a core module in Django that interprets URL requests and matches them against a list of defined patterns. If a URL matches a pattern, the request is passed to the associated function, called a **view**. This allows you to serve different pages depending on what URL is being requested. You can even build complex logic into the function handling the request to make more dynamic, interactive, and exciting pages.

Django can also handle reading and writing data from a database, letting you store and retrieve data used by your application. In the lab, the database holds the customer reviews for the company. When a user loads the website, the logic will ask the database for all available customer reviews. These are retrieved and formatted into a web page, which is served as a response to the URL request. Django makes it easy to interact with data stored in a database by using an **object-relational mapper**, or **ORM**. This tool provides an easy mapping between data models defined as Python classes and an underlying database that stores the data in question.

On top of this, the Django application running in the lab includes an **endpoint** that can be used to add new customer reviews to the database. This endpoint is configured to receive data in JSON format, sent through an HTTP POST request. The data transmitted will then be stored in the database and added to the list of all reviews. The framework even generates an interactive web form, that lets us directly interact with the endpoint using our browser, which can be really handy for testing and debugging.

Django is one of many popular web frameworks. Alternative Python-based web frameworks similar to Django include [Flask](https://www.fullstackpython.com/flask.html), [Bottle](https://bottlepy.org/docs/dev/), [CherryPy](https://cherrypy.org/), and [CubicWeb](https://www.cubicweb.org/). There are a host of other frameworks written in other languages too, not just Python.

## Project Problem Statement

------

To complete this module, you'll write a script that interacts with a running web service. The web service is part of your company's website and is in charge of storing and displaying the customer reviews of the company.

The reviews are stored in text files in the local disk. Your script should open those files, process the information to turn it into the format expected by the web service, then send it to the web service to get stored.

For this lab, the service is running on the same machine, and you can actually look at how all of it is implemented, if you want. But you don't need to change the service implementation to complete the exercise.

Remember that you can take your time to prepare the code that you’ll write. You can start the lab later on, once you have a good idea of what you'll do and how you'll do it.

Also, feel free to check out the resources that we pointed to as many times as you need.

Good luck, you've got this!

### **Introduction**

You’re working at a company that sells second-hand cars. Your company constantly collects feedback in the form of customer reviews. Your manager asks you to take those reviews (saved as .txt files) and display them on your company’s website. To do this, you’ll need to write a script to convert those .txt files and process them into Python dictionaries, then upload the data onto your company’s website (currently using Django).

### **What you’ll do**

- Use the Python OS module to process a directory of text files 
- Manage information stored in Python dictionaries
- Use the Python requests module to upload content to a running Web service
- Understand basic operations for Python requests like GET and POST methods 

## Web server corpweb

**Django** is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. A Web framework is a set of components that provide a standard way to develop websites quickly and easily.

For this lab, a Django web server `corpweb` is already configured under `/projects/corpweb` directory. You can check it out by visiting the external IP address of the `corpweb` VM. The external IP address can be found in the connection details panel. Enter the `corpweb` external IP address in a new separate browser tab.

Output:

![6d4dcdc788626521.png](https://cdn.qwiklabs.com/oTBchVUq807yFZsqyMsAfEt%2F2T9McWLGQ39BWNH4lFI%3D)

You'll see that there's currently no feedback.

Now, append `/feedback` to the external IP address of `corpweb` VM opened in the browser tab.

![4c82e605dae520f3.png](https://cdn.qwiklabs.com/irg5MZwCPQdQQZPVXYKwLR5rlg2VJ%2FZsOr8mFmc0nEs%3D)

This is a web interface for a REST end-point. Through this end-point, you can enter feedback that can be displayed on the company's website. You can use this end-point in the example below. Start by copying and pasting the following JSON to the **Content** field on the website, and click **POST**.

```json
{"title": "Experienced salespeople", "name": "Alex H.", "date": "2020-02-02", "feedback": "It was great to talk to the salespeople in the team, they understood my needs and were able to guide me in the right direction"}
```

Now, go back to the main page by removing the `/feedback` from the URL. You can see that the feedback that you just entered is displayed on the webpage.

![971893c6631c06f6.png](https://cdn.qwiklabs.com/sYBz1LWL83hyw7D2NrCBo51J6WGO5DSpdZf0Ix1a3Ms%3D)

The whole website is stored in `/projects/corpweb`. You're free to look around the configuration files. Also, there's no need to make any changes to the website; all interaction should be done through the REST end-point.

## Process text files and upload to running web server

In this section, you'll write a Python script that will upload the feedback automatically without having to turn it into a dictionary.

Navigate to `/data/feedback` directory, where you'll find a few .txt files with customer reviews for the company.

```bash
cd /data/feedback
ls
```

Output:

![80676af4c8e69cc4.png](https://cdn.qwiklabs.com/%2B3MkEuvftlNNBZUs7YVVPPgta0D6uo4RpebSSDEC4d8%3D)

Use the `cat` command to view these files. For example:

```bash
cat 007.txt
```

Output:

![336fe102a3cdc30b.png](https://cdn.qwiklabs.com/iqjatGUkTc7ZHbJrF62dI9e%2B%2F5Cavugl5CHPktDfn28%3D)

They're all written in the same format (i.e. `title, name, date,` and `feedback).`

Here comes the challenge section of the lab, where you'll write a Python script that uploads all the feedback stored in this folder to the company's website, without having to turn it into a dictionary one by one.

Now, navigate back to the `home` directory and create a Python script named `run.py` using the following command:

```bash
cd ~
nano run.py
```

Add the shebang line:

```bash
#! /usr/bin/env python3
```

The following are a few libraries that will be required for the script. Import them using:

```python
import os
import requests
```

The script should now follow the structure:

- List all .txt files under `/data/feedback` directory that contains the actual feedback to be displayed on the company's website.

  **Hint:** Use `os.listdir()` method for this, which returns a list of all files and directories in the specified path.

- You should now have a list that contains all of the feedback files from the path `/data/feedback`. Traverse over each file and, from the contents of these text files, create a dictionary by keeping `title`, `name`, `date`, and `feedback` as keys for the content value, respectively.

- Now, you need to have a dictionary with keys and their respective values (content from feedback files). This will be uploaded through the Django REST API.

- Use the Python `requests` module to post the dictionary to the company's website. Use the request.post() method to make a POST request to `http://<corpweb-external-IP>/feedback`. Replace `<corpweb-external-IP>` with corpweb's external IP address.

- Make sure an error message isn't returned. You can print the status_code and text of the response objects to check out what's going on. You can also use the response `status_code 201` for created success status response code that indicates the request has succeeded.

Save the `run.py` script file by pressing Ctrl-o, the Enter key, and Ctrl-x.

Grant executable permission to the run.py script.

```bash
chmod +x ~/run.py
```

Now, run the `run.py` script:

```bash
./run.py
```

Your POST requests should have successfully uploaded the feedback on the company's website. Now, visit the website again using the `corpweb` external IP address or just refresh the page if already opened, and you should be able to see the feedback.

![7639cece365f6956.png](https://cdn.qwiklabs.com/RBlUCcCZl3ldcQbpDrRNe9%2Fh9w4RM24kgQ7wAFuvsjM%3D)



# Module 3: Sending Emails and Generating PDFs

------

Welcome back! And congratulations on completing yet another tricky lab.

As you get to practice your Python skills you're probably starting to see that there's a lot more to learn out there. And that's true, there's a lot of tools to help us do a ton of different things. But don't panic! You don't need to learn all these tools at the same time. This course is designed to help you get a first taste of some of the tools available, so that you can learn about more tools in the future. As you keep writing more and more programs, you'll keep coming across more and more tools, expanding your Python skills and knowledge.

In this module, we'll look into a different aspect of automation: automating the generation of nicely formatted output from our scripts, like sending emails.

Most of us use email for a bunch of different things, all the time. We type up an email message, sometimes attach a picture or a document, and send it to someone in our contact list. Have you ever used a script to send an email? By the end of this module, you’ll be able to send an email message with an attachment from Python! You'll even learn how to generate PDF files to attach to those emails.

To help with that, we'll look into a bunch of different Python modules that already include a lot of the functionalities that we want. As we've called out, this is one of the great things about Python -- we can use these modules to accomplish what we want with very little code!

We'll show examples of how you can do a bunch of different operations, like creating the contents of the email or the PDF, attaching a file to an email, and even sending the email to an SMTP server. As always, we recommend that you follow along on your own computer, and even try to come up with new ways to use these libraries.

At the end, you'll have the opportunity to put all of this in practice through the lab.

## Introduction to Python Email Library

------

Email messages look simple in an email client. But behind the scenes the client is doing a lot of work to make that happen! Email messages -- even messages with images and attachments -- are actually complicated text structures made entirely of readable strings!

The [**Simple Mail Transfer Protocol (SMTP)**](https://tools.ietf.org/html/rfc2821.html) and [**Multipurpose Internet Mail Extensions (MIME)**](https://tools.ietf.org/html/rfc2045) standards define how email messages are constructed. You *could* read the standards documentation and create email messages all on your own, but you don't need to go to all that trouble. The [email built-in Python module](https://docs.python.org/3/library/email.html) lets us easily construct email messages.

We'll start by using the [email.message.EmailMessage class](https://docs.python.org/3/library/email.message.html#email.message.EmailMessage) to create an empty email message.

```python
>>> from email.message import EmailMessage
>>> message = EmailMessage()
>>> print(message)
```

As usual, printing the message object gives us the string representation of that object. The email library has a function that converts the complex EmailMessage object into something that is fairly human-readable. Since this is an empty message, there isn't anything to see yet. Let's try adding the sender and recipient to the message and see how that looks.

We'll define a couple of variables so that we can reuse them later.

```python
>>> sender = "me@example.com"
>>> recipient = "you@example.com"
```

And now, add them to the From and To fields of the message.

```python
>>> message['From'] = sender
>>> message['To'] = recipient
>>> print(message)
From: me@example.com
To: you@example.com
```

Cool! That's starting to look a bit more like an email message now. How about a subject?

```python
>>> message['Subject'] = 'Greetings from {} to {}!'.format(sender, recipient)
>>> print(message)
From: me@example.com
To: you@example.com
Subject: Greetings from me@example.com to you@example.com!
```

**From**, **To**, and **Subject** are examples of **email header fields**. They’re **key-value pairs** of labels and instructions used by email clients and servers to route and display the email. They’re separate from the email's **message body**, which is the main content of the message.

Let's go ahead and add a message body!

```python
>>> body = """Hey there!
...
... I'm learning to send emails using Python!"""
>>> message.set_content(body)
```

Alright, now what does that look like?

```python
>>> print(message)
From: me@example.com
To: you@example.com
Subject: Greetings from me@example.com to you@example.com!
MIME-Version: 1.0
Content-Type: text/plain; charset="utf-8"
Content-Transfer-Encoding: 7bit
 
Hey there!
 
I'm learning to send email using Python!
```

The message has a body! The **set_content()** method also automatically added a couple of headers that the email infrastructure will use when sending this message to another machine. Remember in an earlier course, when we talked about **character encodings**? The **Content-Type** and **Content-Transfer-Encoding** headers tell email clients and servers how to interpret the bytes in this email message into a string. Now, what about this other header? What is MIME? We'll learn about that next!

## Adding Attachments

------

Remember, email messages are made up completely of strings. When you add an attachment to an email, whatever type the attachment happens to be, it’s encoded as some form of text. The **Multipurpose Internet Mail Extensions (MIME)** standard is used to encode all sorts of files as text strings that can be sent via email. 

Let's dive in and break down how that works.

In order for the recipient of your message to understand what to do with an attachment, you need to label the attachment with a **MIME type** and **subtype** to tell them what sort of file you’re sending. The **Internet Assigned Numbers Authority (IANA)** ([iana.org](https://iana.org/)) [hosts a registry of valid MIME types](https://www.iana.org/assignments/media-types/media-types.xhtml). If you know the correct type and subtype of the files you’ll be sending, you can use those values directly. If you don't know, you can use the Python **mimetypes** module to make a good guess!

```python
>>> import os.path
>>> attachment_path = "/tmp/example.png"
>>> attachment_filename = os.path.basename(attachment_path)
>>> import mimetypes
>>> mime_type, _ = mimetypes.guess_type(attachment_path)
>>> print(mime_type)
image/png
```

Alright, that **mime_type** string contains the MIME type and subtype, separated by a slash. The **EmailMessage** type needs a MIME type and subtypes as separate strings, so let's split this up:

```python
>>> mime_type, mime_subtype = mime_type.split('/', 1)
>>> print(mime_type)
image
>>> print(mime_subtype)
png
```

Now, finally! Let's add the attachment to our message and see what it looks like.

```python
>>> with open(attachment_path, 'rb') as ap:
...     message.add_attachment(ap.read(),
...                            maintype=mime_type,
...                            subtype=mime_subtype,
...                            filename=os.path.basename(attachment_path))
... 
>>> print(message)
Content-Type: multipart/mixed; boundary="===============5350123048127315795=="
 
--===============5350123048127315795==
Content-Type: text/plain; charset="utf-8"
Content-Transfer-Encoding: 7bit
 
Hey there!
 
I'm learning to send email using Python!
 
--===============5350123048127315795==
Content-Type: image/png
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename="example.png"
MIME-Version: 1.0
 
iVBORw0KGgoAAAANSUhEUgAAASIAAABSCAYAAADw69nDAAAACXBIWXMAAAsTAAALEwEAmpwYAAAg
AElEQVR4nO2dd3wUZf7HP8/M9k2nKIJA4BCUNJKgNJWIBUUgEggCiSgeVhA8jzv05Gc5z4KHiqin
eBZIIBDKIXggKIeCRCAhjQAqx4UiCARSt83uzDy/PzazTDZbwy4BnHde+9qZydNn97Pf5/uUIZRS
(...We deleted a bunch of lines here...)
wgAAAABJRU5ErkJggg==
 
--===============5350123048127315795==--
```

The entire message can still be serialized as a text string, including the image that we attached! The email message as a whole has the MIME type "multipart/mixed". Each **part** of the message has its own MIME type. The message body is still there as a "text/plain" part, and the image attachment is a "image/png" part. Cool!

Now, how do we *send* this email message? That's coming up!

## Sending the Email Through an SMTP Server

------

As we called out, to send emails, our computers use the [**Simple Mail Transfer Protocol (SMTP)**](https://tools.ietf.org/html/rfc2821.html). This protocol specifies how computers can deliver email to each other. There are certain steps that need to be followed to do this correctly. But, as usual, we won't do this manually; we’ll send the message using the built-in [smtplib Python module](https://docs.python.org/3/library/smtplib.html). Let's start by importing the module.

```python
>>> import smtplib
```

With smtplib, we'll create an object that will represent our mail server, and handle sending messages to that server. If you’re using a Linux computer, you might already have a configured SMTP server like postfix or sendmail. But maybe not. Let's create a smtplib.SMTP object and try to connect to the local machine.

```python
>>> mail_server = smtplib.SMTP('localhost')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  (...We deleted a bunch of lines here...)
ConnectionRefusedError: [Errno 61] Connection refused
```

Oops! This error means that there's no local SMTP server configured. But don't panic! You can still connect to the SMTP server for your personal email address. Most personal email services have instructions for sending email through SMTP; just search for the name of your email service and "SMTP connection settings".

When setting this up, there are a couple of things that you'll probably need to do: Use a secure transport layer and authenticate to the service using a username and password. Let's see what this means in practice.

You can connect to a remote SMTP server using **Transport Layer Security (TLS)**. An earlier version of the TLS protocol was called **Secure Sockets Layer (SSL)**, and you’ll sometimes see TLS and SSL used interchangeably. This SSL/TLS is the same protocol that's used to add a secure transmission layer to HTTP, making it HTTPS. Within the smtplib, there are two classes for making connections to an SMTP server: The [**SMTP class**](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) will make a direct SMTP connection, and the [**SMTP_SSL class**](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL) will make a SMTP connection over SSL/TLS. Like this:

```python
>>> mail_server = smtplib.SMTP_SSL('smtp.example.com')
```

If you want to see the SMTP messages that are being sent back and forth by the smtplib module behind the scenes, you can set the debug level on the SMTP or SMTP_SSL object. The examples in this lesson won’t show the debug output, but you might find it interesting!

```python
mail_server.set_debuglevel(1)
```

Now that we’ve made a connection to the SMTP server, the next thing we need to do is authenticate to the SMTP server. Typically, email providers wants us to provide a username and password to connect. Let's put the password into a variable so it's not visible on the screen.

```python
>>> import getpass
>>> mail_pass = getpass.getpass('Password? ')
Password?
>>>
```

The example above uses the [getpass module](https://docs.python.org/3/library/getpass.html) so that passers-by won't see the password on the screen. Watch out, though; the **mail_pass** variable is still just an ordinary string!

```python
>>> print(mail_pass)
It'sASecr3t!
```

Now that we have the email user and password configured, we can authenticate to the email server using the SMTP object's [login method](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.login).

```python
>>> mail_server.login(sender, mail_pass)
(235, b'2.7.0 Accepted')
```

If the login attempt succeeds, the login method will return a tuple of the [SMTP status code](https://tools.ietf.org/html/rfc4954#section-6) and a message explaining the reason for the status. If the login attempt fails, the module will raise a [SMTPAuthenticationError](https://docs.python.org/3.8/library/smtplib.html#smtplib.SMTPAuthenticationError) exception.

If you wrote a script to send an email message, how would you handle this exception?

### Sending your message

Alright! We're connected and authenticated to the SMTP server. Now, how do we send the message?

```python
>>> mail_server.send_message(message)
{}
```

Okay, well that last bit was pretty easy! We did the hard part first! The [send_message method](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.send_message) returns a dictionary of any recipients that weren’t able to receive the message. Our message was delivered successfully, so send_message returned an empty dictionary. Finally, now that the email is sent, let's close the connection to the mail server.

```python
>>> mail_server.quit()
```

And there you have it! We covered a lot in this lesson, so let's recap! First, we constructed an email message by using the built-in [email module](https://docs.python.org/3/library/email.html)'s [EmailMessage class](https://docs.python.org/3/library/email.message.html). Next, we added an attachment to our message with the help of the built-in [mimetypes module](https://docs.python.org/3/library/mimetypes.html). Finally, we connected to a SMTP server and sent the email using the smtplib module's 's [SMTP_SSL class](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL).

Did you have any idea all of this was happening behind a simple email message?

## Introduction to Generating PDFs

------

Depending on what your automation does, you might want to generate a PDF report at the end, which lets you decide exactly how you want your information to look like.

There's a few tools in Python that let you generate PDFs with the content that you want. Here, we'll learn about one of them: [**ReportLab**](https://bitbucket.org/rptlab/reportlab/src/default/). ReportLab has a **lot** of different features for creating PDF documents. We'll cover just the basics here, and give you pointers for more information at the end.

For our examples, we'll be mostly using the high-level classes and methods in the **Page Layout and Typography Using Scripts (PLATYPUS)** part of the ReportLab module.

Let's say that I have an awesome collection of fruit, and I want to create a PDF report of all the different kinds of fruit I have! I can easily represent the different kinds of fruit and how much of each I have with a Python dictionary. It might look something like this:

```python
fruit = {
  "elderberries": 1,
  "figs": 1,
  "apples": 2,
  "durians": 3,
  "bananas": 5,
  "cherries": 8,
  "grapes": 13
}

```

Now let's take this information and turn it into a report that we can show off! We're going to use the **SimpleDocTemplate** class to build our PDF. 

```python
>>> from reportlab.platypus import SimpleDocTemplate
>>> report = SimpleDocTemplate("/tmp/report.pdf")
```

The **report** object that we just created will end up generating a PDF using the filename **/tmp/report.pdf**. Now, let's add some content to it! We'll create a title, some text in paragraphs, and some charts and images. For that, we're going to use what reportlab calls **Flowables**. Flowables are sort of like chunks of a document that reportlab can arrange to make a complete report. Let's import some Flowable classes.

```python
>>> from reportlab.platypus import Paragraph, Spacer, Table, Image
```

Each of these items (**Paragraph**, **Spacer**, **Table**, and **Image**) are classes that build individual elements in the final document. We have to tell reportlab what **style** we want each part of the document to have, so let's import some more things from the module to describe style.

```python
>>> from reportlab.lib.styles import getSampleStyleSheet
>>> styles = getSampleStyleSheet()
```

You can make a style all of your own, but we’ll use the default provided by the module for these examples. The **styles** object now contains a default "sample" style. It’s like a dictionary of different style settings. If you've ever written HTML, the style settings will look familiar. For example **h1** represents the style for the first level of headers. Alright, we're finally ready to give this report a title!

```python
>>> report_title = Paragraph("A Complete Inventory of My Fruit", styles["h1"])
```

Let's take a look at what this will look like. We can build the PDF now by using the **build()** method of our report. It takes a list of Flowable elements, and generates a PDF with them.

```python
>>> report.build([report_title])
```

Okay, now let's take a look at the PDF:

![img](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_86YSNzcRjWOmEjc3PY1-Q_bcbba43b212bfe5591e1b701b44a28e2_pasted-image-0.png?expiry=1615420800000&hmac=PB_AhY_sx-INksc540l5ED1E2-2FQnNLIRl1UERXofU)

It's not much, but it's a start!

Up next, we'll look into an interesting Flowable for our reports: Tables.

## Adding Tables to our PDFs

------

Up to now, we've generated an extra simple PDF file, that just includes a title.

Let's spice this up by adding a **Table**. To make a Table object, we need our data to be in a **list-of-lists**, sometimes called a **two-dimensional array**. We have our inventory of fruit in a dictionary. How can we convert a dictionary into a list-of-lists?

```python
>>> table_data = []
>>> for k, v in fruit.items():
...   table_data.append([k, v])
...
>>> print(table_data)
[['elderberries', 1], ['figs', 1], ['apples', 2], ['durians', 3], ['bananas', 5], ['cherries', 8], ['grapes', 13]]
```

Great, we have the list of lists. We can now add it to our report and then generate the PDF file once again by calling the **build** method.

```python
>>> report_table = Table(data=table_data)
>>> report.build([report_title, report_table])
```

And this is how the generated report looks now:

![img](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/dDC4EkhjRs2wuBJIYybNYg_819760c210201ef87129ffcb56d26626_pasted-image-0-1-.png?expiry=1615420800000&hmac=AYlVKg7sn-aS-vYljlDDy0H0ouidWwBG5C2mBPc9cOY)

Okay, it worked! It's not very easy to read, though. Maybe we should add some style to **report_table**. For our example, we'll add a border around all of the cells in our table, and move the table over to the left. **TableStyle** definitions can get pretty complicated, so feel free to take a look at the documentation for a more complete idea of what’s possible.

```python
>>> from reportlab.lib import colors
>>> table_style = [('GRID', (0,0), (-1,-1), 1, colors.black)]
>>> report_table = Table(data=table_data, style=table_style, hAlign="LEFT")
>>> report.build([report_title, report_table])
```

![img](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/mEW73N03StaFu9zdN5rWYw_e6a691a4ab0b80af644ec2ba5890c8ba_pasted-image-0-2-.png?expiry=1615420800000&hmac=HdSmpCkcaa1Dn6Bf2dtXI8czlKCCGA-uJJG-71PXSqs)

Much better! Up next, we'll look into making this more colorful by adding graphs to our reports.

## Adding Graphics to our PDFs

------

Up to now, we've generated a report with a title and a table of data. Next let's add something a little more graphical. What could be better than a fruit pie (graph)?! We’re going to need to use the **Drawing** Flowable class to create a **Pie** chart.

```python
>>> from reportlab.graphics.shapes import Drawing
>>> from reportlab.graphics.charts.piecharts import Pie
>>> report_pie = Pie(width=3*inch, height=3*inch)
```

To add data to our **Pie** chart, we need two separate lists: One for data, and one for labels. Once more, we’re going to have to transform our fruit dictionary into a different shape. For an added twist, let's sort the fruit in alphabetical order:

```python
>>> report_pie.data = []
>>> report_pie.labels = []
>>> for fruit_name in sorted(fruit):
...   report_pie.data.append(fruit[fruit_name])
...   report_pie.labels.append(fruit_name)
...
>>> print(report_pie.data)
[2, 5, 8, 3, 1, 1, 13]
>>> print(report_pie.labels)
['apples', 'bananas', 'cherries', 'durians', 'elderberries', 'figs', 'grapes']
```

The **Pie** object isn’t Flowable, but it can be placed inside of a Flowable ***Drawing\***.

```python
>>> report_chart = Drawing()
>>> report_chart.add(report_pie)
```

Now, we'll add the new Drawing to the report, and see what it looks like.

```python
report.build([report_title, report_table, report_chart])
```

![img](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/kB8L5tDnR_qfC-bQ5xf6MQ_fedb9ca05eec18eb64a7f541e5b855c9_pasted-image-0-3-.png?expiry=1615420800000&hmac=xCkLxVAgyclo2wC7QSkaxPnmXdbIkUFdx7GR_swIxWQ)

Alright, and with that, you've seen a few examples of what we can do with the ReportLab library. There's a ton more things that can be done that we won't cover here. You'll want to refer to the [ReportLab User Guide](https://www.reportlab.com/docs/reportlab-userguide.pdf) for more details on the features we've seen, and to see what else you can create with it.

By the way, the ReportLab User Guide is a PDF that [is generated using reportlab](https://bitbucket.org/rptlab/reportlab/src/default/docs/)! Cool, right?

## Project Problem Statement

------

It's that time again, time to flex your programming muscles and practice solving a real-life problem with the skills you acquired!

In the next lab, you'll have to process information related to the sales your company generated last month, and turn that into a nicely formatted PDF report that you'll then send by email so that your boss can look at it. The lab machine has email configured so that you can check your resulting emails through a nice webmail interface that's already up and running.

The system that you'll work with already includes some scripts that will do part of the work for you. You'll need to put these pieces together to get the result you want, basing your code on the one that's already there.

As we called out before, solving these problems can take some time, and that's ok! Solving complex problems is the best way to really master your coding skills. Before you start the lab, make sure you understand what you need to do and that you know how you want to solve it. Nobody is rushing you, so take as much time as you need, review any concepts that are not totally clear, and then get to it.

Good luck, you can totally do this!

### **Introduction**

You work for a company that sells second hand cars. Management wants to get a summary of the amounts of vehicles that have been sold at the end of every month. The company already has a web service which serves sales data at the end of every month but management wants an email to be sent out with an attached PDF so that data is more easily readable.

### **What you’ll do**

- Write a script that summarizes and processes sales data into different categories
- Generate a PDF using Python
- Automatically send a PDF by email 

## Sample report

In this section, you will be creating a PDF report named "**A Complete Inventory of My Fruit**". The script to generate this report and send it by email is already pre-done. You can have a look at the script in the `scripts/` directory.

```bash
ls ~/scripts
```

Output:

![d88741641edb4e4e.png](https://cdn.qwiklabs.com/rUInm6B0Qy3UeH1XXEKCEVy2UZy4e1uZYzGiRqs%2BbA8%3D)

In the `scripts/` directory, you will find `reports.py` and `emails.py` files. These files are used to **generate PDF files** and **send emails** respectively.

Take a look at these files using `cat` command.

```bash
cat ~/scripts/reports.py
```

Output:

![86bd37a685f9718e.png](https://cdn.qwiklabs.com/i56VdMuHLeKKX3Os%2BNgWUppDi4eysFfbqvSqMTu3J8w%3D)

```bash
cat ~/scripts/emails.py
```

Output:

![a8e8db253f010864.png](https://cdn.qwiklabs.com/gF3Hv%2B59YaeH2he4EtWf1Fb6LkH989IlBv%2FpBgnOtlI%3D)

Now, take a look at `example.py`, which uses these two modules **reports** and **emails** to create a report and then send it by email.

```bash
cat ~/scripts/example.py
```

Grant executable permission to the `example.py` script.

```bash
sudo chmod o+wx ~/scripts/example.py
```

Run the `example.py` script, which will generate mail to you.

```bash
./scripts/example.py
```

A mail should now be successfully sent.

Copy the `external IP address` of your instance from the Connection Details Panel on the left side and open a new web browser tab and enter the IP address. The Roundcube Webmail login page appears.

Here, you'll need a login to **roundcube** using the username and password mentioned in the Connection Details Panel on the left hand side, followed by clicking **Login**.

![10a23ccdb979a002.png](https://cdn.qwiklabs.com/OXW2yZtaYTQ%2BZTVIcMUspBmZBCkBmmTQUEppra6WwMI%3D)

Now you should be able to see your inbox, with one unread email. Open the mail by double clicking on it. There should be a report in PDF format attached to the mail. View the report by opening it.

Output:

![41a28598157d4729.png](https://cdn.qwiklabs.com/Jkzel%2BFKxrzSvwCNotGofHYqCi3Nztd2GEWTcGAirY0%3D)

### Generate report

Now, let's make a couple of changes in the `example.py` file to add a new fruit and change the sender followed by granting editor permission. Open `example.py` file using the following command:

```bash
nano ~/scripts/example.py
```

And update the following variables:

| **variable_name** | **value**                                                    |
| ----------------- | ------------------------------------------------------------ |
| sender            | Replace **sender@example.com** with **automation@example.com** |
| table_data        | Add another entry into the list: `['kiwi', 4, 0.49]`         |

The file should now look similar to:

```python
#!/usr/bin/env python3
import emails
import os
import reports
table_data=[
  ['Name', 'Amount', 'Value'],
  ['elderberries', 10, 0.45],
  ['figs', 5, 3],
  ['apples', 4, 2.75],
  ['durians', 1, 25],
  ['bananas', 5, 1.99],
  ['cherries', 23, 5.80],
  ['grapes', 13, 2.48],
  ['kiwi', 4, 0.49]]
reports.generate("/tmp/report.pdf", "A Complete Inventory of My Fruit", "This is all my fruit.", table_data)
sender = "automation@example.com"
receiver = "{}@example.com".format(os.environ.get('USER'))
subject = "List of Fruits"
body = "Hi\n\nI'm sending an attachment with all my fruit."
message = emails.generate(sender, receiver, subject, body, "/tmp/report.pdf")
emails.send(message)
```

Once you've made the changes in the `example.py` script, save the file by typing **Ctrl-o**, **Enter** key and **Ctrl-x**.

Now execute the example script again.

```bash
./scripts/example.py
```

Now, check the webmail for any new mail. You can click on the **Refresh** button to refresh your inbox.

![6f55d4c2f3ad0c4.png](https://cdn.qwiklabs.com/x4bb%2B2%2Fkwck7d7SXgVjzbmHiqAhVFyLsKzwugFGGpQ4%3D)

## Sales summary

In this section, let's view the summary of last month's sales for all the models offered by the company. This data is in a JSON file named `car_sales.json`. Let's have a look at it.

```bash
cat car_sales.json
```

Output:

![dccac1f426670528.png](https://cdn.qwiklabs.com/A2aAqrGDdDqk0sbLXhXAl%2FluSkUdrypVdWv5qYyRgwo%3D)

To simplify the JSON structure, here is an example of one of the JSON objects among the list.

```json
{
        "id": 47,
        "car": {
                "car_make": "Lamborghini",
                "car_model": "Murciélago",
                "car_year": 2002
        },
        "price": "$13724.05",
        "total_sales": 149
}
content_copy
```

Here `id, car, price and total_sales` are the field names (key).

The script `cars.py` already contains part of the work, but learners need to complete the task by writing the remaining pieces. The script already calculates the car model with the most revenue (price * total_sales) in the `process_data` method. Learners need to add the following:

- Calculate the car model which had the most sales by completing the process_data method, and then appending a formatted string to the `summary` list in the below format:
  - `"The {car model} had the most sales: {total sales}"`

- Calculate the most popular car_year across all car make/models (in other words, find the total count of cars with the car_year equal to 2005, equal to 2006, etc. and then figure out the most popular year) by completing the `process_data` method, and append a formatted string to the `summary` list in the below format:
  - `"The most popular year was {year} with {total sales in that year} sales."`

### The challenge

Here, you are going to update the script `cars.py`. You will be using the above JSON data to process information. A part of the script is already done for you, where it calculates the car model with the most revenue (price * total_sales). You should now fulfil the following objectives with the script:

- Calculate the car model which had the most sales.

- Call `format_car` method for the car model.

- Calculate the most popular `car_year` across all car make/models.

**Hint:** Find the total count of cars with the car_year equal to 2005, equal to 2006, etc. and then figure out the most popular year.

Grant required permissions to the file `cars.py` and open it using nano editor.

```
sudo chmod o+wx ~/scripts/cars.py
content_copy
nano ~/scripts/cars.py
content_copy
```

The code is well commented including the TODO sections for you to understand and fulfill the objectives.

### Generate PDF and send Email

Once the data is collected, you will also need to further update the script to generate a PDF report and automatically send it through email.

To generate a PDF:

- Use the `reports.generate()` function within the main function.

- The report should be named as **cars.pdf**, and placed in the folder **/tmp/**.

- The PDF should contain:

  - A summary paragraph which contains the most sales/most revenue/most popular year values worked out in the previous step.

  **Note:** To add line breaks in the PDF, use: <br/> between the lines.

  - A table which contains all the information parsed from the JSON file, organised by id_number. The car details should be combined into one column in the form <car_make> <car_model> (<car_year>).

  **Note:** You can use the **cars_dict_to_table** function for the above task.

Example:

| **ID** | **Car**              | **Price** | **Total Sales** |
| ------ | -------------------- | --------- | --------------- |
| 47     | Acura TL (2007)      | €14459,15 | 1192            |
| 73     | Porsche 911 (2010)   | €6057,74  | 882             |
| 85     | Mercury Sable (2005) | €45660,46 | 874             |

To send the PDF through email:

Once the PDF is generated, you need to send the email, using the `emails.generate()` and `emails.send()` methods.

Use the following details to pass the parameters to `emails.generate()`:

- **From:** automation@example.com
- **To:** <user>@example.com
- **Subject line**: Sales summary for last month
- **E-mail Body:** The same summary from the PDF, but using `\n` between the lines
- **Attachment:** Attach the PDF path i.e. generated in the previous step

Once you have completed editing `cars.py` script, save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Run the `cars.py` script, which will generate mail to their user.

```bash
./scripts/cars.py
```

Now, check the webmail for any new mail. You can click on the **Refresh** button to refresh your inbox.

Output:

![e066799de7dd10fe.png](https://cdn.qwiklabs.com/EGbZxG2RRNc%2F%2B70k%2FDDPpXB1l6Wza4ZSNTZba4rdYWo%3D)

Open `cars.pdf` that's located on the right most side.



![15f205f9bf5782f5.png](https://cdn.qwiklabs.com/pPYYMs48r3Z3qP7wkDJqi6uiOj%2F3YMtC8%2BH0wAhC0AA%3D)

## Optional challenge

As **optional** challenges, you could try some of the following functionalities:

1. Sort the list of cars in the PDF by total sales.
2. Create a pie chart for the total sales of each car made.
3. Create a bar chart showing total sales for the top 10 best selling vehicles using the [ReportLab Diagra library](https://www.reportlab.com/software/diagra/). Put the vehicle name on the X-axis and **total revenue** (remember, price * total sales!) along the Y-axis.

# Module 4: Final Course Project

------

Great job, you've made it to the final module! You’ve come so far! Can you believe how much you’ve learned?

In the past few modules, you've seen how you can modify images using Python Imaging Library; how you can interact with web services using the Python requests module, sending data in JSON format; how you can generate PDF files with the content you want; and how you can send emails with those PDFs as an attachment. 

For the final project in this course, you’ll use the techniques and concepts you've seen to build a solution to a complex IT task. This can seem a bit daunting at first, but don't worry, you already have all the tools to solve this task!

In the next couple of readings, we're going to get into what to expect, and some things you should keep in mind when writing your solution.

## Project Problem Statement

------

Okay, here's the scenario:

You work for an online fruit store, and you need to develop a system that will update the catalog information with data provided by your suppliers. When each supplier has new products for your store, they give you an image and a description of each product.

Given a bunch of images and descriptions of each of the new products, you’ll:

- Upload the new products to your online store. Images and descriptions should be uploaded separately, using two different web endpoints.
- Send a report back to the supplier, letting them know what you imported.

Since this process is key to your business's success, you need to make sure that it keeps running! So, you’ll also:

- Run a script on your web server to monitor system health.
- Send an email with an alert if the server is ever unhealthy.

Hopefully this summary has helped you start thinking about how you’ll approach this task. In case you’re feeling a little scared, don't worry, you can definitely do this! You have all the necessary tools, and the lab description will go into a lot more detail of what you need to do.

Up next, we'll give you a few tips that can help you along the way.

## How to Approach the Problem

------

We're giving you a pretty big project to do at the end of this course -- but you can totally complete it with what you've learned until now! Take your time, and be methodical. Use these tips to help you:

**Break the problem down into smaller pieces.** If you’re not sure how to solve a piece of the puzzle, look for an even smaller piece that you *can* solve. Build up those smaller pieces into a larger solution!

**Make one change at a time.** Write unit tests to make sure that each new part of the solution works the way you think it does. Run your unit tests frequently to make sure that each part of your solution **keeps working** as you make changes.

**Use version control.** Check each part of your solution into version control as you complete it, so you can always roll back to a known version of your code if you make a mistake.

***Review module documentation!\*** You are going to need to use these modules to complete the final project. Reading the documentation takes time, but as you become more familiar with the APIs provided by these modules, it could save you from writing a bunch of custom code that could have just been a call to a module function! Remember, we’ve covered these modules in previous lessons too, so feel free to go back and review them if you need a refresher!

- [Python Image Library (PIL)](https://pillow.readthedocs.io/) - [Tutorial](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html)

- [Requests](https://requests.readthedocs.io/) (HTTP client library) - [Quickstart](https://requests.readthedocs.io/en/master/user/quickstart/)

- [ReportLab](https://www.reportlab.com/docs/reportlab-userguide.pdf) (PDF creation library)
- [email](https://docs.python.org/3/library/email.examples.html) (constructing email)
- [psutil](https://psutil.readthedocs.io/) (processes and system utilization)
- [shutil](https://docs.python.org/3/library/shutil.html) (file operations)
- [smtplib](https://docs.python.org/3/library/smtplib.html) (sending email)

***Read the lab instructions carefully!\*** Following the instructions and implementing your solution to the specifications that you’re given are critical to completing the task, and to being accurately graded! 

## **Introduction**

You work for an online fruits store, and you need to develop a system that will update the catalog information with data provided by your suppliers. The suppliers send the data as large images with an associated description of the products in two files (.TIF for the image and .txt for the description). The images need to be converted to smaller jpeg images and the text needs to be turned into an HTML file that shows the image and the product description. The contents of the HTML file need to be uploaded to a web service that is already running using Django. You also need to gather the name and weight of all fruits from the .txt files and use a Python request to upload it to your Django server.

You will create a Python script that will process the images and descriptions and then update your company's online website to add the new products.

Once the task is complete, the supplier should be notified with an email that indicates the total weight of fruit (in lbs) that were uploaded. The email should have a PDF attached with the name of the fruit and its total weight (in lbs). 

Finally, in parallel to the automation running, we want to check the health of the system and send an email if something goes wrong. 

## **What you’ll do**

- Write a script that summarizes and processes sales data into different categories 
- Generate a PDF using Python
- Automatically send a PDF by email 
- Write a script to check the health status of the system 

## Fetching supplier data

You'll first need to get the information from the supplier that is currently stored in a Google Drive file. The supplier has sent data as large images with an associated description of the products in two files (.TIF for the image and .txt for the description).

Here, you'll find two script files `download_drive_file.sh` and the `example_upload.py` files. You can view it by using the following command.

```bash
ls ~/
```

Output:

![19cdba5cb97d3091.png](https://cdn.qwiklabs.com/oZa6n6ycZXfdecHuhLeD9euSrlh%2Fefq7A6qzL2zx4ug%3D)

To download the file from the supplier onto our `linux-instance` virtual machine we will first grant executable permission to the `download_drive_file.sh` script.

```bash
sudo chmod +x ~/download_drive_file.sh
```

Run the `download_drive_file.sh` shell script with the following arguments:

```bash
./download_drive_file.sh 1LePo57dJcgzoK4uiI_48S01Etck7w_5f supplier-data.tar.gz
```

Output:

![fa96a73a09a0fb81.png](https://cdn.qwiklabs.com/cY7GAoO%2FDl5UHWHlnjNcpZtC3Zo8NzMN6hFcdAvfNDU%3D)

You have now downloaded a file named `supplier-data.tar.gz` containing the supplier's data. Let's extract the contents from this file using the following command:

```\
tar xf ~/supplier-data.tar.gz
```

This creates a directory named `supplier-data`, that contains subdirectories named `images` and `descriptions`.

![2ba417715369f867.png](https://cdn.qwiklabs.com/5ft5dMC5m7MF2HDYCSg%2BZ5Q9pfYgMFzUOSgqu0aWECo%3D)

List contents of the `supplier-data` directory using the following command:

```bash
ls ~/supplier-data
```

Output:

![3fb0e0016e2bb0f7.png](https://cdn.qwiklabs.com/HTrio1kwEPHbufRsHN%2BjTDd7vkef4o32I9UWm3Jl9VA%3D)

The subdirectory `images` contain images of various fruits, while the `descriptions` subdirectory has text files containing the description of each fruit. You can have a look at any of these text files using `cat` command.

```bash
cat ~/supplier-data/descriptions/007.txt
```

Output:

![3047a30cc5caf228.png](https://cdn.qwiklabs.com/nVGspBqLFe%2BBtyTK2EDZu3rLxFJr30tgPez%2Blbbp9fQ%3D)

The first line contains the name of the fruit followed by the weight of the fruit and finally the description of the fruit.

## Working with supplier images

In this section, you will write a Python script named `changeImage.py` to process the supplier images. You will be using the PIL library to update all images within ~`/supplier-data/images` directory to the following specifications:

- **Size**: Change image resolution from **3000x2000** to **600x400** pixel
- **Format**: Change image format from **.TIFF** to **.JPEG**

Create and open the file using nano editor.

```python
nano ~/changeImage.py
```

Add a shebang line in the first line.

```python
#!/usr/bin/env python3
```

This is the challenge section, where you will be writing a script that satisfies the above objectives.

**Note:** The raw images from `images` subdirectory contains alpha transparency layers. So, it is better to first convert `RGBA` 4-channel format to `RGB` 3-channel format before processing the images. Use convert("RGB") method for converting RGBA to RGB image.

After processing the images, save them in the same path `~/supplier-data/images`, with a JPEG extension.

Once you have completed editing the `changeImage.py` script, save the file by clicking **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Grant executable permissions to the `changeImage.py` script.

```bash
sudo chmod +x ~/changeImage.py=
```

Now run the `changeImage.py` script:

```bash
./changeImage.py=
```

Now, let's check the specifications of the images you just updated. Open any image using the following command:

```bash
file ~/supplier-data/images/003.jpeg=
```

Output:

![48b82d8d8a4f3c51.png](https://cdn.qwiklabs.com/nE8H4Vo8aI5yHiEuRy86b0Wb9soj144dHeNhYejdFq0%3D)



## Uploading images to web server

You have modified the fruit images through `changeImage.py` script. Now, you will have to upload these modified images to the web server that is handling the fruit catalog. To do that, you'll have to use the Python `requests` module to send the file contents to the `[linux-instance-IP-Address]/upload` URL.

Copy the `external IP address` of your instance from the Connection Details Panel on the left side and enter the IP address in a new web browser tab. This opens a web page displaying the text "`Fruit Catalog`".

In the home directory, you'll have a script named `example_upload.py` to upload images to the running fruit catalog web server. To view the `example_upload.py` script use the `cat` command.

```bash
cat ~/example_upload.py
```

Output:

![d1a53f8b31586d73.png](https://cdn.qwiklabs.com/9yJABmfzWCPRfvhKEPYiqdR9teLcxpG%2Bn8xaenQbucs%3D)

In this script, we are going to upload a sample image named `icon.sheet.png`.

Grant executable permission to the `example_upload.py` script.

```bash
sudo chmod +x ~/example_upload.py
```

Execute the `example_upload.py` script, which will upload the images.

```bash
./example_upload.p
```

Now check out that the file `icon.sheet.png` was uploaded to the web server by visiting the URL `[linux-instance-IP-Address]/media/images/`, followed by clicking on the file name.

Output:

![2ff93301dabfc549.png](https://cdn.qwiklabs.com/rEdNe73TPnSnB4aiLMzl0clBHTeYHWrwRNEYTL2EEm4%3D)

In a similar way, you are going to write a script named `supplier_image_upload.py` that takes the **jpeg** images from the `supplier-data/images` directory that you've processed previously and uploads them to the web server fruit catalog.

Use the nano editor to create a file named `supplier_image_upload.py`:

```bash
nano ~/supplier_image_upload.py
```

Complete the script with the same technique as used in the file `example_upload.py`.

Once you have completed editing the `supplier_image_upload.py` script, save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Grant executable permission to the `supplier_image_upload.py` script.

```bash
sudo chmod +x ~/supplier_image_upload.py
```

Run the `supplier_image_upload.py` script.

```bash
./supplier_image_upload.py
```

Refresh the URL opened earlier, and now you should find all the images uploaded successfully.

Output:

![1664f43929363847.png](https://cdn.qwiklabs.com/D21DfEDXkfgBjiVA2%2FNjHedxh22tBmPLhx61U2GkXbw%3D)

## Uploading the descriptions

The Django server is already set up to show the fruit catalog for your company. You can visit the main website by entering `linux-instance-IP-Address` in the URL bar or by removing /media/images from the existing URL opened earlier. The interface looks like this:

![3c3e31b6d0ca1038.png](https://cdn.qwiklabs.com/JWxbvtE2tFc%2F0cgPNlv8%2F1xYgnpDxjmXjR2gI%2FlUP44%3D)

Check out the Django REST framework, by navigating to `linux-instance-IP-Address/fruits` in your browser.

![44aaa38049449875.png](https://cdn.qwiklabs.com/ZPQ%2BmfewKIAeESZLRCjUkjqmZ5DQFKxxmkHVKhtirnk%3D)

Currently, there are no products in the fruit catalog web-server. You can create a test fruit entry by entering the following into the **content** field:

```
{"name": "Test Fruit", "weight": 100, "description": "This is the description of my test fruit", "image_name": "icon.sheet.png"}
```

After entering the above data into the content field click on the POST button. Now visit the main page of your website (by going to `http://[linux-instance-external-IP]/`), and the new test fruit you uploaded appears.

![d72416aaf9bb08c3.png](https://cdn.qwiklabs.com/ZxpDdwsTvAW48PonnnIRepsamtLOQNztvqhzhKgrnro%3D)

To add fruit images and their descriptions from the supplier on the fruit catalog web-server, create a new Python script that will automatically POST the **fruit images** and their respective **description** in JSON format.

Write a Python script named `run.py` to process the text files (001.txt, 003.txt ...) from the `supplier-data/descriptions` directory. The script should turn the data into a JSON dictionary by adding all the required fields, including the image associated with the fruit (image_name), and uploading it to `http://[linux-instance-external-IP]/fruits` using the Python **requests** library.

Create `run.py` using the nano editor:

```bash
nano ~/run.py
```

Add the shebang line and import necessary libraries.

```bash
#! /usr/bin/env python3

import os
import requests
```

Now, you'll have to process the .txt files (named `001.txt, 002.txt, ...`) in the `supplier-data/descriptions/` directory and save them in a data structure so that you can then upload them via JSON. Note that all files are written in the following format, with each piece of information on its own line:

- name
- weight (in lbs)
- description

The data model in the Django application `fruit` has the following fields: `name`, `weight`, `description` and `image_name`. The `weight` field is defined as an **integer** field. So when you process the weight information of the fruit from the .txt file, you need to convert it into an integer. For example if the weight is "**500 lbs**", you need to **drop "lbs"** and **convert "500" to an integer**.

The `image_name` field will allow the system to find the image associated with the fruit. Don't forget to add all fields, including the `image_name`! The final JSON object should be similar to:

```
{"name": "Watermelon", "weight": 500, "description": "Watermelon is good for relieving heat, eliminating annoyance and quenching thirst. It contains a lot of water, which is good for relieving the symptoms of acute fever immediately. The sugar and salt contained in watermelon can diuretic and eliminate kidney inflammation. Watermelon also contains substances that can lower blood pressure.", "image_name": "010.jpeg"}
```

Iterate over all the fruits and use **post** method from Python requests library to upload all the data to the URL `http://[linux-instance-external-IP]/fruits`

Once you complete editing `run.py` script, save the file by clicking **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Grant executable permission to the `run.py` script.

```bash
sudo chmod +x ~/run.py
```

Run the `run.py` script:

```bash
./run.py
```

Now go to the main page of your website (by going to `http://[linux-instance-IP-Address]/`) and check out how the new fruits appear.

![202677b175787ed9.png](https://cdn.qwiklabs.com/T6xJ3BXTcGFy%2FTfQ8B25zRLl4ffCStGL6XCjDLHiUPs%3D)

## Generate a PDF report and send it through email

Once the `images` and `descriptions` have been uploaded to the fruit store web-server, you will have to generate a PDF file to send to the supplier, indicating that the data was correctly processed. To generate PDF reports, you can use the `ReportLab` library. The content of the report should look like this:

**Processed Update on <Today's date>**

[blank line]

name: Apple

weight: 500 lbs

[blank line]

name: Avocado

weight: 200 lbs

[blank line]

...

### Script to generate a PDF report

Create a script `reports.py` to generate PDF report to supplier using the nano editor:

```bash
nano ~/reports.py
```

Add a shebang line in the first line.

```bash
#!/usr/bin/env python3
```

Using the `reportlab` Python library, define the method `generate_report` to build the PDF reports. We have already covered how to generate PDF reports in an earlier lesson; you will want to use similar concepts to create a PDF report named **processed.pdf**.

Once you have finished editing the script `reports.py`, save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Create another script named `report_email.py` to process supplier fruit description data from `supplier-data/descriptions` directory. Use the following command to create `report_email.py`.

```bash
nano ~/report_email.py
```

Add a shebang line.

```bash
#!/usr/bin/env python3
```

Import all the necessary libraries(`os`, `datetime` and `reports`) that will be used to process the text data from the `supplier-data/descriptions` directory into the format below:

name: Apple

weight: 500 lbs

[blank line]

name: Avocado

weight: 200 lbs

[blank line]

...

Once you have completed this, call the main method which will process the data and call the `generate_report` method from the `reports` module:

```bash
if __name__ == "__main__":
```

You will need to pass the following arguments to the `reports.generate_report` method: the text description processed from the text files as the `paragraph` argument, the report title as the `title` argument, and the file path of the PDF to be generated as the `attachment` argument (use ‘`/tmp/processed.pdf`')

```bash
  reports.generate_report(attachment, title, paragraph)
```

Once you have completed the `report_email.py` script. Save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

### Send report through email

Once the PDF is generated, you need to send the email using the `emails.generate_email()` and `emails.send_email()` methods.

Create `emails.py` using the nano editor using the following command:

```bash
nano ~/emails.py
```

Define `generate_email` and `send_email` methods by importing necessary libraries.

Once you have finished editing the `emails.py` script, save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Now, open the `report_email.py` script using the nano editor:

```bash
nano ~/report_email.py
```

Once you define the `generate_email` and `send_email` methods, call the methods under the main method after creating the PDF report:

```bash
if __name__ == "__main__":
```

Use the following details to pass the parameters to `emails.generate_email()`:

- **From:** automation@example.com

- To:

   

  username@example.com

  - Replace `username` with the `username` given in the Connection Details Panel on the right hand side.

- **Subject line**: Upload Completed - Online Fruit Store

- **E-mail Body:** All fruits are uploaded to our website successfully. A detailed list is attached to this email.

- **Attachment:** Attach the path to the file `processed.pdf`

Once you have finished editing the `report_email.py` script, save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Grant executable permissions to the script `report_email.py`.

```bash
sudo chmod +x ~/report_email.py
```

Run the `report_email.py` script.

```bash
./report_email.py
```

Now, check the webmail by visiting `[linux-instance-external-IP]/webmail`. Here, you'll need a login to **roundcube** using the username and password mentioned in the Connection Details Panel on the left hand side, followed by clicking **Login**.

Now you should be able to see your inbox, with one unread email. Open the mail by double clicking on it. There should be a report in PDF format attached to the mail. View the report by opening it.

Output:

![20ecb14552c7fd28.png](https://cdn.qwiklabs.com/JxgPNyddBbHW4tIT1XD6chuuJOtcTBR4obwZc9MBneA%3D)



## Health check

This is the last part of the lab, where you will have to write a Python script named `health_check.py` that will run in the background monitoring some of your system statistics: CPU usage, disk space, available memory and name resolution. Moreover, this Python script should send an email if there are problems, such as:

- Report an error if CPU usage is over 80%
- Report an error if available disk space is lower than 20%
- Report an error if available memory is less than 500MB
- Report an error if the hostname "localhost" cannot be resolved to "127.0.0.1"

Create a python script named `health_check.py` using the nano editor:

```bash
nano ~/health_check.py
```

Add a shebang line.

```bash
#!/usr/bin/env python3
```

Import the necessary Python libraries (eg. shutil, psutil) to write this script.

Complete the script to check the system statistics every 60 seconds, and in event of any issues detected among the ones mentioned above, an email should be sent with the following content:

- **From:** automation@example.com

- To:

   

  username@example.com

  - Replace `username` with the `username` given in the Connection Details Panel on the right hand side.

- Subject line

  :

  | **Case**                                               | **Subject line**                                  |
  | ------------------------------------------------------ | ------------------------------------------------- |
  | CPU usage is over 80%                                  | Error - CPU usage is over 80%                     |
  | Available disk space is lower than 20%                 | Error - Available disk space is less than 20%     |
  | available memory is less than 500MB                    | Error - Available memory is less than 500MB       |
  | hostname "localhost" cannot be resolved to "127.0.0.1" | Error - localhost cannot be resolved to 127.0.0.1 |

- **E-mail Body:** Please check your system and resolve the issue as soon as possible.

**Note:** There is no attachment file here, so you must be careful while defining the generate_email() method in the `emails.py` script or you can create a separate generate_error_report() method for handling non-attachment email.

Once you have completed the `health_check.py` script. Save the file by typing **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Grant executable permissions to the script `health_check.py`.

```bash
sudo chmod +x ~/health_check.py
```

Run the file.

```bash
./health_check.py
```

Next, go to the webmail inbox and refresh it. There should only be an email something goes wrong, so hopefully you don't see a new email.

Output:

![f9c9477ca64b4b6e.png](https://cdn.qwiklabs.com/yCiv8AiTBvFkvQb1o93nAlf2fWkIbS%2FRSOANFxdCYQM%3D)

To test out your script, you can install the `stress` tool.

```bash
sudo apt install stress
```

Next, call the tool using a good number of CPUs to fully load our CPU resources:

```bash
stress --cpu 8
```

Allow the stress test to run, as it will maximize our CPU utilization. Now run `health_check.py` by opening another SSH connection to the `linux-instance.` Navigate to `Accessing the virtual machine` on the navigation pane on the right-hand side to open another connection to the instance.

Now run the script:

```bash
./health_check.py
```

Check your inbox for any new email.

Output:

![c179392b8b65cd7f.png](https://cdn.qwiklabs.com/17yEGmfRw9VTXyx21kJzkb9TSgPMj9GIaePsLG8siB4%3D)

Open the email with the subject "Error - CPU usage is over 80%" by double clicking it.

![2f3df5a11070691e.png](https://cdn.qwiklabs.com/7o7xptowOPJbmcferNUOeYGFQj4EJYvSxEVu8oO%2B2oY%3D)



Close the `stress --cpu` command by clicking **Ctrl-c**.

Now, you will be setting a cron job that executes the script `health_check.py` every 60 seconds and sends health status to the respective user.

To set a user cron job use the following command:

```bash
crontab -e
```

Output:

![crontab-update.png](https://cdn.qwiklabs.com/%2FFOC%2BLjj%2BUu03wWQZvjxdxlTdNHPXSMCcEGLQTOB4gM%3D)

Enter 1 to open in the nano editor. Now, set the complete path for `health_check.py` script, and save by clicking **Ctrl-o**, **Enter** key, and **Ctrl-x**.

Output:

![crontab-edited-image.png](https://cdn.qwiklabs.com/U46V%2Fm1wNxLVvuut0fFPAVYTZxdbg%2FMZp28TmcJv4JY%3D)

# Tutorials

------

## Pillow Tutorial

### Using the Image class

The most important class in the Python Imaging Library is the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) class, defined in the module with the same name. You can create instances of this class in several ways; either by loading images from files, processing other images, or creating images from scratch.

To load an image from a file, use the [`open()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.open) function in the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#module-PIL.Image) module:

```python
>>> from PIL import Image
>>> im = Image.open("hopper.ppm")
```

If successful, this function returns an [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) object. You can now use instance attributes to examine the file contents:

```python
>>> print(im.format, im.size, im.mode)
PPM (512, 512) RGB
```

The [`format`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.format) attribute identifies the source of an image. If the image was not read from a file, it is set to None. The size attribute is a 2-tuple containing width and height (in pixels). The [`mode`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.mode) attribute defines the number and names of the bands in the image, and also the pixel type and depth. Common modes are “L” (luminance) for greyscale images, “RGB” for true color images, and “CMYK” for pre-press images.

If the file cannot be opened, an [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError) exception is raised.

Once you have an instance of the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) class, you can use the methods defined by this class to process and manipulate the image. For example, let’s display the image we just loaded:

```python
>>> im.show()
```

> **Note**
>
> The standard version of [`show()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.show) is not very efficient, since it saves the image to a temporary file and calls a utility to display the image. If you don’t have an appropriate utility installed, it won’t even work. When it does work though, it is very handy for debugging and tests.

The following sections provide an overview of the different functions provided in this library.

### Reading and writing images

The Python Imaging Library supports a wide variety of image file formats. To read files from disk, use the [`open()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.open) function in the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#module-PIL.Image) module. You don’t have to know the file format to open a file. The library automatically determines the format based on the contents of the file.

To save a file, use the [`save()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.save) method of the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) class. When saving files, the name becomes important. Unless you specify the format, the library uses the filename extension to discover which file storage format to use.

#### Convert files to JPEG

```python
import os, sys
from PIL import Image

for infile in sys.argv[1:]:
    f, e = os.path.splitext(infile)
    outfile = f + ".jpg"
    if infile != outfile:
        try:
            with Image.open(infile) as im:
                im.save(outfile)
        except OSError:
            print("cannot convert", infile)
```

A second argument can be supplied to the [`save()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.save) method which explicitly specifies a file format. If you use a non-standard extension, you must always specify the format this way:

#### Create JPEG thumbnails

```python
import os, sys
from PIL import Image

size = (128, 128)

for infile in sys.argv[1:]:
    outfile = os.path.splitext(infile)[0] + ".thumbnail"
    if infile != outfile:
        try:
            with Image.open(infile) as im:
                im.thumbnail(size)
                im.save(outfile, "JPEG")
        except OSError:
            print("cannot create thumbnail for", infile)
```

It is important to note that the library doesn’t decode or load the raster data unless it really has to. When you open a file, the file header is read to determine the file format and extract things like mode, size, and other properties required to decode the file, but the rest of the file is not processed until later.

This means that opening an image file is a fast operation, which is independent of the file size and compression type. Here’s a simple script to quickly identify a set of image files:

#### Identify Image Files

```python
import sys
from PIL import Image

for infile in sys.argv[1:]:
    try:
        with Image.open(infile) as im:
            print(infile, im.format, f"{im.size}x{im.mode}")
    except OSError:
        pass
```

### Cutting, pasting, and merging images

The [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) class contains methods allowing you to manipulate regions within an image. To extract a sub-rectangle from an image, use the [`crop()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.crop) method.

#### Copying a subrectangle from an image

```python
box = (100, 100, 400, 400)
region = im.crop(box)
```

The region is defined by a 4-tuple, where coordinates are (left, upper, right, lower). The Python Imaging Library uses a coordinate system with (0, 0) in the upper left corner. Also note that coordinates refer to positions between the pixels, so the region in the above example is exactly 300x300 pixels.

The region could now be processed in a certain manner and pasted back.

#### Processing a subrectangle, and pasting it back

```python
region = region.transpose(Image.ROTATE_180)
im.paste(region, box)
```

When pasting regions back, the size of the region must match the given region exactly. In addition, the region cannot extend outside the image. However, the modes of the original image and the region do not need to match. If they don’t, the region is automatically converted before being pasted (see the section on [Color transforms](https://pillow.readthedocs.io/en/stable/handbook/tutorial.html#color-transforms) below for details).

Here’s an additional example:

#### Rolling an image

```python
def roll(image, delta):
    """Roll an image sideways."""
    xsize, ysize = image.size

    delta = delta % xsize
    if delta == 0: return image

    part1 = image.crop((0, 0, delta, ysize))
    part2 = image.crop((delta, 0, xsize, ysize))
    image.paste(part1, (xsize-delta, 0, xsize, ysize))
    image.paste(part2, (0, 0, xsize-delta, ysize))

    return image
```

For more advanced tricks, the paste method can also take a transparency mask as an optional argument. In this mask, the value 255 indicates that the pasted image is opaque in that position (that is, the pasted image should be used as is). The value 0 means that the pasted image is completely transparent. Values in-between indicate different levels of transparency. For example, pasting an RGBA image and also using it as the mask would paste the opaque portion of the image but not its transparent background.

The Python Imaging Library also allows you to work with the individual bands of an multi-band image, such as an RGB image. The split method creates a set of new images, each containing one band from the original multi-band image. The merge function takes a mode and a tuple of images, and combines them into a new image. The following sample swaps the three bands of an RGB image:

#### Splitting and merging bands

```python
r, g, b = im.split()
im = Image.merge("RGB", (b, g, r))
```

Note that for a single-band image, [`split()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.split) returns the image itself. To work with individual color bands, you may want to convert the image to “RGB” first.

### Geometrical transforms

The [`PIL.Image.Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) class contains methods to [`resize()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.resize) and [`rotate()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.rotate) an image. The former takes a tuple giving the new size, the latter the angle in degrees counter-clockwise.

#### Simple geometry transforms

```python
out = im.resize((128, 128))
out = im.rotate(45) # degrees counter-clockwise
```

To rotate the image in 90 degree steps, you can either use the [`rotate()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.rotate) method or the [`transpose()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.transpose) method. The latter can also be used to flip an image around its horizontal or vertical axis.

#### Transposing an image

```python
out = im.transpose(Image.FLIP_LEFT_RIGHT)
out = im.transpose(Image.FLIP_TOP_BOTTOM)
out = im.transpose(Image.ROTATE_90)
out = im.transpose(Image.ROTATE_180)
out = im.transpose(Image.ROTATE_270)
```

`transpose(ROTATE)` operations can also be performed identically with [`rotate()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.rotate) operations, provided the `expand` flag is true, to provide for the same changes to the image’s size.

A more general form of image transformations can be carried out via the [`transform()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.transform) method.



### Color transforms

The Python Imaging Library allows you to convert images between different pixel representations using the [`convert()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.convert) method.

#### Converting between modes

```python
from PIL import Image
with Image.open("hopper.ppm") as im:
    im = im.convert("L")
```

The library supports transformations between each supported mode and the “L” and “RGB” modes. To convert between other modes, you may have to use an intermediate image (typically an “RGB” image).

### Image enhancement

The Python Imaging Library provides a number of methods and modules that can be used to enhance images.

#### Filters

The [`ImageFilter`](https://pillow.readthedocs.io/en/stable/reference/ImageFilter.html#module-PIL.ImageFilter) module contains a number of pre-defined enhancement filters that can be used with the [`filter()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.filter) method.

##### Applying filters

```python
from PIL import ImageFilter
out = im.filter(ImageFilter.DETAIL)
```

#### Point Operations

The [`point()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.point) method can be used to translate the pixel values of an image (e.g. image contrast manipulation). In most cases, a function object expecting one argument can be passed to this method. Each pixel is processed according to that function:

##### Applying point transforms

```python
# multiply each pixel by 1.2
out = im.point(lambda i: i * 1.2)
```

Using the above technique, you can quickly apply any simple expression to an image. You can also combine the [`point()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.point) and [`paste()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.paste) methods to selectively modify an image:

##### Processing individual bands

```python
# split the image into individual bands
source = im.split()

R, G, B = 0, 1, 2

# select regions where red is less than 100
mask = source[R].point(lambda i: i < 100 and 255)

# process the green band
out = source[G].point(lambda i: i * 0.7)

# paste the processed band back, but only where red was < 100
source[G].paste(out, None, mask)

# build a new multiband image
im = Image.merge(im.mode, source)
```

Note the syntax used to create the mask:

```
imout = im.point(lambda i: expression and 255)
```

Python only evaluates the portion of a logical expression as is necessary to determine the outcome, and returns the last value examined as the result of the expression. So if the expression above is false (0), Python does not look at the second operand, and thus returns 0. Otherwise, it returns 255.

#### Enhancement

For more advanced image enhancement, you can use the classes in the [`ImageEnhance`](https://pillow.readthedocs.io/en/stable/reference/ImageEnhance.html#module-PIL.ImageEnhance) module. Once created from an image, an enhancement object can be used to quickly try out different settings.

You can adjust contrast, brightness, color balance and sharpness in this way.

##### Enhancing images

```python
from PIL import ImageEnhance

enh = ImageEnhance.Contrast(im)
enh.enhance(1.3).show("30% more contrast")
```

### Image sequences

The Python Imaging Library contains some basic support for image sequences (also called animation formats). Supported sequence formats include FLI/FLC, GIF, and a few experimental formats. TIFF files can also contain more than one frame.

When you open a sequence file, PIL automatically loads the first frame in the sequence. You can use the seek and tell methods to move between different frames:

#### Reading sequences

```python
from PIL import Image

with Image.open("animation.gif") as im:
    im.seek(1) # skip to the second frame

    try:
        while 1:
            im.seek(im.tell()+1)
            # do something to im
    except EOFError:
        pass # end of sequence
```

As seen in this example, you’ll get an [`EOFError`](https://docs.python.org/3/library/exceptions.html#EOFError) exception when the sequence ends.

The following class lets you use the for-statement to loop over the sequence:

#### Using the ImageSequence Iterator class

```python
from PIL import ImageSequence
for frame in ImageSequence.Iterator(im):
    # ...do something to frame...
```

### PostScript printing

The Python Imaging Library includes functions to print images, text and graphics on PostScript printers. Here’s a simple example:

#### Drawing PostScript

```python
from PIL import Image
from PIL import PSDraw

with Image.open("hopper.ppm") as im:
    title = "hopper"
    box = (1*72, 2*72, 7*72, 10*72) # in points

    ps = PSDraw.PSDraw() # default is sys.stdout
    ps.begin_document(title)

    # draw the image (75 dpi)
    ps.image(box, im, 75)
    ps.rectangle(box)

    # draw title
    ps.setfont("HelveticaNarrow-Bold", 36)
    ps.text((3*72, 4*72), title)

    ps.end_document()
```

### More on reading images

As described earlier, the [`open()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.open) function of the [`Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#module-PIL.Image) module is used to open an image file. In most cases, you simply pass it the filename as an argument. `Image.open()` can be used as a context manager:

```python
from PIL import Image
with Image.open("hopper.ppm") as im:
    ...
```

If everything goes well, the result is an [`PIL.Image.Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image) object. Otherwise, an [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError) exception is raised.

You can use a file-like object instead of the filename. The object must implement `file.read`, `file.seek` and `file.tell` methods, and be opened in binary mode.

#### Reading from an open file

```python
from PIL import Image
with open("hopper.ppm", "rb") as fp:
    im = Image.open(fp)
```

To read an image from binary data, use the [`BytesIO`](https://docs.python.org/3/library/io.html#io.BytesIO) class:

#### Reading from binary data

```python
from PIL import Image
import io
im = Image.open(io.BytesIO(buffer))
```

Note that the library rewinds the file (using `seek(0)`) before reading the image header. In addition, seek will also be used when the image data is read (by the load method). If the image file is embedded in a larger file, such as a tar file, you can use the [`ContainerIO`](https://pillow.readthedocs.io/en/stable/PIL.html#module-PIL.ContainerIO) or [`TarIO`](https://pillow.readthedocs.io/en/stable/PIL.html#module-PIL.TarIO) modules to access it.

#### Reading from a tar archive

```python
from PIL import Image, TarIO

fp = TarIO.TarIO("Tests/images/hopper.tar", "hopper.jpg")
im = Image.open(fp)
```

### Controlling the decoder

Some decoders allow you to manipulate the image while reading it from a file. This can often be used to speed up decoding when creating thumbnails (when speed is usually more important than quality) and printing to a monochrome laser printer (when only a greyscale version of the image is needed).

The [`draft()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.draft) method manipulates an opened but not yet loaded image so it as closely as possible matches the given mode and size. This is done by reconfiguring the image decoder.

#### Reading in draft mode

This is only available for JPEG and MPO files.

```python
from PIL import Image

with Image.open(file) as im:
    print("original =", im.mode, im.size)

    im.draft("L", (100, 100))
    print("draft =", im.mode, im.size)
```

This prints something like:

```python
original = RGB (512, 512)
draft = L (128, 128)
```

Note that the resulting image may not exactly match the requested mode and size. To make sure that the image is not larger than the given size, use the thumbnail method instead.

### Bands

An image can consist of one or more bands of data. The Python Imaging Library allows you to store several bands in a single image, provided they all have the same dimensions and depth. For example, a PNG image might have ‘R’, ‘G’, ‘B’, and ‘A’ bands for the red, green, blue, and alpha transparency values. Many operations act on each band separately, e.g., histograms. It is often useful to think of each pixel as having one value per band.

To get the number and names of bands in an image, use the [`getbands()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.getbands) method.

### Modes

The `mode` of an image is a string which defines the type and depth of a pixel in the image. Each pixel uses the full range of the bit depth. So a 1-bit pixel has a range of 0-1, an 8-bit pixel has a range of 0-255 and so on. The current release supports the following standard modes:

> - `1` (1-bit pixels, black and white, stored with one pixel per byte)
> - `L` (8-bit pixels, black and white)
> - `P` (8-bit pixels, mapped to any other mode using a color palette)
> - `RGB` (3x8-bit pixels, true color)
> - `RGBA` (4x8-bit pixels, true color with transparency mask)
> - `CMYK` (4x8-bit pixels, color separation)
> - `YCbCr` (3x8-bit pixels, color video format)
>   - Note that this refers to the JPEG, and not the ITU-R BT.2020, standard
> - `LAB` (3x8-bit pixels, the L*a*b color space)
> - `HSV` (3x8-bit pixels, Hue, Saturation, Value color space)
> - `I` (32-bit signed integer pixels)
> - `F` (32-bit floating point pixels)

Pillow also provides limited support for a few special modes, including:

> - `LA` (L with alpha)
> - `PA` (P with alpha)
> - `RGBX` (true color with padding)
> - `RGBa` (true color with premultiplied alpha)
> - `La` (L with premultiplied alpha)
> - `I;16` (16-bit unsigned integer pixels)
> - `I;16L` (16-bit little endian unsigned integer pixels)
> - `I;16B` (16-bit big endian unsigned integer pixels)
> - `I;16N` (16-bit native endian unsigned integer pixels)
> - `BGR;15` (15-bit reversed true colour)
> - `BGR;16` (16-bit reversed true colour)
> - `BGR;24` (24-bit reversed true colour)
> - `BGR;32` (32-bit reversed true colour)

However, Pillow doesn’t support user-defined modes; if you need to handle band combinations that are not listed above, use a sequence of Image objects.

You can read the mode of an image through the [`mode`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.mode) attribute. This is a string containing one of the above values.

### Size

You can read the image size through the [`size`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.size) attribute. This is a 2-tuple, containing the horizontal and vertical size in pixels.

### Coordinate System

The Python Imaging Library uses a Cartesian pixel coordinate system, with (0,0) in the upper left corner. Note that the coordinates refer to the implied pixel corners; the centre of a pixel addressed as (0, 0) actually lies at (0.5, 0.5).

Coordinates are usually passed to the library as 2-tuples (x, y). Rectangles are represented as 4-tuples, with the upper left corner given first. For example, a rectangle covering all of an 800x600 pixel image is written as (0, 0, 800, 600).

### Palette

The palette mode (`P`) uses a color palette to define the actual color for each pixel.

### Info

You can attach auxiliary information to an image using the [`info`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.info) attribute. This is a dictionary object.

How such information is handled when loading and saving image files is up to the file format handler (see the chapter on [Image file formats](https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html#image-file-formats)). Most handlers add properties to the [`info`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.info) attribute when loading an image, but ignore it when saving images.

### Orientation

A common element of the [`info`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.info) attribute for JPG and TIFF images is the EXIF orientation tag. This is an instruction for how the image data should be oriented. For example, it may instruct an image to be rotated by 90 degrees, or to be mirrored. To apply this information to an image, [`exif_transpose()`](https://pillow.readthedocs.io/en/stable/reference/ImageOps.html#PIL.ImageOps.exif_transpose) can be used.

### Filters

For geometry operations that may map multiple input pixels to a single output pixel, the Python Imaging Library provides different resampling *filters*.

- `PIL.Image.NEAREST`

  Pick one nearest pixel from the input image. Ignore all other input pixels.

- `PIL.Image.BOX`

  Each pixel of source image contributes to one pixel of the destination image with identical weights. For upscaling is equivalent of [`NEAREST`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.NEAREST). This filter can only be used with the [`resize()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.resize) and [`thumbnail()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.thumbnail) methods.*New in version 3.4.0.*

- `PIL.Image.BILINEAR`

  For resize calculate the output pixel value using linear interpolation on all pixels that may contribute to the output value. For other transformations linear interpolation over a 2x2 environment in the input image is used.

- `PIL.Image.HAMMING`

  Produces a sharper image than [`BILINEAR`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.BILINEAR), doesn’t have dislocations on local level like with [`BOX`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.BOX). This filter can only be used with the [`resize()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.resize) and [`thumbnail()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.thumbnail) methods.*New in version 3.4.0.*

- `PIL.Image.BICUBIC`

  For resize calculate the output pixel value using cubic interpolation on all pixels that may contribute to the output value. For other transformations cubic interpolation over a 4x4 environment in the input image is used.

- `PIL.Image.LANCZOS`

  Calculate the output pixel value using a high-quality Lanczos filter (a truncated sinc) on all pixels that may contribute to the output value. This filter can only be used with the [`resize()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.resize) and [`thumbnail()`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image.thumbnail) methods.*New in version 1.1.3.*

#### Filters comparison table

| Filter                                                       | Downscaling quality | Upscaling quality | Performance |
| ------------------------------------------------------------ | ------------------- | ----------------- | ----------- |
| [`NEAREST`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.NEAREST) |                     |                   | ⭐⭐⭐⭐⭐       |
| [`BOX`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.BOX) | ⭐                   |                   | ⭐⭐⭐⭐        |
| [`BILINEAR`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.BILINEAR) | ⭐                   | ⭐                 | ⭐⭐⭐         |
| [`HAMMING`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.HAMMING) | ⭐⭐                  |                   | ⭐⭐⭐         |
| [`BICUBIC`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.BICUBIC) | ⭐⭐⭐                 | ⭐⭐⭐               | ⭐⭐          |
| [`LANCZOS`](https://pillow.readthedocs.io/en/stable/handbook/concepts.html#PIL.Image.LANCZOS) | ⭐⭐⭐⭐                | ⭐⭐⭐⭐              | ⭐           |

## Requests Module Quickstart

Eager to get started? This page gives a good introduction in how to get started with Requests.

First, make sure that:

- Requests is [installed](https://requests.readthedocs.io/en/master/user/install/#install)
- Requests is [up-to-date](https://requests.readthedocs.io/en/master/community/updates/#updates)

Let’s get started with some simple examples.

### Make a Request

Making a request with Requests is very simple.

Begin by importing the Requests module:

```python
>>> import requests
```

Now, let’s try to get a webpage. For this example, let’s get GitHub’s public timeline:

```python
>>> r = requests.get('https://api.github.com/events')
```

Now, we have a [`Response`](https://requests.readthedocs.io/en/master/api/#requests.Response) object called `r`. We can get all the information we need from this object.

Requests’ simple API means that all forms of HTTP request are as obvious. For example, this is how you make an HTTP POST request:

```python
>>> r = requests.post('https://httpbin.org/post', data = {'key':'value'})
```

Nice, right? What about the other HTTP request types: PUT, DELETE, HEAD and OPTIONS? These are all just as simple:

```python
>>> r = requests.put('https://httpbin.org/put', data = {'key':'value'})
>>> r = requests.delete('https://httpbin.org/delete')
>>> r = requests.head('https://httpbin.org/get')
>>> r = requests.options('https://httpbin.org/get')
```

That’s all well and good, but it’s also only the start of what Requests can do.

### Passing Parameters In URLs

You often want to send some sort of data in the URL’s query string. If you were constructing the URL by hand, this data would be given as key/value pairs in the URL after a question mark, e.g. `httpbin.org/get?key=val`. Requests allows you to provide these arguments as a dictionary of strings, using the `params` keyword argument. As an example, if you wanted to pass `key1=value1` and `key2=value2` to `httpbin.org/get`, you would use the following code:

```python
>>> payload = {'key1': 'value1', 'key2': 'value2'}
>>> r = requests.get('https://httpbin.org/get', params=payload)
```

You can see that the URL has been correctly encoded by printing the URL:

```python
>>> print(r.url)
https://httpbin.org/get?key2=value2&key1=value1
```

Note that any dictionary key whose value is `None` will not be added to the URL’s query string.

You can also pass a list of items as a value:

```python
>>> payload = {'key1': 'value1', 'key2': ['value2', 'value3']}

>>> r = requests.get('https://httpbin.org/get', params=payload)
>>> print(r.url)
https://httpbin.org/get?key1=value1&key2=value2&key2=value3
```

### Response Content

We can read the content of the server’s response. Consider the GitHub timeline again:

```python
>>> import requests

>>> r = requests.get('https://api.github.com/events')
>>> r.text
'[{"repository":{"open_issues":0,"url":"https://github.com/...
```

Requests will automatically decode content from the server. Most unicode charsets are seamlessly decoded.

When you make a request, Requests makes educated guesses about the encoding of the response based on the HTTP headers. The text encoding guessed by Requests is used when you access `r.text`. You can find out what encoding Requests is using, and change it, using the `r.encoding` property:

```python
>>> r.encoding
'utf-8'
>>> r.encoding = 'ISO-8859-1'
```

If you change the encoding, Requests will use the new value of `r.encoding` whenever you call `r.text`. You might want to do this in any situation where you can apply special logic to work out what the encoding of the content will be. For example, HTML and XML have the ability to specify their encoding in their body. In situations like this, you should use `r.content` to find the encoding, and then set `r.encoding`. This will let you use `r.text` with the correct encoding.

Requests will also use custom encodings in the event that you need them. If you have created your own encoding and registered it with the `codecs` module, you can simply use the codec name as the value of `r.encoding` and Requests will handle the decoding for you.

### Binary Response Content

You can also access the response body as bytes, for non-text requests:

```python
>>> r.content
b'[{"repository":{"open_issues":0,"url":"https://github.com/...
```

The `gzip` and `deflate` transfer-encodings are automatically decoded for you.

For example, to create an image from binary data returned by a request, you can use the following code:

```python
>>> from PIL import Image
>>> from io import BytesIO

>>> i = Image.open(BytesIO(r.content))
```

### JSON Response Content

There’s also a builtin JSON decoder, in case you’re dealing with JSON data:

```python
>>> import requests

>>> r = requests.get('https://api.github.com/events')
>>> r.json()
[{'repository': {'open_issues': 0, 'url': 'https://github.com/...
```

In case the JSON decoding fails, `r.json()` raises an exception. For example, if the response gets a 204 (No Content), or if the response contains invalid JSON, attempting `r.json()` raises `ValueError: No JSON object could be decoded`.

It should be noted that the success of the call to `r.json()` does **not** indicate the success of the response. Some servers may return a JSON object in a failed response (e.g. error details with HTTP 500). Such JSON will be decoded and returned. To check that a request is successful, use `r.raise_for_status()` or check `r.status_code` is what you expect.

### Raw Response Content

In the rare case that you’d like to get the raw socket response from the server, you can access `r.raw`. If you want to do this, make sure you set `stream=True` in your initial request. Once you do, you can do this:

```python
>>> r = requests.get('https://api.github.com/events', stream=True)

>>> r.raw
<urllib3.response.HTTPResponse object at 0x101194810>

>>> r.raw.read(10)
'\x1f\x8b\x08\x00\x00\x00\x00\x00\x00\x03'
```

In general, however, you should use a pattern like this to save what is being streamed to a file:

```python
with open(filename, 'wb') as fd:
    for chunk in r.iter_content(chunk_size=128):
        fd.write(chunk)
```

Using `Response.iter_content` will handle a lot of what you would otherwise have to handle when using `Response.raw` directly. When streaming a download, the above is the preferred and recommended way to retrieve the content. Note that `chunk_size` can be freely adjusted to a number that may better fit your use cases.

> **Note**
>
> An important note about using `Response.iter_content` versus `Response.raw`. `Response.iter_content` will automatically decode the `gzip` and `deflate` transfer-encodings. `Response.raw` is a raw stream of bytes – it does not transform the response content. If you really need access to the bytes as they were returned, use `Response.raw`.

### Custom Headers

If you’d like to add HTTP headers to a request, simply pass in a `dict` to the `headers` parameter.

For example, we didn’t specify our user-agent in the previous example:

```python
>>> url = 'https://api.github.com/some/endpoint'
>>> headers = {'user-agent': 'my-app/0.0.1'}

>>> r = requests.get(url, headers=headers)
```

Note: Custom headers are given less precedence than more specific sources of information. For instance:

- Authorization headers set with headers= will be overridden if credentials are specified in `.netrc`, which in turn will be overridden by the `auth=` parameter. Requests will search for the netrc file at ~/.netrc, ~/_netrc, or at the path specified by the NETRC environment variable.
- Authorization headers will be removed if you get redirected off-host.
- Proxy-Authorization headers will be overridden by proxy credentials provided in the URL.
- Content-Length headers will be overridden when we can determine the length of the content.

Furthermore, Requests does not change its behavior at all based on which custom headers are specified. The headers are simply passed on into the final request.

> **Note**: 
>
> All header values must be a `string`, bytestring, or unicode. While permitted, it’s advised to avoid passing unicode header values.

### More complicated POST requests

Typically, you want to send some form-encoded data — much like an HTML form. To do this, simply pass a dictionary to the `data` argument. Your dictionary of data will automatically be form-encoded when the request is made:

```python
>>> payload = {'key1': 'value1', 'key2': 'value2'}

>>> r = requests.post("https://httpbin.org/post", data=payload)
>>> print(r.text)
{
  ...
  "form": {
    "key2": "value2",
    "key1": "value1"
  },
  ...
}
```

The `data` argument can also have multiple values for each key. This can be done by making `data` either a list of tuples or a dictionary with lists as values. This is particularly useful when the form has multiple elements that use the same key:

```python
>>> payload_tuples = [('key1', 'value1'), ('key1', 'value2')]
>>> r1 = requests.post('https://httpbin.org/post', data=payload_tuples)
>>> payload_dict = {'key1': ['value1', 'value2']}
>>> r2 = requests.post('https://httpbin.org/post', data=payload_dict)
>>> print(r1.text)
{
  ...
  "form": {
    "key1": [
      "value1",
      "value2"
    ]
  },
  ...
}
>>> r1.text == r2.text
True
```

There are times that you may want to send data that is not form-encoded. If you pass in a `string` instead of a `dict`, that data will be posted directly.

For example, the GitHub API v3 accepts JSON-Encoded POST/PATCH data:

```python
>>> import json

>>> url = 'https://api.github.com/some/endpoint'
>>> payload = {'some': 'data'}

>>> r = requests.post(url, data=json.dumps(payload))
```

Instead of encoding the `dict` yourself, you can also pass it directly using the `json` parameter (added in version 2.4.2) and it will be encoded automatically:

```python
>>> url = 'https://api.github.com/some/endpoint'
>>> payload = {'some': 'data'}

>>> r = requests.post(url, json=payload)
```

Note, the `json` parameter is ignored if either `data` or `files` is passed.

Using the `json` parameter in the request will change the `Content-Type` in the header to `application/json`.

### POST a Multipart-Encoded File

Requests makes it simple to upload Multipart-encoded files:

```python
>>> url = 'https://httpbin.org/post'
>>> files = {'file': open('report.xls', 'rb')}

>>> r = requests.post(url, files=files)
>>> r.text
{
  ...
  "files": {
    "file": "<censored...binary...data>"
  },
  ...
}
```

You can set the filename, content_type and headers explicitly:

```python
>>> url = 'https://httpbin.org/post'
>>> files = {'file': ('report.xls', open('report.xls', 'rb'), 'application/vnd.ms-excel', {'Expires': '0'})}

>>> r = requests.post(url, files=files)
>>> r.text
{
  ...
  "files": {
    "file": "<censored...binary...data>"
  },
  ...
}
```

If you want, you can send strings to be received as files:

```python
>>> url = 'https://httpbin.org/post'
>>> files = {'file': ('report.csv', 'some,data,to,send\nanother,row,to,send\n')}

>>> r = requests.post(url, files=files)
>>> r.text
{
  ...
  "files": {
    "file": "some,data,to,send\\nanother,row,to,send\\n"
  },
  ...
}
```

In the event you are posting a very large file as a `multipart/form-data` request, you may want to stream the request. By default, `requests` does not support this, but there is a separate package which does - `requests-toolbelt`. You should read [the toolbelt’s documentation](https://toolbelt.readthedocs.io/) for more details about how to use it.

For sending multiple files in one request refer to the [advanced](https://requests.readthedocs.io/en/master/user/advanced/#advanced) section.

> **Warning**
>
> It is strongly recommended that you open files in [binary mode](https://docs.python.org/3/tutorial/inputoutput.html#tut-files). This is because Requests may attempt to provide the `Content-Length` header for you, and if it does this value will be set to the number of *bytes* in the file. Errors may occur if you open the file in *text mode*.

### Response Status Codes

We can check the response status code:

```python
>>> r = requests.get('https://httpbin.org/get')
>>> r.status_code
200
```

Requests also comes with a built-in status code lookup object for easy reference:

```python
>>> r.status_code == requests.codes.ok
True
```

If we made a bad request (a 4XX client error or 5XX server error response), we can raise it with [`Response.raise_for_status()`](https://requests.readthedocs.io/en/master/api/#requests.Response.raise_for_status):

```python
>>> bad_r = requests.get('https://httpbin.org/status/404')
>>> bad_r.status_code
404

>>> bad_r.raise_for_status()
Traceback (most recent call last):
  File "requests/models.py", line 832, in raise_for_status
    raise http_error
requests.exceptions.HTTPError: 404 Client Error
```

But, since our `status_code` for `r` was `200`, when we call `raise_for_status()` we get:

```python
>>> r.raise_for_status()
None
```

All is well.

### Response Headers

We can view the server’s response headers using a Python dictionary:

```python
>>> r.headers
{
    'content-encoding': 'gzip',
    'transfer-encoding': 'chunked',
    'connection': 'close',
    'server': 'nginx/1.0.4',
    'x-runtime': '148ms',
    'etag': '"e1ca502697e5c9317743dc078f67693f"',
    'content-type': 'application/json'
}
```

The dictionary is special, though: it’s made just for HTTP headers. According to [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2), HTTP Header names are case-insensitive.

So, we can access the headers using any capitalization we want:

```python
>>> r.headers['Content-Type']
'application/json'

>>> r.headers.get('content-type')
'application/json'
```

It is also special in that the server could have sent the same header multiple times with different values, but requests combines them so they can be represented in the dictionary within a single mapping, as per [RFC 7230](https://tools.ietf.org/html/rfc7230#section-3.2):

> A recipient MAY combine multiple header fields with the same field name into one “field-name: field-value” pair, without changing the semantics of the message, by appending each subsequent field value to the combined field value in order, separated by a comma.

### Cookies

If a response contains some Cookies, you can quickly access them:

```python
>>> url = 'http://example.com/some/cookie/setting/url'
>>> r = requests.get(url)

>>> r.cookies['example_cookie_name']
'example_cookie_value'
```

To send your own cookies to the server, you can use the `cookies` parameter:

```python
>>> url = 'https://httpbin.org/cookies'
>>> cookies = dict(cookies_are='working')

>>> r = requests.get(url, cookies=cookies)
>>> r.text
'{"cookies": {"cookies_are": "working"}}'
```

Cookies are returned in a [`RequestsCookieJar`](https://requests.readthedocs.io/en/master/api/#requests.cookies.RequestsCookieJar), which acts like a `dict` but also offers a more complete interface, suitable for use over multiple domains or paths. Cookie jars can also be passed in to requests:

```python
>>> jar = requests.cookies.RequestsCookieJar()
>>> jar.set('tasty_cookie', 'yum', domain='httpbin.org', path='/cookies')
>>> jar.set('gross_cookie', 'blech', domain='httpbin.org', path='/elsewhere')
>>> url = 'https://httpbin.org/cookies'
>>> r = requests.get(url, cookies=jar)
>>> r.text
'{"cookies": {"tasty_cookie": "yum"}}'
```

### Redirection and History

By default Requests will perform location redirection for all verbs except HEAD.

We can use the `history` property of the Response object to track redirection.

The [`Response.history`](https://requests.readthedocs.io/en/master/api/#requests.Response.history) list contains the [`Response`](https://requests.readthedocs.io/en/master/api/#requests.Response) objects that were created in order to complete the request. The list is sorted from the oldest to the most recent response.

For example, GitHub redirects all HTTP requests to HTTPS:

```python
>>> r = requests.get('http://github.com/')

>>> r.url
'https://github.com/'

>>> r.status_code
200

>>> r.history
[<Response [301]>]
```

If you’re using GET, OPTIONS, POST, PUT, PATCH or DELETE, you can disable redirection handling with the `allow_redirects` parameter:

```python
>>> r = requests.get('http://github.com/', allow_redirects=False)

>>> r.status_code
301

>>> r.history
[]
```

If you’re using HEAD, you can enable redirection as well:

```python
>>> r = requests.head('http://github.com/', allow_redirects=True)

>>> r.url
'https://github.com/'

>>> r.history
[<Response [301]>]
```

### Timeouts

You can tell Requests to stop waiting for a response after a given number of seconds with the `timeout` parameter. Nearly all production code should use this parameter in nearly all requests. Failure to do so can cause your program to hang indefinitely:

```python
>>> requests.get('https://github.com/', timeout=0.001)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
requests.exceptions.Timeout: HTTPConnectionPool(host='github.com', port=80): Request timed out. (timeout=0.001)
```

> **Note**
>
> `timeout` is not a time limit on the entire response download; rather, an exception is raised if the server has not issued a response for `timeout` seconds (more precisely, if no bytes have been received on the underlying socket for `timeout` seconds). If no timeout is specified explicitly, requests do not time out.

### Errors and Exceptions

In the event of a network problem (e.g. DNS failure, refused connection, etc), Requests will raise a `ConnectionError` exception.

[`Response.raise_for_status()`](https://requests.readthedocs.io/en/master/api/#requests.Response.raise_for_status) will raise an `HTTPError` if the HTTP request returned an unsuccessful status code.

If a request times out, a `Timeout` exception is raised.

If a request exceeds the configured number of maximum redirections, a `TooManyRedirects` exception is raised.

All exceptions that Requests explicitly raises inherit from `requests.exceptions.RequestException`.

### Session Objects

The Session object allows you to persist certain parameters across requests. It also persists cookies across all requests made from the Session instance, and will use `urllib3`’s [connection pooling](https://urllib3.readthedocs.io/en/latest/reference/index.html#module-urllib3.connectionpool). So if you’re making several requests to the same host, the underlying TCP connection will be reused, which can result in a significant performance increase (see [HTTP persistent connection](https://en.wikipedia.org/wiki/HTTP_persistent_connection)).

A Session object has all the methods of the main Requests API.

Let’s persist some cookies across requests:

```python
s = requests.Session()

s.get('https://httpbin.org/cookies/set/sessioncookie/123456789')
r = s.get('https://httpbin.org/cookies')

print(r.text)
# '{"cookies": {"sessioncookie": "123456789"}}'
```

Sessions can also be used to provide default data to the request methods. This is done by providing data to the properties on a Session object:

```python
s = requests.Session()
s.auth = ('user', 'pass')
s.headers.update({'x-test': 'true'})

# both 'x-test' and 'x-test2' are sent
s.get('https://httpbin.org/headers', headers={'x-test2': 'true'})
```

Any dictionaries that you pass to a request method will be merged with the session-level values that are set. The method-level parameters override session parameters.

Note, however, that method-level parameters will *not* be persisted across requests, even if using a session. This example will only send the cookies with the first request, but not the second:

```python
s = requests.Session()

r = s.get('https://httpbin.org/cookies', cookies={'from-my': 'browser'})
print(r.text)
# '{"cookies": {"from-my": "browser"}}'

r = s.get('https://httpbin.org/cookies')
print(r.text)
# '{"cookies": {}}'
```

If you want to manually add cookies to your session, use the [Cookie utility functions](https://requests.readthedocs.io/en/master/api/#api-cookies) to manipulate [`Session.cookies`](https://requests.readthedocs.io/en/master/api/#requests.Session.cookies).

Sessions can also be used as context managers:

```python
with requests.Session() as s:
    s.get('https://httpbin.org/cookies/set/sessioncookie/123456789')
```

This will make sure the session is closed as soon as the `with` block is exited, even if unhandled exceptions occurred.

#### Remove a Value From a Dict Parameter

Sometimes you’ll want to omit session-level keys from a dict parameter. To do this, you simply set that key’s value to `None` in the method-level parameter. It will automatically be omitted.

All values that are contained within a session are directly available to you. See the [Session API Docs](https://requests.readthedocs.io/en/master/api/#sessionapi) to learn more.

### Request and Response Objects

Whenever a call is made to `requests.get()` and friends, you are doing two major things. First, you are constructing a `Request` object which will be sent off to a server to request or query some resource. Second, a `Response` object is generated once Requests gets a response back from the server. The `Response` object contains all of the information returned by the server and also contains the `Request` object you created originally. Here is a simple request to get some very important information from Wikipedia’s servers:

```python
>>> r = requests.get('https://en.wikipedia.org/wiki/Monty_Python')
```

If we want to access the headers the server sent back to us, we do this:

```python
>>> r.headers
{'content-length': '56170', 'x-content-type-options': 'nosniff', 'x-cache':
'HIT from cp1006.eqiad.wmnet, MISS from cp1010.eqiad.wmnet', 'content-encoding':
'gzip', 'age': '3080', 'content-language': 'en', 'vary': 'Accept-Encoding,Cookie',
'server': 'Apache', 'last-modified': 'Wed, 13 Jun 2012 01:33:50 GMT',
'connection': 'close', 'cache-control': 'private, s-maxage=0, max-age=0,
must-revalidate', 'date': 'Thu, 14 Jun 2012 12:59:39 GMT', 'content-type':
'text/html; charset=UTF-8', 'x-cache-lookup': 'HIT from cp1006.eqiad.wmnet:3128,
MISS from cp1010.eqiad.wmnet:80'}
```

However, if we want to get the headers we sent the server, we simply access the request, and then the request’s headers:

```python
>>> r.request.headers
{'Accept-Encoding': 'identity, deflate, compress, gzip',
'Accept': '*/*', 'User-Agent': 'python-requests/1.2.0'}
```

### Prepared Requests

Whenever you receive a [`Response`](https://requests.readthedocs.io/en/master/api/#requests.Response) object from an API call or a Session call, the `request` attribute is actually the `PreparedRequest` that was used. In some cases you may wish to do some extra work to the body or headers (or anything else really) before sending a request. The simple recipe for this is the following:

```python
from requests import Request, Session

s = Session()

req = Request('POST', url, data=data, headers=headers)
prepped = req.prepare()

# do something with prepped.body
prepped.body = 'No, I want exactly this as the body.'

# do something with prepped.headers
del prepped.headers['Content-Type']

resp = s.send(prepped,
    stream=stream,
    verify=verify,
    proxies=proxies,
    cert=cert,
    timeout=timeout
)

print(resp.status_code)
```

Since you are not doing anything special with the `Request` object, you prepare it immediately and modify the `PreparedRequest` object. You then send that with the other parameters you would have sent to `requests.*` or `Session.*`.

However, the above code will lose some of the advantages of having a Requests [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session) object. In particular, [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session)-level state such as cookies will not get applied to your request. To get a [`PreparedRequest`](https://requests.readthedocs.io/en/master/api/#requests.PreparedRequest) with that state applied, replace the call to [`Request.prepare()`](https://requests.readthedocs.io/en/master/api/#requests.Request.prepare) with a call to [`Session.prepare_request()`](https://requests.readthedocs.io/en/master/api/#requests.Session.prepare_request), like this:

```python
from requests import Request, Session

s = Session()
req = Request('GET',  url, data=data, headers=headers)

prepped = s.prepare_request(req)

# do something with prepped.body
prepped.body = 'Seriously, send exactly these bytes.'

# do something with prepped.headers
prepped.headers['Keep-Dead'] = 'parrot'

resp = s.send(prepped,
    stream=stream,
    verify=verify,
    proxies=proxies,
    cert=cert,
    timeout=timeout
)

print(resp.status_code)
```

When you are using the prepared request flow, keep in mind that it does not take into account the environment. This can cause problems if you are using environment variables to change the behaviour of requests. For example: Self-signed SSL certificates specified in `REQUESTS_CA_BUNDLE` will not be taken into account. As a result an `SSL: CERTIFICATE_VERIFY_FAILED` is thrown. You can get around this behaviour by explicitly merging the environment settings into your session:

```python
from requests import Request, Session

s = Session()
req = Request('GET', url)

prepped = s.prepare_request(req)

# Merge environment settings into session
settings = s.merge_environment_settings(prepped.url, {}, None, None, None)
resp = s.send(prepped, **settings)

print(resp.status_code)
```

### SSL Cert Verification

Requests verifies SSL certificates for HTTPS requests, just like a web browser. By default, SSL verification is enabled, and Requests will throw a SSLError if it’s unable to verify the certificate:

```python
>>> requests.get('https://requestb.in')
requests.exceptions.SSLError: hostname 'requestb.in' doesn't match either of '*.herokuapp.com', 'herokuapp.com'
```

I don’t have SSL setup on this domain, so it throws an exception. Excellent. GitHub does though:

```python
>>> requests.get('https://github.com')
<Response [200]>
```

You can pass `verify` the path to a CA_BUNDLE file or directory with certificates of trusted CAs:

```python
>>> requests.get('https://github.com', verify='/path/to/certfile')
```

or persistent:

```python
s = requests.Session()
s.verify = '/path/to/certfile'
```

> **Note**
>
> If `verify` is set to a path to a directory, the directory must have been processed using the `c_rehash` utility supplied with OpenSSL.

This list of trusted CAs can also be specified through the `REQUESTS_CA_BUNDLE` environment variable. If `REQUESTS_CA_BUNDLE` is not set, `CURL_CA_BUNDLE` will be used as fallback.

Requests can also ignore verifying the SSL certificate if you set `verify` to False:

```python
>>> requests.get('https://kennethreitz.org', verify=False)
<Response [200]>
```

Note that when `verify` is set to `False`, requests will accept any TLS certificate presented by the server, and will ignore hostname mismatches and/or expired certificates, which will make your application vulnerable to man-in-the-middle (MitM) attacks. Setting verify to `False` may be useful during local development or testing.

By default, `verify` is set to True. Option `verify` only applies to host certs.

### Client Side Certificates

You can also specify a local cert to use as client side certificate, as a single file (containing the private key and the certificate) or as a tuple of both files’ paths:

```python
>>> requests.get('https://kennethreitz.org', cert=('/path/client.cert', '/path/client.key'))
<Response [200]>
```

or persistent:

```python
s = requests.Session()
s.cert = '/path/client.cert'
```

If you specify a wrong path or an invalid cert, you’ll get a SSLError:

```python
>>> requests.get('https://kennethreitz.org', cert='/wrong_path/client.pem')
SSLError: [Errno 336265225] _ssl.c:347: error:140B0009:SSL routines:SSL_CTX_use_PrivateKey_file:PEM lib
```

> **Warning**
>
> The private key to your local certificate *must* be **unencrypted**. Currently, Requests does not support using encrypted keys.

### CA Certificates

Requests uses certificates from the package [certifi](https://certifiio.readthedocs.io/). This allows for users to update their trusted certificates without changing the version of Requests.

Before version 2.16, Requests bundled a set of root CAs that it trusted, sourced from the [Mozilla trust store](https://hg.mozilla.org/mozilla-central/raw-file/tip/security/nss/lib/ckfw/builtins/certdata.txt). The certificates were only updated once for each Requests version. When `certifi` was not installed, this led to extremely out-of-date certificate bundles when using significantly older versions of Requests.

For the sake of security we recommend upgrading certifi frequently!

### Body Content Workflow

By default, when you make a request, the body of the response is downloaded immediately. You can override this behaviour and defer downloading the response body until you access the [`Response.content`](https://requests.readthedocs.io/en/master/api/#requests.Response.content) attribute with the `stream` parameter:

```python
tarball_url = 'https://github.com/psf/requests/tarball/master'
r = requests.get(tarball_url, stream=True)
```

At this point only the response headers have been downloaded and the connection remains open, hence allowing us to make content retrieval conditional:

```python
if int(r.headers['content-length']) < TOO_LONG:
  content = r.content
  ...
```

You can further control the workflow by use of the [`Response.iter_content()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_content) and [`Response.iter_lines()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_lines) methods. Alternatively, you can read the undecoded body from the underlying urllib3 [`urllib3.HTTPResponse`](https://urllib3.readthedocs.io/en/latest/reference/urllib3.response.html#urllib3.response.HTTPResponse) at [`Response.raw`](https://requests.readthedocs.io/en/master/api/#requests.Response.raw).

If you set `stream` to `True` when making a request, Requests cannot release the connection back to the pool unless you consume all the data or call [`Response.close`](https://requests.readthedocs.io/en/master/api/#requests.Response.close). This can lead to inefficiency with connections. If you find yourself partially reading request bodies (or not reading them at all) while using `stream=True`, you should make the request within a `with` statement to ensure it’s always closed:

```python
with requests.get('https://httpbin.org/get', stream=True) as r:
    # Do things with the response here.
```

### Keep-Alive

Excellent news — thanks to urllib3, keep-alive is 100% automatic within a session! Any requests that you make within a session will automatically reuse the appropriate connection!

Note that connections are only released back to the pool for reuse once all body data has been read; be sure to either set `stream` to `False` or read the `content` property of the `Response` object.

### Streaming Uploads

Requests supports streaming uploads, which allow you to send large streams or files without reading them into memory. To stream and upload, simply provide a file-like object for your body:

```python
with open('massive-body', 'rb') as f:
    requests.post('http://some.url/streamed', data=f)
```

> **Warning**
>
> It is strongly recommended that you open files in [binary mode](https://docs.python.org/3/tutorial/inputoutput.html#tut-files). This is because Requests may attempt to provide the `Content-Length` header for you, and if it does this value will be set to the number of *bytes* in the file. Errors may occur if you open the file in *text mode*.

### Chunk-Encoded Requests

Requests also supports Chunked transfer encoding for outgoing and incoming requests. To send a chunk-encoded request, simply provide a generator (or any iterator without a length) for your body:

```python
def gen():
    yield 'hi'
    yield 'there'

requests.post('http://some.url/chunked', data=gen())
```

For chunked encoded responses, it’s best to iterate over the data using [`Response.iter_content()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_content). In an ideal situation you’ll have set `stream=True` on the request, in which case you can iterate chunk-by-chunk by calling `iter_content` with a `chunk_size` parameter of `None`. If you want to set a maximum size of the chunk, you can set a `chunk_size` parameter to any integer.

### POST Multiple Multipart-Encoded Files

You can send multiple files in one request. For example, suppose you want to upload image files to an HTML form with a multiple file field ‘images’:

```python
<input type="file" name="images" multiple="true" required="true"/>
```

To do that, just set files to a list of tuples of `(form_field_name, file_info)`:

```python
>>> url = 'https://httpbin.org/post'
>>> multiple_files = [
...     ('images', ('foo.png', open('foo.png', 'rb'), 'image/png')),
...     ('images', ('bar.png', open('bar.png', 'rb'), 'image/png'))]
>>> r = requests.post(url, files=multiple_files)
>>> r.text
{
  ...
  'files': {'images': 'data:image/png;base64,iVBORw ....'}
  'Content-Type': 'multipart/form-data; boundary=3131623adb2043caaeb5538cc7aa0b3a',
  ...
}
```

> **Warning**
>
> It is strongly recommended that you open files in [binary mode](https://docs.python.org/3/tutorial/inputoutput.html#tut-files). This is because Requests may attempt to provide the `Content-Length` header for you, and if it does this value will be set to the number of *bytes* in the file. Errors may occur if you open the file in *text mode*.

### Event Hooks

Requests has a hook system that you can use to manipulate portions of the request process, or signal event handling.

Available hooks:

- `response`:

  The response generated from a Request.

You can assign a hook function on a per-request basis by passing a `{hook_name: callback_function}` dictionary to the `hooks` request parameter:

```python
hooks={'response': print_url}
```

That `callback_function` will receive a chunk of data as its first argument.

```python
def print_url(r, *args, **kwargs):
    print(r.url)
```

If an error occurs while executing your callback, a warning is given.

If the callback function returns a value, it is assumed that it is to replace the data that was passed in. If the function doesn’t return anything, nothing else is affected.

```python
def record_hook(r, *args, **kwargs):
    r.hook_called = True
    return r
```

Let’s print some request method arguments at runtime:

```python
>>> requests.get('https://httpbin.org/', hooks={'response': print_url})
https://httpbin.org/
<Response [200]>
```

You can add multiple hooks to a single request. Let’s call two hooks at once:

```python
>>> r = requests.get('https://httpbin.org/', hooks={'response': [print_url, record_hook]})
>>> r.hook_called
True
```

You can also add hooks to a `Session` instance. Any hooks you add will then be called on every request made to the session. For example:

```python
>>> s = requests.Session()
>>> s.hooks['response'].append(print_url)
>>> s.get('https://httpbin.org/')
 https://httpbin.org/
 <Response [200]>
```

A `Session` can have multiple hooks, which will be called in the order they are added.

### Custom Authentication

Requests allows you to specify your own authentication mechanism.

Any callable which is passed as the `auth` argument to a request method will have the opportunity to modify the request before it is dispatched.

Authentication implementations are subclasses of [`AuthBase`](https://requests.readthedocs.io/en/master/api/#requests.auth.AuthBase), and are easy to define. Requests provides two common authentication scheme implementations in `requests.auth`: [`HTTPBasicAuth`](https://requests.readthedocs.io/en/master/api/#requests.auth.HTTPBasicAuth) and [`HTTPDigestAuth`](https://requests.readthedocs.io/en/master/api/#requests.auth.HTTPDigestAuth).

Let’s pretend that we have a web service that will only respond if the `X-Pizza` header is set to a password value. Unlikely, but just go with it.

```python
from requests.auth import AuthBase

class PizzaAuth(AuthBase):
    """Attaches HTTP Pizza Authentication to the given Request object."""
    def __init__(self, username):
        # setup any auth-related data here
        self.username = username

    def __call__(self, r):
        # modify and return the request
        r.headers['X-Pizza'] = self.username
        return r
```

Then, we can make a request using our Pizza Auth:

```python
>>> requests.get('http://pizzabin.org/admin', auth=PizzaAuth('kenneth'))
<Response [200]>
```

### Streaming Requests

With [`Response.iter_lines()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_lines) you can easily iterate over streaming APIs such as the [Twitter Streaming API](https://dev.twitter.com/streaming/overview). Simply set `stream` to `True` and iterate over the response with [`iter_lines`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_lines):

```python
import json
import requests

r = requests.get('https://httpbin.org/stream/20', stream=True)

for line in r.iter_lines():

    # filter out keep-alive new lines
    if line:
        decoded_line = line.decode('utf-8')
        print(json.loads(decoded_line))
```

When using decode_unicode=True with [`Response.iter_lines()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_lines) or [`Response.iter_content()`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_content), you’ll want to provide a fallback encoding in the event the server doesn’t provide one:

```python
r = requests.get('https://httpbin.org/stream/20', stream=True)

if r.encoding is None:
    r.encoding = 'utf-8'

for line in r.iter_lines(decode_unicode=True):
    if line:
        print(json.loads(line))
```

> **Warning**
>
> [`iter_lines`](https://requests.readthedocs.io/en/master/api/#requests.Response.iter_lines) is not reentrant safe. Calling this method multiple times causes some of the received data being lost. In case you need to call it from multiple places, use the resulting iterator object instead:

```python
lines = r.iter_lines()
# Save the first line for later or just skip it

first_line = next(lines)

for line in lines:
    print(line)
```

### Proxies

If you need to use a proxy, you can configure individual requests with the `proxies` argument to any request method:

```python
import requests

proxies = {
  'http': 'http://10.10.1.10:3128',
  'https': 'http://10.10.1.10:1080',
}

requests.get('http://example.org', proxies=proxies)
```

Alternatively you can configure it once for an entire [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session):

```python
import requests

proxies = {
  'http': 'http://10.10.1.10:3128',
  'https': 'http://10.10.1.10:1080',
}
session = requests.Session()
session.proxies.update(proxies)

session.get('http://example.org')
```

When the proxies configuration is not overridden in python as shown above, by default Requests relies on the proxy configuration defined by standard environment variables `http_proxy`, `https_proxy`, `no_proxy` and `curl_ca_bundle`. Uppercase variants of these variables are also supported. You can therefore set them to configure Requests (only set the ones relevant to your needs):

```python
$ export HTTP_PROXY="http://10.10.1.10:3128"
$ export HTTPS_PROXY="http://10.10.1.10:1080"

$ python
>>> import requests
>>> requests.get('http://example.org')
```

To use HTTP Basic Auth with your proxy, use the http://user:password@host/ syntax in any of the above configuration entries:

```python
$ export HTTPS_PROXY="http://user:pass@10.10.1.10:1080"

$ python
>>> proxies = {'http': 'http://user:pass@10.10.1.10:3128/'}
```

> **Warning**
>
> Storing sensitive username and password information in an environment variable or a version-controlled file is a security risk and is highly discouraged.

To give a proxy for a specific scheme and host, use the scheme://hostname form for the key. This will match for any request to the given scheme and exact hostname.

```python
proxies = {'http://10.20.1.128': 'http://10.10.1.10:5323'}
```

Note that proxy URLs must include the scheme.

Finally, note that using a proxy for https connections typically requires your local machine to trust the proxy’s root certificate. By default the list of certificates trusted by Requests can be found with:

```python
from requests.utils import DEFAULT_CA_BUNDLE_PATH
print(DEFAULT_CA_BUNDLE_PATH)
```

You override this default certificate bundle by setting the standard `curl_ca_bundle` environment variable to another file path:

```python
$ export curl_ca_bundle="/usr/local/myproxy_info/cacert.pem"
$ export https_proxy="http://10.10.1.10:1080"

$ python
>>> import requests
>>> requests.get('https://example.org')
```

#### SOCKS

*New in version 2.10.0.*

In addition to basic HTTP proxies, Requests also supports proxies using the SOCKS protocol. This is an optional feature that requires that additional third-party libraries be installed before use.

You can get the dependencies for this feature from `pip`:

```python
$ python -m pip install requests[socks]
```

Once you’ve installed those dependencies, using a SOCKS proxy is just as easy as using a HTTP one:

```python
proxies = {
    'http': 'socks5://user:pass@host:port',
    'https': 'socks5://user:pass@host:port'
}
```

Using the scheme `socks5` causes the **DNS resolution to happen on the client**, rather than on the proxy server. This is in line with curl, which uses the scheme to decide whether to do the DNS resolution on the client or proxy. If you want to resolve the domains on the proxy server, use `socks5h` as the scheme.

### Compliance

Requests is intended to be compliant with all relevant specifications and RFCs where that compliance will not cause difficulties for users. This attention to the specification can lead to some behaviour that may seem unusual to those not familiar with the relevant specification.

#### Encodings

When you receive a response, Requests makes a guess at the encoding to use for decoding the response when you access the [`Response.text`](https://requests.readthedocs.io/en/master/api/#requests.Response.text) attribute. Requests will first check for an encoding in the HTTP header, and if none is present, will use [chardet](https://pypi.org/project/chardet/) to attempt to guess the encoding.

The only time Requests will not do this is if no explicit charset is present in the HTTP headers **and** the `Content-Type` header contains `text`. In this situation, [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.7.1) specifies that the default charset must be `ISO-8859-1`. Requests follows the specification in this case. If you require a different encoding, you can manually set the [`Response.encoding`](https://requests.readthedocs.io/en/master/api/#requests.Response.encoding) property, or use the raw [`Response.content`](https://requests.readthedocs.io/en/master/api/#requests.Response.content).

### HTTP Verbs

Requests provides access to almost the full range of HTTP verbs: GET, OPTIONS, HEAD, POST, PUT, PATCH and DELETE. The following provides detailed examples of using these various verbs in Requests, using the GitHub API.

We will begin with the verb most commonly used: GET. HTTP GET is an idempotent method that returns a resource from a given URL. As a result, it is the verb you ought to use when attempting to retrieve data from a web location. An example usage would be attempting to get information about a specific commit from GitHub. Suppose we wanted commit `a050faf` on Requests. We would get it like so:

```python
>>> import requests
>>> r = requests.get('https://api.github.com/repos/psf/requests/git/commits/a050faf084662f3a352dd1a941f2c7c9f886d4ad')
```

We should confirm that GitHub responded correctly. If it has, we want to work out what type of content it is. Do this like so:

```python
>>> if r.status_code == requests.codes.ok:
...     print(r.headers['content-type'])
...
application/json; charset=utf-8
```

So, GitHub returns JSON. That’s great, we can use the [`r.json`](https://requests.readthedocs.io/en/master/api/#requests.Response.json) method to parse it into Python objects.

```python
>>> commit_data = r.json()

>>> print(commit_data.keys())
['committer', 'author', 'url', 'tree', 'sha', 'parents', 'message']

>>> print(commit_data['committer'])
{'date': '2012-05-10T11:10:50-07:00', 'email': 'me@kennethreitz.com', 'name': 'Kenneth Reitz'}

>>> print(commit_data['message'])
makin' history
```

So far, so simple. Well, let’s investigate the GitHub API a little bit. Now, we could look at the documentation, but we might have a little more fun if we use Requests instead. We can take advantage of the Requests OPTIONS verb to see what kinds of HTTP methods are supported on the url we just used.

```python
>>> verbs = requests.options(r.url)
>>> verbs.status_code
500
```

Uh, what? That’s unhelpful! Turns out GitHub, like many API providers, don’t actually implement the OPTIONS method. This is an annoying oversight, but it’s OK, we can just use the boring documentation. If GitHub had correctly implemented OPTIONS, however, they should return the allowed methods in the headers, e.g.

```python
>>> verbs = requests.options('http://a-good-website.com/api/cats')
>>> print(verbs.headers['allow'])
GET,HEAD,POST,OPTIONS
```

Turning to the documentation, we see that the only other method allowed for commits is POST, which creates a new commit. As we’re using the Requests repo, we should probably avoid making ham-handed POSTS to it. Instead, let’s play with the Issues feature of GitHub.

This documentation was added in response to [Issue #482](https://github.com/psf/requests/issues/482). Given that this issue already exists, we will use it as an example. Let’s start by getting it.

```python
>>> r = requests.get('https://api.github.com/repos/psf/requests/issues/482')
>>> r.status_code
200

>>> issue = json.loads(r.text)

>>> print(issue['title'])
Feature any http verb in docs

>>> print(issue['comments'])
3
```

Cool, we have three comments. Let’s take a look at the last of them.

```python
>>> r = requests.get(r.url + '/comments')
>>> r.status_code
200

>>> comments = r.json()

>>> print(comments[0].keys())
['body', 'url', 'created_at', 'updated_at', 'user', 'id']

>>> print(comments[2]['body'])
Probably in the "advanced" section
```

Well, that seems like a silly place. Let’s post a comment telling the poster that he’s silly. Who is the poster, anyway?

```python
>>> print(comments[2]['user']['login'])
kennethreitz
```

OK, so let’s tell this Kenneth guy that we think this example should go in the quickstart guide instead. According to the GitHub API doc, the way to do this is to POST to the thread. Let’s do it.

```python
>>> body = json.dumps({u"body": u"Sounds great! I'll get right on it!"})
>>> url = u"https://api.github.com/repos/psf/requests/issues/482/comments"

>>> r = requests.post(url=url, data=body)
>>> r.status_code
404
```

Huh, that’s weird. We probably need to authenticate. That’ll be a pain, right? Wrong. Requests makes it easy to use many forms of authentication, including the very common Basic Auth.

```python
>>> from requests.auth import HTTPBasicAuth
>>> auth = HTTPBasicAuth('fake@example.com', 'not_a_real_password')

>>> r = requests.post(url=url, data=body, auth=auth)
>>> r.status_code
201

>>> content = r.json()
>>> print(content['body'])
Sounds great! I'll get right on it.
```

Brilliant. Oh, wait, no! I meant to add that it would take me a while, because I had to go feed my cat. If only I could edit this comment! Happily, GitHub allows us to use another HTTP verb, PATCH, to edit this comment. Let’s do that.

```python
>>> print(content[u"id"])
5804413

>>> body = json.dumps({u"body": u"Sounds great! I'll get right on it once I feed my cat."})
>>> url = u"https://api.github.com/repos/psf/requests/issues/comments/5804413"

>>> r = requests.patch(url=url, data=body, auth=auth)
>>> r.status_code
200
```

Excellent. Now, just to torture this Kenneth guy, I’ve decided to let him sweat and not tell him that I’m working on this. That means I want to delete this comment. GitHub lets us delete comments using the incredibly aptly named DELETE method. Let’s get rid of it.

```python
>>> r = requests.delete(url=url, auth=auth)
>>> r.status_code
204
>>> r.headers['status']
'204 No Content'
```

Excellent. All gone. The last thing I want to know is how much of my ratelimit I’ve used. Let’s find out. GitHub sends that information in the headers, so rather than download the whole page I’ll send a HEAD request to get the headers.

```python
>>> r = requests.head(url=url, auth=auth)
>>> print(r.headers)
...
'x-ratelimit-remaining': '4995'
'x-ratelimit-limit': '5000'
...
```

Excellent. Time to write a Python program that abuses the GitHub API in all kinds of exciting ways, 4995 more times.

### Custom Verbs

From time to time you may be working with a server that, for whatever reason, allows use or even requires use of HTTP verbs not covered above. One example of this would be the MKCOL method some WEBDAV servers use. Do not fret, these can still be used with Requests. These make use of the built-in `.request` method. For example:

```python
>>> r = requests.request('MKCOL', url, data=data)
>>> r.status_code
200 # Assuming your call was correct
```

Utilising this, you can make use of any method verb that your server allows.

### Link Headers

Many HTTP APIs feature Link headers. They make APIs more self describing and discoverable.

GitHub uses these for [pagination](https://developer.github.com/v3/#pagination) in their API, for example:

```python
>>> url = 'https://api.github.com/users/kennethreitz/repos?page=1&per_page=10'
>>> r = requests.head(url=url)
>>> r.headers['link']
'<https://api.github.com/users/kennethreitz/repos?page=2&per_page=10>; rel="next", <https://api.github.com/users/kennethreitz/repos?page=6&per_page=10>; rel="last"'
```

Requests will automatically parse these link headers and make them easily consumable:

```python
>>> r.links["next"]
{'url': 'https://api.github.com/users/kennethreitz/repos?page=2&per_page=10', 'rel': 'next'}

>>> r.links["last"]
{'url': 'https://api.github.com/users/kennethreitz/repos?page=7&per_page=10', 'rel': 'last'}
```

### Transport Adapters

As of v1.0.0, Requests has moved to a modular internal design. Part of the reason this was done was to implement Transport Adapters, originally [described here](https://www.kennethreitz.org/essays/the-future-of-python-http). Transport Adapters provide a mechanism to define interaction methods for an HTTP service. In particular, they allow you to apply per-service configuration.

Requests ships with a single Transport Adapter, the [`HTTPAdapter`](https://requests.readthedocs.io/en/master/api/#requests.adapters.HTTPAdapter). This adapter provides the default Requests interaction with HTTP and HTTPS using the powerful [urllib3](https://github.com/shazow/urllib3) library. Whenever a Requests [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session) is initialized, one of these is attached to the [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session) object for HTTP, and one for HTTPS.

Requests enables users to create and use their own Transport Adapters that provide specific functionality. Once created, a Transport Adapter can be mounted to a Session object, along with an indication of which web services it should apply to.

```python
>>> s = requests.Session()
>>> s.mount('https://github.com/', MyAdapter())
```

The mount call registers a specific instance of a Transport Adapter to a prefix. Once mounted, any HTTP request made using that session whose URL starts with the given prefix will use the given Transport Adapter.

Many of the details of implementing a Transport Adapter are beyond the scope of this documentation, but take a look at the next example for a simple SSL use- case. For more than that, you might look at subclassing the [`BaseAdapter`](https://requests.readthedocs.io/en/master/api/#requests.adapters.BaseAdapter).

#### Example: Specific SSL Version

The Requests team has made a specific choice to use whatever SSL version is default in the underlying library ([urllib3](https://github.com/shazow/urllib3)). Normally this is fine, but from time to time, you might find yourself needing to connect to a service-endpoint that uses a version that isn’t compatible with the default.

You can use Transport Adapters for this by taking most of the existing implementation of HTTPAdapter, and adding a parameter *ssl_version* that gets passed-through to urllib3. We’ll make a Transport Adapter that instructs the library to use SSLv3:

```python
import ssl
from urllib3.poolmanager import PoolManager

from requests.adapters import HTTPAdapter


class Ssl3HttpAdapter(HTTPAdapter):
    """"Transport adapter" that allows us to use SSLv3."""

    def init_poolmanager(self, connections, maxsize, block=False):
        self.poolmanager = PoolManager(
            num_pools=connections, maxsize=maxsize,
            block=block, ssl_version=ssl.PROTOCOL_SSLv3)
```

### Blocking Or Non-Blocking?

With the default Transport Adapter in place, Requests does not provide any kind of non-blocking IO. The [`Response.content`](https://requests.readthedocs.io/en/master/api/#requests.Response.content) property will block until the entire response has been downloaded. If you require more granularity, the streaming features of the library (see [Streaming Requests](https://requests.readthedocs.io/en/master/user/advanced/#streaming-requests)) allow you to retrieve smaller quantities of the response at a time. However, these calls will still block.

If you are concerned about the use of blocking IO, there are lots of projects out there that combine Requests with one of Python’s asynchronicity frameworks. Some excellent examples are [requests-threads](https://github.com/requests/requests-threads), [grequests](https://github.com/kennethreitz/grequests), [requests-futures](https://github.com/ross/requests-futures), and [httpx](https://github.com/encode/httpx).

### Header Ordering

In unusual circumstances you may want to provide headers in an ordered manner. If you pass an `OrderedDict` to the `headers` keyword argument, that will provide the headers with an ordering. *However*, the ordering of the default headers used by Requests will be preferred, which means that if you override default headers in the `headers` keyword argument, they may appear out of order compared to other headers in that keyword argument.

If this is problematic, users should consider setting the default headers on a [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session) object, by setting [`Session`](https://requests.readthedocs.io/en/master/api/#requests.Session.headers) to a custom `OrderedDict`. That ordering will always be preferred.

### Timeouts

Most requests to external servers should have a timeout attached, in case the server is not responding in a timely manner. By default, requests do not time out unless a timeout value is set explicitly. Without a timeout, your code may hang for minutes or more.

The **connect** timeout is the number of seconds Requests will wait for your client to establish a connection to a remote machine (corresponding to the [connect()](https://linux.die.net/man/2/connect)) call on the socket. It’s a good practice to set connect timeouts to slightly larger than a multiple of 3, which is the default [TCP packet retransmission window](https://www.hjp.at/doc/rfc/rfc2988.txt).

Once your client has connected to the server and sent the HTTP request, the **read** timeout is the number of seconds the client will wait for the server to send a response. (Specifically, it’s the number of seconds that the client will wait *between* bytes sent from the server. In 99.9% of cases, this is the time before the server sends the first byte).

If you specify a single value for the timeout, like this:

```python
r = requests.get('https://github.com', timeout=5)
```

The timeout value will be applied to both the `connect` and the `read` timeouts. Specify a tuple if you would like to set the values separately:

```python
r = requests.get('https://github.com', timeout=(3.05, 27))
```

If the remote server is very slow, you can tell Requests to wait forever for a response, by passing None as a timeout value and then retrieving a cup of coffee.

```
r = requests.get('https://github.com', timeout=None)
```

## [`email`](https://docs.python.org/3/library/email.html#module-email): Examples

Here are a few examples of how to use the [`email`](https://docs.python.org/3/library/email.html#module-email) package to read, write, and send simple email messages, as well as more complex MIME messages.

First, let’s see how to create and send a simple text message (both the text content and the addresses may contain unicode characters):

```python
# Import smtplib for the actual sending function
import smtplib

# Import the email modules we'll need
from email.message import EmailMessage

# Open the plain text file whose name is in textfile for reading.
with open(textfile) as fp:
    # Create a text/plain message
    msg = EmailMessage()
    msg.set_content(fp.read())

# me == the sender's email address
# you == the recipient's email address
msg['Subject'] = f'The contents of {textfile}'
msg['From'] = me
msg['To'] = you

# Send the message via our own SMTP server.
s = smtplib.SMTP('localhost')
s.send_message(msg)
s.quit()
```

Parsing [**RFC 822**](https://tools.ietf.org/html/rfc822.html) headers can easily be done by the using the classes from the [`parser`](https://docs.python.org/3/library/email.parser.html#module-email.parser) module:

```python
# Import the email modules we'll need
from email.parser import BytesParser, Parser
from email.policy import default

# If the e-mail headers are in a file, uncomment these two lines:
# with open(messagefile, 'rb') as fp:
#     headers = BytesParser(policy=default).parse(fp)

#  Or for parsing headers in a string (this is an uncommon operation), use:
headers = Parser(policy=default).parsestr(
        'From: Foo Bar <user@example.com>\n'
        'To: <someone_else@example.com>\n'
        'Subject: Test message\n'
        '\n'
        'Body would go here\n')

#  Now the header items can be accessed as a dictionary:
print('To: {}'.format(headers['to']))
print('From: {}'.format(headers['from']))
print('Subject: {}'.format(headers['subject']))

# You can also access the parts of the addresses:
print('Recipient username: {}'.format(headers['to'].addresses[0].username))
print('Sender name: {}'.format(headers['from'].addresses[0].display_name))
```

Here’s an example of how to send a MIME message containing a bunch of family pictures that may be residing in a directory:

```python
# Import smtplib for the actual sending function
import smtplib

# And imghdr to find the types of our images
import imghdr

# Here are the email package modules we'll need
from email.message import EmailMessage

# Create the container email message.
msg = EmailMessage()
msg['Subject'] = 'Our family reunion'
# me == the sender's email address
# family = the list of all recipients' email addresses
msg['From'] = me
msg['To'] = ', '.join(family)
msg.preamble = 'You will not see this in a MIME-aware mail reader.\n'

# Open the files in binary mode.  Use imghdr to figure out the
# MIME subtype for each specific image.
for file in pngfiles:
    with open(file, 'rb') as fp:
        img_data = fp.read()
    msg.add_attachment(img_data, maintype='image',
                                 subtype=imghdr.what(None, img_data))

# Send the email via our own SMTP server.
with smtplib.SMTP('localhost') as s:
    s.send_message(msg)
```

Here’s an example of how to send the entire contents of a directory as an email message: [1](https://docs.python.org/3/library/email.examples.html#id3)

```python
#!/usr/bin/env python3

"""Send the contents of a directory as a MIME message."""

import os
import smtplib
# For guessing MIME type based on file name extension
import mimetypes

from argparse import ArgumentParser

from email.message import EmailMessage
from email.policy import SMTP


def main():
    parser = ArgumentParser(description="""\
Send the contents of a directory as a MIME message.
Unless the -o option is given, the email is sent by forwarding to your local
SMTP server, which then does the normal delivery process.  Your local machine
must be running an SMTP server.
""")
    parser.add_argument('-d', '--directory',
                        help="""Mail the contents of the specified directory,
                        otherwise use the current directory.  Only the regular
                        files in the directory are sent, and we don't recurse to
                        subdirectories.""")
    parser.add_argument('-o', '--output',
                        metavar='FILE',
                        help="""Print the composed message to FILE instead of
                        sending the message to the SMTP server.""")
    parser.add_argument('-s', '--sender', required=True,
                        help='The value of the From: header (required)')
    parser.add_argument('-r', '--recipient', required=True,
                        action='append', metavar='RECIPIENT',
                        default=[], dest='recipients',
                        help='A To: header value (at least one required)')
    args = parser.parse_args()
    directory = args.directory
    if not directory:
        directory = '.'
    # Create the message
    msg = EmailMessage()
    msg['Subject'] = f'Contents of directory {os.path.abspath(directory)}'
    msg['To'] = ', '.join(args.recipients)
    msg['From'] = args.sender
    msg.preamble = 'You will not see this in a MIME-aware mail reader.\n'

    for filename in os.listdir(directory):
        path = os.path.join(directory, filename)
        if not os.path.isfile(path):
            continue
        # Guess the content type based on the file's extension.  Encoding
        # will be ignored, although we should check for simple things like
        # gzip'd or compressed files.
        ctype, encoding = mimetypes.guess_type(path)
        if ctype is None or encoding is not None:
            # No guess could be made, or the file is encoded (compressed), so
            # use a generic bag-of-bits type.
            ctype = 'application/octet-stream'
        maintype, subtype = ctype.split('/', 1)
        with open(path, 'rb') as fp:
            msg.add_attachment(fp.read(),
                               maintype=maintype,
                               subtype=subtype,
                               filename=filename)
    # Now send or store the message
    if args.output:
        with open(args.output, 'wb') as fp:
            fp.write(msg.as_bytes(policy=SMTP))
    else:
        with smtplib.SMTP('localhost') as s:
            s.send_message(msg)


if __name__ == '__main__':
    main()
```

Here’s an example of how to unpack a MIME message like the one above, into a directory of files:

```python
#!/usr/bin/env python3

"""Unpack a MIME message into a directory of files."""

import os
import email
import mimetypes

from email.policy import default

from argparse import ArgumentParser


def main():
    parser = ArgumentParser(description="""\
Unpack a MIME message into a directory of files.
""")
    parser.add_argument('-d', '--directory', required=True,
                        help="""Unpack the MIME message into the named
                        directory, which will be created if it doesn't already
                        exist.""")
    parser.add_argument('msgfile')
    args = parser.parse_args()

    with open(args.msgfile, 'rb') as fp:
        msg = email.message_from_binary_file(fp, policy=default)

    try:
        os.mkdir(args.directory)
    except FileExistsError:
        pass

    counter = 1
    for part in msg.walk():
        # multipart/* are just containers
        if part.get_content_maintype() == 'multipart':
            continue
        # Applications should really sanitize the given filename so that an
        # email message can't be used to overwrite important files
        filename = part.get_filename()
        if not filename:
            ext = mimetypes.guess_extension(part.get_content_type())
            if not ext:
                # Use a generic bag-of-bits extension
                ext = '.bin'
            filename = f'part-{counter:03d}{ext}'
        counter += 1
        with open(os.path.join(args.directory, filename), 'wb') as fp:
            fp.write(part.get_payload(decode=True))


if __name__ == '__main__':
    main()
```

Here’s an example of how to create an HTML message with an alternative plain text version. To make things a bit more interesting, we include a related image in the html part, and we save a copy of what we are going to send to disk, as well as sending it.

```python
#!/usr/bin/env python3

import smtplib

from email.message import EmailMessage
from email.headerregistry import Address
from email.utils import make_msgid

# Create the base text message.
msg = EmailMessage()
msg['Subject'] = "Ayons asperges pour le déjeuner"
msg['From'] = Address("Pepé Le Pew", "pepe", "example.com")
msg['To'] = (Address("Penelope Pussycat", "penelope", "example.com"),
             Address("Fabrette Pussycat", "fabrette", "example.com"))
msg.set_content("""\
Salut!

Cela ressemble à un excellent recipie[1] déjeuner.

[1] http://www.yummly.com/recipe/Roasted-Asparagus-Epicurious-203718

--Pepé
""")

# Add the html version.  This converts the message into a multipart/alternative
# container, with the original text message as the first part and the new html
# message as the second part.
asparagus_cid = make_msgid()
msg.add_alternative("""\
<html>
  <head></head>
  <body>
    <p>Salut!</p>
    <p>Cela ressemble à un excellent
        <a href="http://www.yummly.com/recipe/Roasted-Asparagus-Epicurious-203718">
            recipie
        </a> déjeuner.
    </p>
    <img src="cid:{asparagus_cid}" />
  </body>
</html>
""".format(asparagus_cid=asparagus_cid[1:-1]), subtype='html')
# note that we needed to peel the <> off the msgid for use in the html.

# Now add the related image to the html part.
with open("roasted-asparagus.jpg", 'rb') as img:
    msg.get_payload()[1].add_related(img.read(), 'image', 'jpeg',
                                     cid=asparagus_cid)

# Make a local copy of what we are going to send.
with open('outgoing.msg', 'wb') as f:
    f.write(bytes(msg))

# Send the message via local SMTP server.
with smtplib.SMTP('localhost') as s:
    s.send_message(msg)
```

If we were sent the message from the last example, here is one way we could process it:

```python
import os
import sys
import tempfile
import mimetypes
import webbrowser

# Import the email modules we'll need
from email import policy
from email.parser import BytesParser

# An imaginary module that would make this work and be safe.
from imaginary import magic_html_parser

# In a real program you'd get the filename from the arguments.
with open('outgoing.msg', 'rb') as fp:
    msg = BytesParser(policy=policy.default).parse(fp)

# Now the header items can be accessed as a dictionary, and any non-ASCII will
# be converted to unicode:
print('To:', msg['to'])
print('From:', msg['from'])
print('Subject:', msg['subject'])

# If we want to print a preview of the message content, we can extract whatever
# the least formatted payload is and print the first three lines.  Of course,
# if the message has no plain text part printing the first three lines of html
# is probably useless, but this is just a conceptual example.
simplest = msg.get_body(preferencelist=('plain', 'html'))
print()
print(''.join(simplest.get_content().splitlines(keepends=True)[:3]))

ans = input("View full message?")
if ans.lower()[0] == 'n':
    sys.exit()

# We can extract the richest alternative in order to display it:
richest = msg.get_body()
partfiles = {}
if richest['content-type'].maintype == 'text':
    if richest['content-type'].subtype == 'plain':
        for line in richest.get_content().splitlines():
            print(line)
        sys.exit()
    elif richest['content-type'].subtype == 'html':
        body = richest
    else:
        print("Don't know how to display {}".format(richest.get_content_type()))
        sys.exit()
elif richest['content-type'].content_type == 'multipart/related':
    body = richest.get_body(preferencelist=('html'))
    for part in richest.iter_attachments():
        fn = part.get_filename()
        if fn:
            extension = os.path.splitext(part.get_filename())[1]
        else:
            extension = mimetypes.guess_extension(part.get_content_type())
        with tempfile.NamedTemporaryFile(suffix=extension, delete=False) as f:
            f.write(part.get_content())
            # again strip the <> to go from email form of cid to html form.
            partfiles[part['content-id'][1:-1]] = f.name
else:
    print("Don't know how to display {}".format(richest.get_content_type()))
    sys.exit()
with tempfile.NamedTemporaryFile(mode='w', delete=False) as f:
    # The magic_html_parser has to rewrite the href="cid:...." attributes to
    # point to the filenames in partfiles.  It also has to do a safety-sanitize
    # of the html.  It could be written using html.parser.
    f.write(magic_html_parser(body.get_content(), partfiles))
webbrowser.open(f.name)
os.remove(f.name)
for fn in partfiles.values():
    os.remove(fn)

# Of course, there are lots of email messages that could break this simple
# minded program, but it will handle the most common ones.
```

Up to the prompt, the output from the above is:

```python
To: Penelope Pussycat <penelope@example.com>, Fabrette Pussycat <fabrette@example.com>
From: Pepé Le Pew <pepe@example.com>
Subject: Ayons asperges pour le déjeuner

Salut!

Cela ressemble à un excellent recipie[1] déjeuner.
```

## [`smtplib`](https://docs.python.org/3/library/smtplib.html#module-smtplib) — SMTP protocol client

**Source code:** [Lib/smtplib.py](https://github.com/python/cpython/tree/3.9/Lib/smtplib.py)

------

The [`smtplib`](https://docs.python.org/3/library/smtplib.html#module-smtplib) module defines an SMTP client session object that can be used to send mail to any Internet machine with an SMTP or ESMTP listener daemon. For details of SMTP and ESMTP operation, consult [**RFC 821**](https://tools.ietf.org/html/rfc821.html) (Simple Mail Transfer Protocol) and [**RFC 1869**](https://tools.ietf.org/html/rfc1869.html) (SMTP Service Extensions).

- *class* `smtplib.``SMTP`(*host=''*, *port=0*, *local_hostname=None*, [*timeout*, ]*source_address=None*)

  An [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) instance encapsulates an SMTP connection. It has methods that support a full repertoire of SMTP and ESMTP operations. If the optional host and port parameters are given, the SMTP [`connect()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.connect) method is called with those parameters during initialization. If specified, *local_hostname* is used as the FQDN of the local host in the HELO/EHLO command. Otherwise, the local hostname is found using [`socket.getfqdn()`](https://docs.python.org/3/library/socket.html#socket.getfqdn). If the [`connect()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.connect) call returns anything other than a success code, an [`SMTPConnectError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPConnectError) is raised. The optional *timeout* parameter specifies a timeout in seconds for blocking operations like the connection attempt (if not specified, the global default timeout setting will be used). If the timeout expires, [`socket.timeout`](https://docs.python.org/3/library/socket.html#socket.timeout) is raised. The optional source_address parameter allows binding to some specific source address in a machine with multiple network interfaces, and/or to some specific source TCP port. It takes a 2-tuple (host, port), for the socket to bind to as its source address before connecting. If omitted (or if host or port are `''` and/or 0 respectively) the OS default behavior will be used.For normal use, you should only require the initialization/connect, [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail), and [`SMTP.quit()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.quit) methods. An example is included below.The [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) class supports the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) statement. When used like this, the SMTP `QUIT` command is issued automatically when the `with` statement exits. E.g.:>>>`>>> from smtplib import SMTP >>> with SMTP("domain.org") as smtp: ...     smtp.noop() ... (250, b'Ok') >>> `All commands will raise an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `smtplib.SMTP.send` with arguments `self` and `data`, where `data` is the bytes about to be sent to the remote host.*Changed in version 3.3:* Support for the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) statement was added.*Changed in version 3.3:* source_address argument was added.*New in version 3.5:* The SMTPUTF8 extension ([**RFC 6531**](https://tools.ietf.org/html/rfc6531.html)) is now supported.*Changed in version 3.9:* If the *timeout* parameter is set to be zero, it will raise a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) to prevent the creation of a non-blocking socket

- *class* `smtplib.``SMTP_SSL`(*host=''*, *port=0*, *local_hostname=None*, *keyfile=None*, *certfile=None*, [*timeout*, ]*context=None*, *source_address=None*)

  An [`SMTP_SSL`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL) instance behaves exactly the same as instances of [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP). [`SMTP_SSL`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP_SSL) should be used for situations where SSL is required from the beginning of the connection and using `starttls()` is not appropriate. If *host* is not specified, the local host is used. If *port* is zero, the standard SMTP-over-SSL port (465) is used. The optional arguments *local_hostname*, *timeout* and *source_address* have the same meaning as they do in the [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) class. *context*, also optional, can contain a [`SSLContext`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext) and allows configuring various aspects of the secure connection. Please read [Security considerations](https://docs.python.org/3/library/ssl.html#ssl-security) for best practices.*keyfile* and *certfile* are a legacy alternative to *context*, and can point to a PEM formatted private key and certificate chain file for the SSL connection.*Changed in version 3.3:* *context* was added.*Changed in version 3.3:* source_address argument was added.*Changed in version 3.4:* The class now supports hostname check with [`ssl.SSLContext.check_hostname`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext.check_hostname) and *Server Name Indication* (see [`ssl.HAS_SNI`](https://docs.python.org/3/library/ssl.html#ssl.HAS_SNI)).*Deprecated since version 3.6:* *keyfile* and *certfile* are deprecated in favor of *context*. Please use [`ssl.SSLContext.load_cert_chain()`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext.load_cert_chain) instead, or let [`ssl.create_default_context()`](https://docs.python.org/3/library/ssl.html#ssl.create_default_context) select the system’s trusted CA certificates for you.*Changed in version 3.9:* If the *timeout* parameter is set to be zero, it will raise a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) to prevent the creation of a non-blocking socket

- *class* `smtplib.``LMTP`(*host=''*, *port=LMTP_PORT*, *local_hostname=None*, *source_address=None*[, *timeout*])

  The LMTP protocol, which is very similar to ESMTP, is heavily based on the standard SMTP client. It’s common to use Unix sockets for LMTP, so our `connect()` method must support that as well as a regular host:port server. The optional arguments local_hostname and source_address have the same meaning as they do in the [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) class. To specify a Unix socket, you must use an absolute path for *host*, starting with a ‘/’.Authentication is supported, using the regular SMTP mechanism. When using a Unix socket, LMTP generally don’t support or require any authentication, but your mileage might vary.*Changed in version 3.9:* The optional *timeout* parameter was added.

A nice selection of exceptions is defined as well:

- *exception* `smtplib.``SMTPException`

  Subclass of [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError) that is the base exception class for all the other exceptions provided by this module.*Changed in version 3.4:* SMTPException became subclass of [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError)

- *exception* `smtplib.``SMTPServerDisconnected`

  This exception is raised when the server unexpectedly disconnects, or when an attempt is made to use the [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) instance before connecting it to a server.

- *exception* `smtplib.``SMTPResponseException`

  Base class for all exceptions that include an SMTP error code. These exceptions are generated in some instances when the SMTP server returns an error code. The error code is stored in the `smtp_code` attribute of the error, and the `smtp_error` attribute is set to the error message.

- *exception* `smtplib.``SMTPSenderRefused`

  Sender address refused. In addition to the attributes set by on all [`SMTPResponseException`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPResponseException) exceptions, this sets ‘sender’ to the string that the SMTP server refused.

- *exception* `smtplib.``SMTPRecipientsRefused`

  All recipient addresses refused. The errors for each recipient are accessible through the attribute `recipients`, which is a dictionary of exactly the same sort as [`SMTP.sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail) returns.

- *exception* `smtplib.``SMTPDataError`

  The SMTP server refused to accept the message data.

- *exception* `smtplib.``SMTPConnectError`

  Error occurred during establishment of a connection with the server.

- *exception* `smtplib.``SMTPHeloError`

  The server refused our `HELO` message.

- *exception* `smtplib.``SMTPNotSupportedError`

  The command or option attempted is not supported by the server.*New in version 3.5.*

- *exception* `smtplib.``SMTPAuthenticationError`

  SMTP authentication went wrong. Most probably the server didn’t accept the username/password combination provided.

See also

- [**RFC 821**](https://tools.ietf.org/html/rfc821.html) - Simple Mail Transfer Protocol

  Protocol definition for SMTP. This document covers the model, operating procedure, and protocol details for SMTP.

- [**RFC 1869**](https://tools.ietf.org/html/rfc1869.html) - SMTP Service Extensions

  Definition of the ESMTP extensions for SMTP. This describes a framework for extending SMTP with new commands, supporting dynamic discovery of the commands provided by the server, and defines a few additional commands.

### SMTP Objects

An [`SMTP`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP) instance has the following methods:

- `SMTP.``set_debuglevel`(*level*)

  Set the debug output level. A value of 1 or `True` for *level* results in debug messages for connection and for all messages sent to and received from the server. A value of 2 for *level* results in these messages being timestamped.*Changed in version 3.5:* Added debuglevel 2.

- `SMTP.``docmd`(*cmd*, *args=''*)

  Send a command *cmd* to the server. The optional argument *args* is simply concatenated to the command, separated by a space.This returns a 2-tuple composed of a numeric response code and the actual response line (multiline responses are joined into one long line.)In normal operation it should not be necessary to call this method explicitly. It is used to implement other methods and may be useful for testing private extensions.If the connection to the server is lost while waiting for the reply, [`SMTPServerDisconnected`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPServerDisconnected) will be raised.

- `SMTP.``connect`(*host='localhost'*, *port=0*)

  Connect to a host on a given port. The defaults are to connect to the local host at the standard SMTP port (25). If the hostname ends with a colon (`':'`) followed by a number, that suffix will be stripped off and the number interpreted as the port number to use. This method is automatically invoked by the constructor if a host is specified during instantiation. Returns a 2-tuple of the response code and message sent by the server in its connection response.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `smtplib.connect` with arguments `self`, `host`, `port`.

- `SMTP.``helo`(*name=''*)

  Identify yourself to the SMTP server using `HELO`. The hostname argument defaults to the fully qualified domain name of the local host. The message returned by the server is stored as the `helo_resp` attribute of the object.In normal operation it should not be necessary to call this method explicitly. It will be implicitly called by the [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail) when necessary.

- `SMTP.``ehlo`(*name=''*)

  Identify yourself to an ESMTP server using `EHLO`. The hostname argument defaults to the fully qualified domain name of the local host. Examine the response for ESMTP option and store them for use by [`has_extn()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.has_extn). Also sets several informational attributes: the message returned by the server is stored as the `ehlo_resp` attribute, `does_esmtp` is set to true or false depending on whether the server supports ESMTP, and `esmtp_features` will be a dictionary containing the names of the SMTP service extensions this server supports, and their parameters (if any).Unless you wish to use [`has_extn()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.has_extn) before sending mail, it should not be necessary to call this method explicitly. It will be implicitly called by [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail) when necessary.

- `SMTP.``ehlo_or_helo_if_needed`()

  This method calls [`ehlo()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.ehlo) and/or [`helo()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.helo) if there has been no previous `EHLO` or `HELO` command this session. It tries ESMTP `EHLO` first.[`SMTPHeloError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPHeloError)The server didn’t reply properly to the `HELO` greeting.

- `SMTP.``has_extn`(*name*)

  Return [`True`](https://docs.python.org/3/library/constants.html#True) if *name* is in the set of SMTP service extensions returned by the server, [`False`](https://docs.python.org/3/library/constants.html#False) otherwise. Case is ignored.

- `SMTP.``verify`(*address*)

  Check the validity of an address on this server using SMTP `VRFY`. Returns a tuple consisting of code 250 and a full [**RFC 822**](https://tools.ietf.org/html/rfc822.html) address (including human name) if the user address is valid. Otherwise returns an SMTP error code of 400 or greater and an error string.Note Many sites disable SMTP `VRFY` in order to foil spammers.

- `SMTP.``login`(*user*, *password*, ***, *initial_response_ok=True*)

  Log in on an SMTP server that requires authentication. The arguments are the username and the password to authenticate with. If there has been no previous `EHLO` or `HELO` command this session, this method tries ESMTP `EHLO` first. This method will return normally if the authentication was successful, or may raise the following exceptions:[`SMTPHeloError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPHeloError)The server didn’t reply properly to the `HELO` greeting.[`SMTPAuthenticationError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPAuthenticationError)The server didn’t accept the username/password combination.[`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError)The `AUTH` command is not supported by the server.[`SMTPException`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPException)No suitable authentication method was found.Each of the authentication methods supported by [`smtplib`](https://docs.python.org/3/library/smtplib.html#module-smtplib) are tried in turn if they are advertised as supported by the server. See [`auth()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.auth) for a list of supported authentication methods. *initial_response_ok* is passed through to [`auth()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.auth).Optional keyword argument *initial_response_ok* specifies whether, for authentication methods that support it, an “initial response” as specified in [**RFC 4954**](https://tools.ietf.org/html/rfc4954.html) can be sent along with the `AUTH` command, rather than requiring a challenge/response.*Changed in version 3.5:* [`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError) may be raised, and the *initial_response_ok* parameter was added.

- `SMTP.``auth`(*mechanism*, *authobject*, ***, *initial_response_ok=True*)

  Issue an `SMTP` `AUTH` command for the specified authentication *mechanism*, and handle the challenge response via *authobject*.*mechanism* specifies which authentication mechanism is to be used as argument to the `AUTH` command; the valid values are those listed in the `auth` element of `esmtp_features`.*authobject* must be a callable object taking an optional single argument:data = authobject(challenge=None)If optional keyword argument *initial_response_ok* is true, `authobject()` will be called first with no argument. It can return the [**RFC 4954**](https://tools.ietf.org/html/rfc4954.html) “initial response” ASCII `str` which will be encoded and sent with the `AUTH` command as below. If the `authobject()` does not support an initial response (e.g. because it requires a challenge), it should return `None` when called with `challenge=None`. If *initial_response_ok* is false, then `authobject()` will not be called first with `None`.If the initial response check returns `None`, or if *initial_response_ok* is false, `authobject()` will be called to process the server’s challenge response; the *challenge* argument it is passed will be a `bytes`. It should return ASCII `str` *data* that will be base64 encoded and sent to the server.The `SMTP` class provides `authobjects` for the `CRAM-MD5`, `PLAIN`, and `LOGIN` mechanisms; they are named `SMTP.auth_cram_md5`, `SMTP.auth_plain`, and `SMTP.auth_login` respectively. They all require that the `user` and `password` properties of the `SMTP` instance are set to appropriate values.User code does not normally need to call `auth` directly, but can instead call the [`login()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.login) method, which will try each of the above mechanisms in turn, in the order listed. `auth` is exposed to facilitate the implementation of authentication methods not (or not yet) supported directly by [`smtplib`](https://docs.python.org/3/library/smtplib.html#module-smtplib).*New in version 3.5.*

- `SMTP.``starttls`(*keyfile=None*, *certfile=None*, *context=None*)

  Put the SMTP connection in TLS (Transport Layer Security) mode. All SMTP commands that follow will be encrypted. You should then call [`ehlo()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.ehlo) again.If *keyfile* and *certfile* are provided, they are used to create an [`ssl.SSLContext`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext).Optional *context* parameter is an [`ssl.SSLContext`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext) object; This is an alternative to using a keyfile and a certfile and if specified both *keyfile* and *certfile* should be `None`.If there has been no previous `EHLO` or `HELO` command this session, this method tries ESMTP `EHLO` first.*Deprecated since version 3.6:* *keyfile* and *certfile* are deprecated in favor of *context*. Please use [`ssl.SSLContext.load_cert_chain()`](https://docs.python.org/3/library/ssl.html#ssl.SSLContext.load_cert_chain) instead, or let [`ssl.create_default_context()`](https://docs.python.org/3/library/ssl.html#ssl.create_default_context) select the system’s trusted CA certificates for you.[`SMTPHeloError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPHeloError)The server didn’t reply properly to the `HELO` greeting.[`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError)The server does not support the STARTTLS extension.[`RuntimeError`](https://docs.python.org/3/library/exceptions.html#RuntimeError)SSL/TLS support is not available to your Python interpreter.*Changed in version 3.3:* *context* was added.*Changed in version 3.4:* The method now supports hostname check with `SSLContext.check_hostname` and *Server Name Indicator* (see [`HAS_SNI`](https://docs.python.org/3/library/ssl.html#ssl.HAS_SNI)).*Changed in version 3.5:* The error raised for lack of STARTTLS support is now the [`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError) subclass instead of the base [`SMTPException`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPException).

- `SMTP.``sendmail`(*from_addr*, *to_addrs*, *msg*, *mail_options=()*, *rcpt_options=()*)

  Send mail. The required arguments are an [**RFC 822**](https://tools.ietf.org/html/rfc822.html) from-address string, a list of [**RFC 822**](https://tools.ietf.org/html/rfc822.html) to-address strings (a bare string will be treated as a list with 1 address), and a message string. The caller may pass a list of ESMTP options (such as `8bitmime`) to be used in `MAIL FROM` commands as *mail_options*. ESMTP options (such as `DSN` commands) that should be used with all `RCPT` commands can be passed as *rcpt_options*. (If you need to use different ESMTP options to different recipients you have to use the low-level methods such as `mail()`, `rcpt()` and `data()` to send the message.)Note The *from_addr* and *to_addrs* parameters are used to construct the message envelope used by the transport agents. `sendmail` does not modify the message headers in any way.*msg* may be a string containing characters in the ASCII range, or a byte string. A string is encoded to bytes using the ascii codec, and lone `\r` and `\n` characters are converted to `\r\n` characters. A byte string is not modified.If there has been no previous `EHLO` or `HELO` command this session, this method tries ESMTP `EHLO` first. If the server does ESMTP, message size and each of the specified options will be passed to it (if the option is in the feature set the server advertises). If `EHLO` fails, `HELO` will be tried and ESMTP options suppressed.This method will return normally if the mail is accepted for at least one recipient. Otherwise it will raise an exception. That is, if this method does not raise an exception, then someone should get your mail. If this method does not raise an exception, it returns a dictionary, with one entry for each recipient that was refused. Each entry contains a tuple of the SMTP error code and the accompanying error message sent by the server.If `SMTPUTF8` is included in *mail_options*, and the server supports it, *from_addr* and *to_addrs* may contain non-ASCII characters.This method may raise the following exceptions:[`SMTPRecipientsRefused`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPRecipientsRefused)All recipients were refused. Nobody got the mail. The `recipients` attribute of the exception object is a dictionary with information about the refused recipients (like the one returned when at least one recipient was accepted).[`SMTPHeloError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPHeloError)The server didn’t reply properly to the `HELO` greeting.[`SMTPSenderRefused`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPSenderRefused)The server didn’t accept the *from_addr*.[`SMTPDataError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPDataError)The server replied with an unexpected error code (other than a refusal of a recipient).[`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError)`SMTPUTF8` was given in the *mail_options* but is not supported by the server.Unless otherwise noted, the connection will be open even after an exception is raised.*Changed in version 3.2:* *msg* may be a byte string.*Changed in version 3.5:* `SMTPUTF8` support added, and [`SMTPNotSupportedError`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTPNotSupportedError) may be raised if `SMTPUTF8` is specified but the server does not support it.

- `SMTP.``send_message`(*msg*, *from_addr=None*, *to_addrs=None*, *mail_options=()*, *rcpt_options=()*)

  This is a convenience method for calling [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail) with the message represented by an [`email.message.Message`](https://docs.python.org/3/library/email.compat32-message.html#email.message.Message) object. The arguments have the same meaning as for [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail), except that *msg* is a `Message` object.If *from_addr* is `None` or *to_addrs* is `None`, `send_message` fills those arguments with addresses extracted from the headers of *msg* as specified in [**RFC 5322**](https://tools.ietf.org/html/rfc5322.html): *from_addr* is set to the *Sender* field if it is present, and otherwise to the *From* field. *to_addrs* combines the values (if any) of the *To*, *Cc*, and *Bcc* fields from *msg*. If exactly one set of *Resent-** headers appear in the message, the regular headers are ignored and the *Resent-** headers are used instead. If the message contains more than one set of *Resent-** headers, a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) is raised, since there is no way to unambiguously detect the most recent set of *Resent-* headers.`send_message` serializes *msg* using [`BytesGenerator`](https://docs.python.org/3/library/email.generator.html#email.generator.BytesGenerator) with `\r\n` as the *linesep*, and calls [`sendmail()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.sendmail) to transmit the resulting message. Regardless of the values of *from_addr* and *to_addrs*, `send_message` does not transmit any *Bcc* or *Resent-Bcc* headers that may appear in *msg*. If any of the addresses in *from_addr* and *to_addrs* contain non-ASCII characters and the server does not advertise `SMTPUTF8` support, an `SMTPNotSupported` error is raised. Otherwise the `Message` is serialized with a clone of its [`policy`](https://docs.python.org/3/library/email.policy.html#module-email.policy) with the [`utf8`](https://docs.python.org/3/library/email.policy.html#email.policy.EmailPolicy.utf8) attribute set to `True`, and `SMTPUTF8` and `BODY=8BITMIME` are added to *mail_options*.*New in version 3.2.**New in version 3.5:* Support for internationalized addresses (`SMTPUTF8`).

- `SMTP.``quit`()

  Terminate the SMTP session and close the connection. Return the result of the SMTP `QUIT` command.

Low-level methods corresponding to the standard SMTP/ESMTP commands `HELP`, `RSET`, `NOOP`, `MAIL`, `RCPT`, and `DATA` are also supported. Normally these do not need to be called directly, so they are not documented here. For details, consult the module code.

### SMTP Example

This example prompts the user for addresses needed in the message envelope (‘To’ and ‘From’ addresses), and the message to be delivered. Note that the headers to be included with the message must be included in the message as entered; this example doesn’t do any processing of the [**RFC 822**](https://tools.ietf.org/html/rfc822.html) headers. In particular, the ‘To’ and ‘From’ addresses must be included in the message headers explicitly.

```python
import smtplib

def prompt(prompt):
    return input(prompt).strip()

fromaddr = prompt("From: ")
toaddrs  = prompt("To: ").split()
print("Enter message, end with ^D (Unix) or ^Z (Windows):")

# Add the From: and To: headers at the start!
msg = ("From: %s\r\nTo: %s\r\n\r\n"
       % (fromaddr, ", ".join(toaddrs)))
while True:
    try:
        line = input()
    except EOFError:
        break
    if not line:
        break
    msg = msg + line

print("Message length is", len(msg))

server = smtplib.SMTP('localhost')
server.set_debuglevel(1)
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

> **Note**
>
> In general, you will want to use the [`email`](https://docs.python.org/3/library/email.html#module-email) package’s features to construct an email message, which you can then send via [`send_message()`](https://docs.python.org/3/library/smtplib.html#smtplib.SMTP.send_message); see [email: Examples](https://docs.python.org/3/library/email.examples.html#email-examples).

## [`shutil`](https://docs.python.org/3/library/shutil.html#module-shutil) — High-level file operations

**Source code:** [Lib/shutil.py](https://github.com/python/cpython/tree/3.9/Lib/shutil.py)

------

The [`shutil`](https://docs.python.org/3/library/shutil.html#module-shutil) module offers a number of high-level operations on files and collections of files. In particular, functions are provided which support file copying and removal. For operations on individual files, see also the [`os`](https://docs.python.org/3/library/os.html#module-os) module.

> **Warning**
>
> Even the higher-level file copying functions ([`shutil.copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy), [`shutil.copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2)) cannot copy all file metadata.

On POSIX platforms, this means that file owner and group are lost as well as ACLs. On Mac OS, the resource fork and other metadata are not used. This means that resources will be lost and file type and creator codes will not be correct. On Windows, file owners, ACLs and alternate data streams are not copied.

### Directory and files operations

- `shutil.``copyfileobj`(*fsrc*, *fdst*[, *length*])

  Copy the contents of the file-like object *fsrc* to the file-like object *fdst*. The integer *length*, if given, is the buffer size. In particular, a negative *length* value means to copy the data without looping over the source data in chunks; by default the data is read in chunks to avoid uncontrolled memory consumption. Note that if the current file position of the *fsrc* object is not 0, only the contents from the current file position to the end of the file will be copied.

- `shutil.``copyfile`(*src*, *dst*, ***, *follow_symlinks=True*)

  Copy the contents (no metadata) of the file named *src* to a file named *dst* and return *dst* in the most efficient way possible. *src* and *dst* are path-like objects or path names given as strings.*dst* must be the complete target file name; look at [`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy) for a copy that accepts a target directory path. If *src* and *dst* specify the same file, [`SameFileError`](https://docs.python.org/3/library/shutil.html#shutil.SameFileError) is raised.The destination location must be writable; otherwise, an [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError) exception will be raised. If *dst* already exists, it will be replaced. Special files such as character or block devices and pipes cannot be copied with this function.If *follow_symlinks* is false and *src* is a symbolic link, a new symbolic link will be created instead of copying the file *src* points to.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copyfile` with arguments `src`, `dst`.*Changed in version 3.3:* [`IOError`](https://docs.python.org/3/library/exceptions.html#IOError) used to be raised instead of [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError). Added *follow_symlinks* argument. Now returns *dst*.*Changed in version 3.4:* Raise [`SameFileError`](https://docs.python.org/3/library/shutil.html#shutil.SameFileError) instead of [`Error`](https://docs.python.org/3/library/shutil.html#shutil.Error). Since the former is a subclass of the latter, this change is backward compatible.*Changed in version 3.8:* Platform-specific fast-copy syscalls may be used internally in order to copy the file more efficiently. See [Platform-dependent efficient copy operations](https://docs.python.org/3/library/shutil.html#shutil-platform-dependent-efficient-copy-operations) section.

- *exception* `shutil.``SameFileError`

  This exception is raised if source and destination in [`copyfile()`](https://docs.python.org/3/library/shutil.html#shutil.copyfile) are the same file.*New in version 3.4.*

- `shutil.``copymode`(*src*, *dst*, ***, *follow_symlinks=True*)

  Copy the permission bits from *src* to *dst*. The file contents, owner, and group are unaffected. *src* and *dst* are path-like objects or path names given as strings. If *follow_symlinks* is false, and both *src* and *dst* are symbolic links, [`copymode()`](https://docs.python.org/3/library/shutil.html#shutil.copymode) will attempt to modify the mode of *dst* itself (rather than the file it points to). This functionality is not available on every platform; please see [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) for more information. If [`copymode()`](https://docs.python.org/3/library/shutil.html#shutil.copymode) cannot modify symbolic links on the local platform, and it is asked to do so, it will do nothing and return.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copymode` with arguments `src`, `dst`.*Changed in version 3.3:* Added *follow_symlinks* argument.

- `shutil.``copystat`(*src*, *dst*, ***, *follow_symlinks=True*)

  Copy the permission bits, last access time, last modification time, and flags from *src* to *dst*. On Linux, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) also copies the “extended attributes” where possible. The file contents, owner, and group are unaffected. *src* and *dst* are path-like objects or path names given as strings.If *follow_symlinks* is false, and *src* and *dst* both refer to symbolic links, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) will operate on the symbolic links themselves rather than the files the symbolic links refer to—reading the information from the *src* symbolic link, and writing the information to the *dst* symbolic link.Note Not all platforms provide the ability to examine and modify symbolic links. Python itself can tell you what functionality is locally available.If `os.chmod in os.supports_follow_symlinks` is `True`, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) can modify the permission bits of a symbolic link.If `os.utime in os.supports_follow_symlinks` is `True`, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) can modify the last access and modification times of a symbolic link.If `os.chflags in os.supports_follow_symlinks` is `True`, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) can modify the flags of a symbolic link. (`os.chflags` is not available on all platforms.)On platforms where some or all of this functionality is unavailable, when asked to modify a symbolic link, [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) will copy everything it can. [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) never returns failure.Please see [`os.supports_follow_symlinks`](https://docs.python.org/3/library/os.html#os.supports_follow_symlinks) for more information.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copystat` with arguments `src`, `dst`.*Changed in version 3.3:* Added *follow_symlinks* argument and support for Linux extended attributes.

- `shutil.``copy`(*src*, *dst*, ***, *follow_symlinks=True*)

  Copies the file *src* to the file or directory *dst*. *src* and *dst* should be [path-like objects](https://docs.python.org/3/glossary.html#term-path-like-object) or strings. If *dst* specifies a directory, the file will be copied into *dst* using the base filename from *src*. Returns the path to the newly created file.If *follow_symlinks* is false, and *src* is a symbolic link, *dst* will be created as a symbolic link. If *follow_symlinks* is true and *src* is a symbolic link, *dst* will be a copy of the file *src* refers to.[`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy) copies the file data and the file’s permission mode (see [`os.chmod()`](https://docs.python.org/3/library/os.html#os.chmod)). Other metadata, like the file’s creation and modification times, is not preserved. To preserve all file metadata from the original, use [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) instead.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copyfile` with arguments `src`, `dst`.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copymode` with arguments `src`, `dst`.*Changed in version 3.3:* Added *follow_symlinks* argument. Now returns path to the newly created file.*Changed in version 3.8:* Platform-specific fast-copy syscalls may be used internally in order to copy the file more efficiently. See [Platform-dependent efficient copy operations](https://docs.python.org/3/library/shutil.html#shutil-platform-dependent-efficient-copy-operations) section.

- `shutil.``copy2`(*src*, *dst*, ***, *follow_symlinks=True*)

  Identical to [`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy) except that [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) also attempts to preserve file metadata.When *follow_symlinks* is false, and *src* is a symbolic link, [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) attempts to copy all metadata from the *src* symbolic link to the newly-created *dst* symbolic link. However, this functionality is not available on all platforms. On platforms where some or all of this functionality is unavailable, [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) will preserve all the metadata it can; [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) never raises an exception because it cannot preserve file metadata.[`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) uses [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) to copy the file metadata. Please see [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat) for more information about platform support for modifying symbolic link metadata.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copyfile` with arguments `src`, `dst`.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copystat` with arguments `src`, `dst`.*Changed in version 3.3:* Added *follow_symlinks* argument, try to copy extended file system attributes too (currently Linux only). Now returns path to the newly created file.*Changed in version 3.8:* Platform-specific fast-copy syscalls may be used internally in order to copy the file more efficiently. See [Platform-dependent efficient copy operations](https://docs.python.org/3/library/shutil.html#shutil-platform-dependent-efficient-copy-operations) section.

- `shutil.``ignore_patterns`(**patterns*)

  This factory function creates a function that can be used as a callable for [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree)’s *ignore* argument, ignoring files and directories that match one of the glob-style *patterns* provided. See the example below.

- `shutil.``copytree`(*src*, *dst*, *symlinks=False*, *ignore=None*, *copy_function=copy2*, *ignore_dangling_symlinks=False*, *dirs_exist_ok=False*)

  Recursively copy an entire directory tree rooted at *src* to a directory named *dst* and return the destination directory. *dirs_exist_ok* dictates whether to raise an exception in case *dst* or any missing parent directory already exists.Permissions and times of directories are copied with [`copystat()`](https://docs.python.org/3/library/shutil.html#shutil.copystat), individual files are copied using [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2).If *symlinks* is true, symbolic links in the source tree are represented as symbolic links in the new tree and the metadata of the original links will be copied as far as the platform allows; if false or omitted, the contents and metadata of the linked files are copied to the new tree.When *symlinks* is false, if the file pointed by the symlink doesn’t exist, an exception will be added in the list of errors raised in an [`Error`](https://docs.python.org/3/library/shutil.html#shutil.Error) exception at the end of the copy process. You can set the optional *ignore_dangling_symlinks* flag to true if you want to silence this exception. Notice that this option has no effect on platforms that don’t support [`os.symlink()`](https://docs.python.org/3/library/os.html#os.symlink).If *ignore* is given, it must be a callable that will receive as its arguments the directory being visited by [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree), and a list of its contents, as returned by [`os.listdir()`](https://docs.python.org/3/library/os.html#os.listdir). Since [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree) is called recursively, the *ignore* callable will be called once for each directory that is copied. The callable must return a sequence of directory and file names relative to the current directory (i.e. a subset of the items in its second argument); these names will then be ignored in the copy process. [`ignore_patterns()`](https://docs.python.org/3/library/shutil.html#shutil.ignore_patterns) can be used to create such a callable that ignores names based on glob-style patterns.If exception(s) occur, an [`Error`](https://docs.python.org/3/library/shutil.html#shutil.Error) is raised with a list of reasons.If *copy_function* is given, it must be a callable that will be used to copy each file. It will be called with the source path and the destination path as arguments. By default, [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2) is used, but any function that supports the same signature (like [`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy)) can be used.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.copytree` with arguments `src`, `dst`.*Changed in version 3.3:* Copy metadata when *symlinks* is false. Now returns *dst*.*Changed in version 3.2:* Added the *copy_function* argument to be able to provide a custom copy function. Added the *ignore_dangling_symlinks* argument to silent dangling symlinks errors when *symlinks* is false.*Changed in version 3.8:* Platform-specific fast-copy syscalls may be used internally in order to copy the file more efficiently. See [Platform-dependent efficient copy operations](https://docs.python.org/3/library/shutil.html#shutil-platform-dependent-efficient-copy-operations) section.*New in version 3.8:* The *dirs_exist_ok* parameter.

- `shutil.``rmtree`(*path*, *ignore_errors=False*, *onerror=None*)

  Delete an entire directory tree; *path* must point to a directory (but not a symbolic link to a directory). If *ignore_errors* is true, errors resulting from failed removals will be ignored; if false or omitted, such errors are handled by calling a handler specified by *onerror* or, if that is omitted, they raise an exception.Note On platforms that support the necessary fd-based functions a symlink attack resistant version of [`rmtree()`](https://docs.python.org/3/library/shutil.html#shutil.rmtree) is used by default. On other platforms, the [`rmtree()`](https://docs.python.org/3/library/shutil.html#shutil.rmtree) implementation is susceptible to a symlink attack: given proper timing and circumstances, attackers can manipulate symlinks on the filesystem to delete files they wouldn’t be able to access otherwise. Applications can use the [`rmtree.avoids_symlink_attacks`](https://docs.python.org/3/library/shutil.html#shutil.rmtree.avoids_symlink_attacks) function attribute to determine which case applies.If *onerror* is provided, it must be a callable that accepts three parameters: *function*, *path*, and *excinfo*.The first parameter, *function*, is the function which raised the exception; it depends on the platform and implementation. The second parameter, *path*, will be the path name passed to *function*. The third parameter, *excinfo*, will be the exception information returned by [`sys.exc_info()`](https://docs.python.org/3/library/sys.html#sys.exc_info). Exceptions raised by *onerror* will not be caught.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.rmtree` with argument `path`.*Changed in version 3.3:* Added a symlink attack resistant version that is used automatically if platform supports fd-based functions.*Changed in version 3.8:* On Windows, will no longer delete the contents of a directory junction before removing the junction.`rmtree.``avoids_symlink_attacks`Indicates whether the current platform and implementation provides a symlink attack resistant version of [`rmtree()`](https://docs.python.org/3/library/shutil.html#shutil.rmtree). Currently this is only true for platforms supporting fd-based directory access functions.*New in version 3.3.*

- `shutil.``move`(*src*, *dst*, *copy_function=copy2*)

  Recursively move a file or directory (*src*) to another location (*dst*) and return the destination.If the destination is an existing directory, then *src* is moved inside that directory. If the destination already exists but is not a directory, it may be overwritten depending on [`os.rename()`](https://docs.python.org/3/library/os.html#os.rename) semantics.If the destination is on the current filesystem, then [`os.rename()`](https://docs.python.org/3/library/os.html#os.rename) is used. Otherwise, *src* is copied to *dst* using *copy_function* and then removed. In case of symlinks, a new symlink pointing to the target of *src* will be created in or as *dst* and *src* will be removed.If *copy_function* is given, it must be a callable that takes two arguments *src* and *dst*, and will be used to copy *src* to *dst* if [`os.rename()`](https://docs.python.org/3/library/os.html#os.rename) cannot be used. If the source is a directory, [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree) is called, passing it the `copy_function()`. The default *copy_function* is [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2). Using [`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy) as the *copy_function* allows the move to succeed when it is not possible to also copy the metadata, at the expense of not copying any of the metadata.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.move` with arguments `src`, `dst`.*Changed in version 3.3:* Added explicit symlink handling for foreign filesystems, thus adapting it to the behavior of GNU’s **mv**. Now returns *dst*.*Changed in version 3.5:* Added the *copy_function* keyword argument.*Changed in version 3.8:* Platform-specific fast-copy syscalls may be used internally in order to copy the file more efficiently. See [Platform-dependent efficient copy operations](https://docs.python.org/3/library/shutil.html#shutil-platform-dependent-efficient-copy-operations) section.*Changed in version 3.9:* Accepts a [path-like object](https://docs.python.org/3/glossary.html#term-path-like-object) for both *src* and *dst*.

- `shutil.``disk_usage`(*path*)

  Return disk usage statistics about the given path as a [named tuple](https://docs.python.org/3/glossary.html#term-named-tuple) with the attributes *total*, *used* and *free*, which are the amount of total, used and free space, in bytes. *path* may be a file or a directory.*New in version 3.3.**Changed in version 3.8:* On Windows, *path* can now be a file or directory.[Availability](https://docs.python.org/3/library/intro.html#availability): Unix, Windows.

- `shutil.``chown`(*path*, *user=None*, *group=None*)

  Change owner *user* and/or *group* of the given *path*.*user* can be a system user name or a uid; the same applies to *group*. At least one argument is required.See also [`os.chown()`](https://docs.python.org/3/library/os.html#os.chown), the underlying function.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.chown` with arguments `path`, `user`, `group`.[Availability](https://docs.python.org/3/library/intro.html#availability): Unix.*New in version 3.3.*

- `shutil.``which`(*cmd*, *mode=os.F_OK | os.X_OK*, *path=None*)

  Return the path to an executable which would be run if the given *cmd* was called. If no *cmd* would be called, return `None`.*mode* is a permission mask passed to [`os.access()`](https://docs.python.org/3/library/os.html#os.access), by default determining if the file exists and executable.When no *path* is specified, the results of [`os.environ()`](https://docs.python.org/3/library/os.html#os.environ) are used, returning either the “PATH” value or a fallback of [`os.defpath`](https://docs.python.org/3/library/os.html#os.defpath).On Windows, the current directory is always prepended to the *path* whether or not you use the default or provide your own, which is the behavior the command shell uses when finding executables. Additionally, when finding the *cmd* in the *path*, the `PATHEXT` environment variable is checked. For example, if you call `shutil.which("python")`, [`which()`](https://docs.python.org/3/library/shutil.html#shutil.which) will search `PATHEXT` to know that it should look for `python.exe` within the *path* directories. For example, on Windows:>>>`>>> shutil.which("python") 'C:\\Python33\\python.EXE' `*New in version 3.3.**Changed in version 3.8:* The [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes) type is now accepted. If *cmd* type is [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes), the result type is also [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes).

- *exception* `shutil.``Error`

  This exception collects exceptions that are raised during a multi-file operation. For [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree), the exception argument is a list of 3-tuples (*srcname*, *dstname*, *exception*).

#### Platform-dependent efficient copy operations

Starting from Python 3.8, all functions involving a file copy ([`copyfile()`](https://docs.python.org/3/library/shutil.html#shutil.copyfile), [`copy()`](https://docs.python.org/3/library/shutil.html#shutil.copy), [`copy2()`](https://docs.python.org/3/library/shutil.html#shutil.copy2), [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree), and [`move()`](https://docs.python.org/3/library/shutil.html#shutil.move)) may use platform-specific “fast-copy” syscalls in order to copy the file more efficiently (see [bpo-33671](https://bugs.python.org/issue33671)). “fast-copy” means that the copying operation occurs within the kernel, avoiding the use of userspace buffers in Python as in “`outfd.write(infd.read())`”.

On macOS [fcopyfile](http://www.manpagez.com/man/3/copyfile/) is used to copy the file content (not metadata).

On Linux [`os.sendfile()`](https://docs.python.org/3/library/os.html#os.sendfile) is used.

On Windows [`shutil.copyfile()`](https://docs.python.org/3/library/shutil.html#shutil.copyfile) uses a bigger default buffer size (1 MiB instead of 64 KiB) and a [`memoryview()`](https://docs.python.org/3/library/stdtypes.html#memoryview)-based variant of [`shutil.copyfileobj()`](https://docs.python.org/3/library/shutil.html#shutil.copyfileobj) is used.

If the fast-copy operation fails and no data was written in the destination file then shutil will silently fallback on using less efficient [`copyfileobj()`](https://docs.python.org/3/library/shutil.html#shutil.copyfileobj) function internally.

*Changed in version 3.8.*

#### copytree example

This example is the implementation of the [`copytree()`](https://docs.python.org/3/library/shutil.html#shutil.copytree) function, described above, with the docstring omitted. It demonstrates many of the other functions provided by this module.

```python
def copytree(src, dst, symlinks=False):
    names = os.listdir(src)
    os.makedirs(dst)
    errors = []
    for name in names:
        srcname = os.path.join(src, name)
        dstname = os.path.join(dst, name)
        try:
            if symlinks and os.path.islink(srcname):
                linkto = os.readlink(srcname)
                os.symlink(linkto, dstname)
            elif os.path.isdir(srcname):
                copytree(srcname, dstname, symlinks)
            else:
                copy2(srcname, dstname)
            # XXX What about devices, sockets etc.?
        except OSError as why:
            errors.append((srcname, dstname, str(why)))
        # catch the Error from the recursive copytree so that we can
        # continue with other files
        except Error as err:
            errors.extend(err.args[0])
    try:
        copystat(src, dst)
    except OSError as why:
        # can't copy file access times on Windows
        if why.winerror is None:
            errors.extend((src, dst, str(why)))
    if errors:
        raise Error(errors)
```

Another example that uses the [`ignore_patterns()`](https://docs.python.org/3/library/shutil.html#shutil.ignore_patterns) helper:

```python
from shutil import copytree, ignore_patterns

copytree(source, destination, ignore=ignore_patterns('*.pyc', 'tmp*'))
```

This will copy everything except `.pyc` files and files or directories whose name starts with `tmp`.

Another example that uses the *ignore* argument to add a logging call:

```python
from shutil import copytree
import logging

def _logpath(path, names):
    logging.info('Working in %s', path)
    return []   # nothing will be ignored

copytree(source, destination, ignore=_logpath)
```

#### rmtree example

This example shows how to remove a directory tree on Windows where some of the files have their read-only bit set. It uses the onerror callback to clear the readonly bit and reattempt the remove. Any subsequent failure will propagate.

```python
import os, stat
import shutil

def remove_readonly(func, path, _):
    "Clear the readonly bit and reattempt the removal"
    os.chmod(path, stat.S_IWRITE)
    func(path)

shutil.rmtree(directory, onerror=remove_readonly)
```

### Archiving operations

*New in version 3.2.*

*Changed in version 3.5:* Added support for the *xztar* format.

High-level utilities to create and read compressed and archived files are also provided. They rely on the [`zipfile`](https://docs.python.org/3/library/zipfile.html#module-zipfile) and [`tarfile`](https://docs.python.org/3/library/tarfile.html#module-tarfile) modules.

- `shutil.``make_archive`(*base_name*, *format*[, *root_dir*[, *base_dir*[, *verbose*[, *dry_run*[, *owner*[, *group*[, *logger*]]]]]]])

  Create an archive file (such as zip or tar) and return its name.*base_name* is the name of the file to create, including the path, minus any format-specific extension. *format* is the archive format: one of “zip” (if the [`zlib`](https://docs.python.org/3/library/zlib.html#module-zlib) module is available), “tar”, “gztar” (if the [`zlib`](https://docs.python.org/3/library/zlib.html#module-zlib) module is available), “bztar” (if the [`bz2`](https://docs.python.org/3/library/bz2.html#module-bz2) module is available), or “xztar” (if the [`lzma`](https://docs.python.org/3/library/lzma.html#module-lzma) module is available).*root_dir* is a directory that will be the root directory of the archive, all paths in the archive will be relative to it; for example, we typically chdir into *root_dir* before creating the archive.*base_dir* is the directory where we start archiving from; i.e. *base_dir* will be the common prefix of all files and directories in the archive. *base_dir* must be given relative to *root_dir*. See [Archiving example with base_dir](https://docs.python.org/3/library/shutil.html#shutil-archiving-example-with-basedir) for how to use *base_dir* and *root_dir* together.*root_dir* and *base_dir* both default to the current directory.If *dry_run* is true, no archive is created, but the operations that would be executed are logged to *logger*.*owner* and *group* are used when creating a tar archive. By default, uses the current owner and group.*logger* must be an object compatible with [**PEP 282**](https://www.python.org/dev/peps/pep-0282), usually an instance of [`logging.Logger`](https://docs.python.org/3/library/logging.html#logging.Logger).The *verbose* argument is unused and deprecated.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.make_archive` with arguments `base_name`, `format`, `root_dir`, `base_dir`.*Changed in version 3.8:* The modern pax (POSIX.1-2001) format is now used instead of the legacy GNU format for archives created with `format="tar"`.

- `shutil.``get_archive_formats`()

  Return a list of supported formats for archiving. Each element of the returned sequence is a tuple `(name, description)`.By default [`shutil`](https://docs.python.org/3/library/shutil.html#module-shutil) provides these formats:*zip*: ZIP file (if the [`zlib`](https://docs.python.org/3/library/zlib.html#module-zlib) module is available).*tar*: Uncompressed tar file. Uses POSIX.1-2001 pax format for new archives.*gztar*: gzip’ed tar-file (if the [`zlib`](https://docs.python.org/3/library/zlib.html#module-zlib) module is available).*bztar*: bzip2’ed tar-file (if the [`bz2`](https://docs.python.org/3/library/bz2.html#module-bz2) module is available).*xztar*: xz’ed tar-file (if the [`lzma`](https://docs.python.org/3/library/lzma.html#module-lzma) module is available).You can register new formats or provide your own archiver for any existing formats, by using [`register_archive_format()`](https://docs.python.org/3/library/shutil.html#shutil.register_archive_format).

- `shutil.``register_archive_format`(*name*, *function*[, *extra_args*[, *description*]])

  Register an archiver for the format *name*.*function* is the callable that will be used to unpack archives. The callable will receive the *base_name* of the file to create, followed by the *base_dir* (which defaults to [`os.curdir`](https://docs.python.org/3/library/os.html#os.curdir)) to start archiving from. Further arguments are passed as keyword arguments: *owner*, *group*, *dry_run* and *logger* (as passed in [`make_archive()`](https://docs.python.org/3/library/shutil.html#shutil.make_archive)).If given, *extra_args* is a sequence of `(name, value)` pairs that will be used as extra keywords arguments when the archiver callable is used.*description* is used by [`get_archive_formats()`](https://docs.python.org/3/library/shutil.html#shutil.get_archive_formats) which returns the list of archivers. Defaults to an empty string.

- `shutil.``unregister_archive_format`(*name*)

  Remove the archive format *name* from the list of supported formats.

- `shutil.``unpack_archive`(*filename*[, *extract_dir*[, *format*]])

  Unpack an archive. *filename* is the full path of the archive.*extract_dir* is the name of the target directory where the archive is unpacked. If not provided, the current working directory is used.*format* is the archive format: one of “zip”, “tar”, “gztar”, “bztar”, or “xztar”. Or any other format registered with [`register_unpack_format()`](https://docs.python.org/3/library/shutil.html#shutil.register_unpack_format). If not provided, [`unpack_archive()`](https://docs.python.org/3/library/shutil.html#shutil.unpack_archive) will use the archive file name extension and see if an unpacker was registered for that extension. In case none is found, a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError) is raised.Raises an [auditing event](https://docs.python.org/3/library/sys.html#auditing) `shutil.unpack_archive` with arguments `filename`, `extract_dir`, `format`.*Changed in version 3.7:* Accepts a [path-like object](https://docs.python.org/3/glossary.html#term-path-like-object) for *filename* and *extract_dir*.

- `shutil.``register_unpack_format`(*name*, *extensions*, *function*[, *extra_args*[, *description*]])

  Registers an unpack format. *name* is the name of the format and *extensions* is a list of extensions corresponding to the format, like `.zip` for Zip files.*function* is the callable that will be used to unpack archives. The callable will receive the path of the archive, followed by the directory the archive must be extracted to.When provided, *extra_args* is a sequence of `(name, value)` tuples that will be passed as keywords arguments to the callable.*description* can be provided to describe the format, and will be returned by the [`get_unpack_formats()`](https://docs.python.org/3/library/shutil.html#shutil.get_unpack_formats) function.

- `shutil.``unregister_unpack_format`(*name*)

  Unregister an unpack format. *name* is the name of the format.

- `shutil.``get_unpack_formats`()

  Return a list of all registered formats for unpacking. Each element of the returned sequence is a tuple `(name, extensions, description)`.By default [`shutil`](https://docs.python.org/3/library/shutil.html#module-shutil) provides these formats:*zip*: ZIP file (unpacking compressed files works only if the corresponding module is available).*tar*: uncompressed tar file.*gztar*: gzip’ed tar-file (if the [`zlib`](https://docs.python.org/3/library/zlib.html#module-zlib) module is available).*bztar*: bzip2’ed tar-file (if the [`bz2`](https://docs.python.org/3/library/bz2.html#module-bz2) module is available).*xztar*: xz’ed tar-file (if the [`lzma`](https://docs.python.org/3/library/lzma.html#module-lzma) module is available).You can register new formats or provide your own unpacker for any existing formats, by using [`register_unpack_format()`](https://docs.python.org/3/library/shutil.html#shutil.register_unpack_format).

### Archiving example

In this example, we create a gzip’ed tar-file archive containing all files found in the `.ssh` directory of the user:

\>>>

```python
>>> from shutil import make_archive
>>> import os
>>> archive_name = os.path.expanduser(os.path.join('~', 'myarchive'))
>>> root_dir = os.path.expanduser(os.path.join('~', '.ssh'))
>>> make_archive(archive_name, 'gztar', root_dir)
'/Users/tarek/myarchive.tar.gz'
```

The resulting archive contains:

```bash
$ tar -tzvf /Users/tarek/myarchive.tar.gz
drwx------ tarek/staff       0 2010-02-01 16:23:40 ./
-rw-r--r-- tarek/staff     609 2008-06-09 13:26:54 ./authorized_keys
-rwxr-xr-x tarek/staff      65 2008-06-09 13:26:54 ./config
-rwx------ tarek/staff     668 2008-06-09 13:26:54 ./id_dsa
-rwxr-xr-x tarek/staff     609 2008-06-09 13:26:54 ./id_dsa.pub
-rw------- tarek/staff    1675 2008-06-09 13:26:54 ./id_rsa
-rw-r--r-- tarek/staff     397 2008-06-09 13:26:54 ./id_rsa.pub
-rw-r--r-- tarek/staff   37192 2010-02-06 18:23:10 ./known_hosts
```



### Archiving example with *base_dir*

In this example, similar to the [one above](https://docs.python.org/3/library/shutil.html#shutil-archiving-example), we show how to use [`make_archive()`](https://docs.python.org/3/library/shutil.html#shutil.make_archive), but this time with the usage of *base_dir*. We now have the following directory structure:

```bash
$ tree tmp
tmp
└── root
    └── structure
        ├── content
            └── please_add.txt
        └── do_not_add.txt
```

In the final archive, `please_add.txt` should be included, but `do_not_add.txt` should not. Therefore we use the following:

\>>>

```python
>>> from shutil import make_archive
>>> import os
>>> archive_name = os.path.expanduser(os.path.join('~', 'myarchive'))
>>> make_archive(
...     archive_name,
...     'tar',
...     root_dir='tmp/root',
...     base_dir='structure/content',
... )
'/Users/tarek/my_archive.tar'
```

Listing the files in the resulting archive gives us:

```bash
$ python -m tarfile -l /Users/tarek/myarchive.tar
structure/content/
structure/content/please_add.txt
```

### Querying the size of the output terminal

- `shutil.``get_terminal_size`(*fallback=(columns*, *lines)*)

  Get the size of the terminal window.For each of the two dimensions, the environment variable, `COLUMNS` and `LINES` respectively, is checked. If the variable is defined and the value is a positive integer, it is used.When `COLUMNS` or `LINES` is not defined, which is the common case, the terminal connected to [`sys.__stdout__`](https://docs.python.org/3/library/sys.html#sys.__stdout__) is queried by invoking [`os.get_terminal_size()`](https://docs.python.org/3/library/os.html#os.get_terminal_size).If the terminal size cannot be successfully queried, either because the system doesn’t support querying, or because we are not connected to a terminal, the value given in `fallback` parameter is used. `fallback` defaults to `(80, 24)` which is the default size used by many terminal emulators.The value returned is a named tuple of type [`os.terminal_size`](https://docs.python.org/3/library/os.html#os.terminal_size).See also: The Single UNIX Specification, Version 2, [Other Environment Variables](http://pubs.opengroup.org/onlinepubs/7908799/xbd/envvar.html#tag_002_003).

