redomino.appytransforms
=======================

It registers a new portal transforms that let you dynamically generate odt or ods files for a given template.

This product is based on http://appyframework.org/pod.html

Since it aims to generate native LibreOffice/OpenOffice formats, it is not necessary running libre office in server mode.

This plugin is meant for developers, it could be used for generating dynamic odt/ods files, write a custom PloneFormGen adapter, etc.

Usage
-----

Example::

    >>> from zope.component import getUtility
    >>> from Products.PortalTransforms.interfaces import IPortalTransformsTool
    >>> file_contents = open('your odt file with variables').read()     # see redomino/appytransforms/tests/input.odt
    >>> portal_transforms = getUtility(IPortalTransformsTool)
    >>> converter = portal_transforms.convertTo(target_mimetype='application/vnd.oasis.opendocument.text.transformed',
    >>>                                        orig=file_contents,
    >>>                                        mimetype='application/vnd.oasis.opendocument.text',
    >>>                                        mapper=dict(plone_version='4.3.2-sunny-day-beta'),
    >>>                                       )
    >>> transformed_odt_contents = converter.getData()

appy.pod's tips and limitations
-------------------------------

Tips and appy.pod's limitations:
* conditional text fields seems to be not supported (as far as I can see), use comments with do text if expr instead
* libreoffice does not support comments on single words (see http://ask.libreoffice.org/en/question/5256/comments-in-writer/), so it seems that you'll have to the only way to 
* repeating list items, it does not works as expected

If you are in trouble trying to get working ODT templates check out the tests doc https://github.com/redomino/redomino.appytransforms/tree/master/redomino/appytransforms/tests

TODO
----

* ods transforms


Tests
-----

Test status:

.. image:: https://secure.travis-ci.org/redomino/redomino.appytransforms.png
   :target: https://travis-ci.org/redomino/redomino.appytransforms

How to launch tests::

    $ ./bin/test -m redomino.appytransforms


Authors
-------

* Davide Moro <davide.moro@redomino.com>

