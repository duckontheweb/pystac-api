Core API
--------

The most basic implementation of a STAC API is simply an endpoint that returns a valid STAC Catalog. Besides being a
valid STAC Catalog, the JSON object must contain a ``"conformsTo"`` attribute that is a list of conformance URIs for
the standards that the service conforms to.

API Interface
+++++++++++++

The :class:`pystac_client.Client` class is the main interface for working with services that conform to the STAC API spec.
This class inherits from the :class:`pystac.Catalog` class and in addition to the methods and attributes implemented by
a Catalog, it also includes convenience methods and attributes for:

* Checking conformance to various specs
* Querying a search endpoint (if the API conforms to the STAC API - Item Search spec)

Create an Instance
__________________

The easiest way to create an :class:`~pystac_client.Client` instance is using the ``pystac_client.Client.from_file`` method (inherited
from :meth:`pystac.STACObject.from_file`). The following code creates an instance by making a call to the Astraea Earth
OnDemand landing page.

.. code-block:: python

    >>> from pystac_client.Client import API
    >>> api = API.from_file('https://eod-catalog-svc-prod.astraea.earth')
    >>> api.title
    'Astraea Earth OnDemand'

Check Conformance
_________________

You can use the :meth:`pystac_client.Client.conforms_to` method to check conformance against conformance classes (specs)
commonly used in STAC APIs. This method provides the ability to check both against a single conformance URI (e.g.
``'https://api.stacspec.org/v1.0.0-beta.1/core'``), or against all known conformance URIs for a given spec. This allows
the package to be used with older APIs that may publish conformance URIs corresponding to older version of the spec or
that were not defined explicitly in the spec when the service was created.

To check against all conformance URIs for a given spec, use the attributes of :class:`pystac_client.ConformanceClasses`
rather than URI strings:

.. code-block:: python

    >>> from pystac_client import ConformanceClasses
    >>> api.conforms_to(ConformanceClasses.STAC_API_ITEM_SEARCH)
    True

To check against a single URI you can pass a string to the :meth:`~pystac_client.Client.conforms_to` method. This can be any
string at all, but you may want to use the :attr:`~pystac_client.conformance.ConformanceClass.uri` of the given conformance
class as these represent the official conformance URIs defined in the STAC API spec.

.. code-block:: python

    >>> api.conforms_to(ConformanceClasses.STAC_API_ITEM_SEARCH.uri)
    False
    >>> ConformanceClasses.STAC_API_ITEM_SEARCH.uri
    'https://api.stacspec.org/v1.0.0-beta.1/item-search'

Collections
+++++++++++

STAC APIs may provide a curated list of catalogs and collections via their ``"links"`` attribute. Links with a ``"rel"``
type of ``"child"`` represent catalogs or collections provided by the API. Since :class:`~pystac_client.Client` instances are
also :class:`pystac.Catalog` instances, we can use the methods defined on that class to get collections:

.. code-block:: python

    >>> child_links = api.get_links('child')
    >>> len(child_links)
    12
    >>> first_child_link = api.get_single_link('child')
    >>> first_child_link.resolve_stac_object(api)
    >>> first_collection = first_child_link.target
    >>> first_collection.title
    'Landsat 8 C1 T1'