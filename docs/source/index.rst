.. pystac-client documentation master file, created by
   sphinx-quickstart on Sat Feb 27 14:27:12 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

STAC Python Client
======================

The STAC Python Client (``pystac_client``) is a Python package for working with APIs that conform to the
`STAC spec <https://github.com/radiantearth/stac-api-spec>`__ and related specifications.

Installation
------------

.. code-block:: console

   $ pip install git+https://github.com/stac-utils/pystac-client.git#egg=pystac_client

``pystac_client`` requires `Python >=3.6 <https://www.python.org/>`__.

This will also install :doc:`PySTAC <pystac:index>` as its only direct external dependency. Like PySTAC, this library
aims to keep its dependencies to a minimum.

Acknowledgements
----------------

This package builds upon the great work of the PySTAC library for working with STAC objects in Python. It also uses
concepts from the `sat-search <https://github.com/sat-utils/sat-search>`__ library for working with STAC API - Item
Search endpoints.

*While this library builds on the work of the PySTAC library and tries to follow the patterns of that project as much
as possible, `pystac-api-client` is a separate project not in any way associated with that library.*

Supported Specifications
------------------------

This library is intended to work with services that implement 1 or more of the following specifications:

* `STAC API - Core <https://github.com/radiantearth/stac-api-spec/tree/master/core>`__
* `STAC API - Item Search <https://github.com/radiantearth/stac-api-spec/tree/master/item-search>`__
   * `Fields Extension <https://github.com/radiantearth/stac-api-spec/tree/master/fragments/fields>`__ (**COMING SOON**)
   * `Query Extension <https://github.com/radiantearth/stac-api-spec/tree/master/fragments/query>`__ (**COMING SOON**)
   * `Sort Extension <https://github.com/radiantearth/stac-api-spec/tree/master/fragments/sort>`__ (**COMING SOON**)
   * `Context Extension <https://github.com/radiantearth/stac-api-spec/tree/master/fragments/context>`__
* `STAC API - Features <https://github.com/radiantearth/stac-api-spec/tree/master/ogcapi-features>`__ (based on
  `OGC API - Features <https://www.ogc.org/standards/ogcapi-features>`__) (**COMING SOON**)

User Guide
----------

This section is primarily prose and describes how to use the package to interact with the various endpoints associated
with a STAC API service. The section is organized by the spec that each set of endpoints is associated with and also
includes user guides for working with paginated responses (from the ``/collections/{collection_id}/items`` and
``/search`` endpoints)..

.. toctree::
   :maxdepth: 2

   usage/stac_api
   usage/stac_api_extensions
   usage/ogc_features

API Documentation
-----------------

This section is autogenerated from in-line code documentation. It is mostly useful as a reference for the various
classes, methods, and other objects in the library, but is not intended to function as a starting point for working
with ``pystac_client``.

.. toctree::
   :maxdepth: 2

   api

Design Decisions
----------------

We document significant design decisions using Architectural Design Records (ADRs), as described by Michael Nygard
`here <https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions>`__.

.. toctree::
   :maxdepth: 2

   design_decisions


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
