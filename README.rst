Tesseract3 language files for Mongolian-Cyrillic
================================================

Main guide: http://code.google.com/p/tesseract-ocr/wiki/TrainingTesseract3


Current status
++++++++++++++

* Arial font set support
  - Arial
  - Arial Bold
  - Arial Italic
  - Arial Bold Italic

TODO
++++

* Times New Roman font set support
* Improve frequent_word_list

Dev tools
+++++++++

* Ubuntu 12.04
* Tesseract 3.02 with Leptonica (tesseract-ocr)
* qt-box-editor (for very efficient box editing)
  Dependencies:
   - qt4-qmake
   - libqt4-dev
   - libleptonica-dev
   - libtesseract-dev
* Gimp (for creating training images)

Training routine
++++++++++++++++

You should read the main TesseractTraining3 guide.

Generate training images
------------------------

Use the test in training_text.txt to create TIFF image file.
The text should have line spacing and letter spacing of at least 2.0.

Use 300ppi resolution and 10pt font size.

In Gimp, save the image as "tif" and choose "deflate" as compression.

The file name should be structured as mnc.[fontname].exp[num].tif.

Generate and edit box files
---------------------------

    tesseract mnc.[fontname].exp[num].tif mnc.[fontname].exp[num] batch.nochop makebox

Or if you already have mnc.traineddata installed:

    tesseract mnc.[fontname].exp[num].tif mnc.[fontname].exp[num] -l mnc batch.nochop makebox

You can use a shortcut for the latter command:

    ./tess_mkbox mnc [fontname] [expnum]

Edit the generated .box file to correct misrecognized characters.
This is the most time consuming task.

Train
-----
Use the box and tif files for training Tesseract.

    tesseract mnc.[fontname].exp[num].tif mnc.[fontname].exp[num] box.train.stderr

Or just:

    ./tess_train mnc [fontname] [expnum]

The output of the command should not contain any FAIL messages.

Update font_properties
----------------------
If you're adding a new font, you should add it to font_properties file.
Look up the main guide about it.

The rest
--------

I'll just use the tess_combine script to do the rest. If you need details see the main guide.

    ./tess_combine mnc

This will generate required files and will install the final mnc.traineddata file.


