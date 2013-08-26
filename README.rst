Tesseract3 language files for Mongolian-Cyrillic
================================================


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
* qt-box-editor_ (for very efficient box editing)
  
  Dependencies:

   - qt4-qmake
   - libqt4-dev
   - libleptonica-dev
   - libtesseract-dev

* Gimp (for creating training images)

.. _qt-box-editor: http://zdenop.github.io/qt-box-editor/

Training routine
++++++++++++++++

You should read the main TrainingTesseract3_ guide.

.. _TrainingTesseract3: http://code.google.com/p/tesseract-ocr/wiki/TrainingTesseract3


Generate training images
------------------------

Use the text in training_text.txt to create TIFF image files.
The text block should have line spacing and letter spacing of at least 2.0.

Use at least 300ppi resolution. 10pt font size should suffice.

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
**This is the most time consuming task.**

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

The rest of it
--------------

I'll just use the tess_combine script to do the rest. If you need details see the main guide.

    ./tess_combine mnc

This will generate required files and will install the final mnc.traineddata file.

Then test your new traineddata, generate box files from it, and so on...

How to contribute
+++++++++++++++++

You can test the language data and/or train new fonts for it. 

If you think the existing training text doesn't do well, improve it, retrain it.
