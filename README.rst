============
On this Fork
============
This fork actually limits some of the features for django-thumbs. the pip install I found was
not python3 compatible which this is (the source on github is mostly compatible with python3). The changes I made were
reasonably minor but effectively this version does away with all settings that can be used in a settings.py file.
Additionally I switched from using cStringIo to io to make it python3 compatible as I found out cStringio is no longer supported by ptyhon3. Their is a very minor imporvement here with thumbnail lookup as it shortcircuits the loop when it finds a match. Finally variables are now pep8 compliant.


=============
Django-thumbs
=============

The easiest way to create thumbnails for your images with Django. Works with any StorageBackend.


Features
========
  
* Easy to integrate in your code (no database changes, works as an ImageField)
* Works perfectly with any StorageBackend
* Generates thumbnails after image is uploaded into memory
* Deletes thumbnails when the image file is deleted
* Provides easy access to the thumbnails' URLs (similar method as with ImageField)


Requirements
============

* Python 2.5+
* Django 1.1+
* PIL (Python Image Library)


Getting It
==========

You can get Django-Thumbs by using pip or easy_install:

::

  $ pip install django-thumbs
  or
  $ easy_install django-thumbs

If you want to install it from source, grab the git repository from github and run setup.py:

::

  $ git clone git://github.com/skitoo/django-thumbs.git
  $ cd django-thumbs
  $ python setup.py install


Installation
============

* Import it in your models.py and replace ImageField with ImageWithThumbsField in your model
* Add a sizes attribute with a list of sizes you want to use for the thumbnails
* Make sure your have defined MEDIA_URL in your settings.py
* That's it!

Working example
===============

::

    from django.db import models
    from django_thumbs.db.models import ImageWithThumbsField

    class Person(models.Model):
        photo = ImageWithThumbsField(upload_to='images', sizes=((125,125),(200,200)))
        second_photo = ImageWithThumbsField(upload_to='images')

In this example we have a Person model with 2 image fields.

You can see the field second_photo doesn't have a sizes attribute. This field works exactly the same way as a normal ImageField.

The field photo has a sizes attribute specifying desired sizes for the thumbnails. This field works the same way as ImageField but it also creates the desired thumbnails when uploading a new file and deletes the thumbnails when deleting the file.

With ImageField you retrieve the URL for the image with: someone.photo.url With ImageWithThumbsField you retrieve it the same way. You also retrieve the URL for every thumbnail specifying its size: In this example we use someone.photo.url_125x125 and someone.photo.url_200x200 to get the URL of both thumbnails.

Uninstall
=========
At any time you can go back and use ImageField again without altering the database or anything else. Just replace ImageWithThumbsField with ImageField again and make sure you delete the sizes attribute. Everything will work the same way it worked before using django-thumbs. Just remember to delete generated thumbnails in the case you don't want to have them anymore.

