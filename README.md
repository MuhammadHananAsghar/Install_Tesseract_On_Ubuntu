# Install Tesseract On Ubuntu


# 1. Installation
1.1 Installing Dependencies

First of all we need to install all the dependencies that are required by Tesserect. Please do not skip any command.
```sh
$ sudo apt-get install libpng-dev libjpeg-dev libtiff-dev zlib1g-dev
$ sudo apt-get install gcc g++
$ sudo apt-get install autoconf automake libtool checkinstall
```
We need image processing toolkit Leptonica to build Tesseract. During the writing of this tutorial, the latest version of Leptonica was 1.73, please check Leptonica’s official website for the latest version. Installing the latest version is highly recommended.

```sh
$ cd ~
$ wget http://www.leptonica.org/source/leptonica-1.80.0.tar.gz
$ tar -zxvf leptonica-1.80.0.tar.gz
$ cd leptonica-1.80.0 
$ ./configure
$ make
$ sudo checkinstall
$ sudo ldconfig
```
# 1.2 Compiling Tesseract

First make sure that you have git installed on your machine. If not, you can install it by running:
```sh
$ sudo apt-get install git
```
Now clone Tesseract and build it.
```sh
$ cd ~ 
$ git clone https://github.com/tesseract-ocr/tesseract.git
$ cd tesseract
$ ./autogen.sh
$ ./configure
$ make
$ sudo make install 
$ sudo ldconfig
```
# 1.3 Installing Language Components

Now download English language data for the OCR engine:
```sh
$ cd ~
$ git clone https://github.com/tesseract-ocr/tessdata.git 
$ sudo mv ~/tessdata/* /usr/local/share/tessdata/
```
Tesserect has finally been installed and configured! Now let’s run it.

# 2. Running It

Select an image with a text, and then run this command in the console (assuming img.png is the input filename):
```sh
$ tesseract img.png out
```
The text read will be saved in out.txt file in the same folder.

# 3. Using Python and Tesserect

Python-tesseract is a python wrapper for google’s Tesseract-OCR. First to install pip, follow these instructions.
```sh
$ sudo apt-get update
$ sudo apt-get -y install python-pip
```
Then to install pytesseract,
```sh
$ sudo pip install pytesseract
```
ALTERNATIVELY, if you want to download and install it from its source:
```sh
$ git clone git@github.com:madmaze/pytesseract.git 
$ sudo python setup.py install
```
Now let’s write a simple python program to read a simple captcha:
```sh
from pytesseract import image_to_string 
import Image
print image_to_string(Image.open('captcha.png'))
```
Then,
```sh
$ python test.py
```
