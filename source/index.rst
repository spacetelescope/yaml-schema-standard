YAML Schema Standard
====================

This document describes the YAML Schema format, an extension to JSON Schema
designed specifically for validating and documenting data products serialized
as YAML.

**This document is a work in progress and does not represent a
released version of the YAML Schema standard.**

.. toctree::
   :maxdepth: 1
   :hidden:

   schemas/stsci.edu/yaml-schema/draft-01.rst
   changes.rst

Introduction
------------

:ref:`YAML Schema <http://stsci.edu/schemas/yaml-schema/draft-01>` is a small
extension to `JSON Schema Draft 4
<http://json-schema.org/latest/json-schema-validation.html>`__ so support
features unique to YAML data serialization language (as opposed to plain JSON),
as well as enhance documentation of schemas.  `Understanding
JSON Schema <http://spacetelescope.github.io/understanding-json-schema/>`__
provides a good resource for understanding how to use JSON Schema, and further
resources are available at `json-schema.org
<http://json-schema.org>`__.  A working understanding of YAML and JSON Schema
is assumed for this document, which only describes what makes YAML
Schema different from JSON Schema.

A YAML schema as defined by this document is typically serialized as YAML,
though may also be serialized as JSON (JSON being a subset of YAML), or any
other format that can encapsulate the structure of JSON data.  In fact, many
JSON Schema validators work by deserializing a JSON document into native data
structures of the language in which it is implemented, and checking that data
structure against the schema.  So although the schema itself is defined in
JSON, JSON Schema is not strictly limited to data that has been at one time
serialized as JSON.  It is, however, limited to data structures that can be
serialized as JSON.

Given some data structure, it will generally be possible to serialize it either
as JSON or as YAML.  However, YAML serializations may contain additional
explicit structure that is not possible in JSON without use of local,
application-specific conventions.  Examples include tags, and ordered objects,
both of which are described in more detail below.  As YAML is designed with
human-readability in mind, presentation is also of more concern, and the YAML
specification has more to say on the topic than JSON.  YAML often provides
multiple options for how the same data can be presented (beyond just placement
of whitespace), and a schema can be used to provide hints to YAML writers for
how a given data structure should be serialized for optimal readability.

To be clear, the JSON Schema specification allows extensions by design [#f1]_,
through definition of additional keywords that may be used in a schema.  JSON
Schema implementations that do not support the additional keywords should
ignore them; as such, to support YAML Schema it is necessary to provide JSON
Schema implementations that interpret the added keywords.  Also, just as JSON
Schema provides a metaschema [#f2]_, YAML Schema has a metaschema describing
how to correctly interpret its additional keywords.  The YAML Schema metaschema
*extends* JSON Schema's metaschema using the JSON Schema extension capability,
and as such is a superset of JSON Schema's metaschema.

History
-------

TODO: Mention as additional history that YAML Schema was created specifically
for ASDF, but may have broader application as well.  Note that by offering
YAML Schema to the community outside the context of ASDF we hope to drive
adoption of this format within the YAML community, and drive development of
implementations.


New Keywords
------------

YAML Schema adds five new keywords to JSON Schema:

TODO: Put a table of contents here, linking to the descriptions of the new
keyword below.


``tag`` keyword
^^^^^^^^^^^^^^^

``tag``, which may be attached to any data type, declares that the
element must have the given YAML tag.

TODO: Write new documentation for this keyword with references/examples
from an example schema that would be included with this documentation, as
opposed to using ASDF as an example.


``propertyOrder`` keyword
^^^^^^^^^^^^^^^^^^^^^^^^^

``propertyOrder``, which applies only to objects, declares that the object must
have its properties presented in the given order.

*TBD: It is not yet clear whether this keyword is necessary or desirable.*

YAML provides an ``!!omap`` type [TODO: link to YAML spec] for *ordered*
mappings.  In JSON terms, this equates to semantically meaningful order to
the properties in the object, which is not normally possible in JSON without
a local convention.  As native language support for ordered mappings is not
implemented in all YAML parsers, applications may choose to ignore this
keyword for validation purposes.  However, this keyword may also be used as
a presentation hint, informing the YAML writer on the order to write out
keywords in a specific mapping object, where possible.


``style`` keyword
^^^^^^^^^^^^^^^^^

TODO


``flowStyle`` keyword
^^^^^^^^^^^^^^^^^^^^^

TODO


``examples`` keyword
^^^^^^^^^^^^^^^^^^^^

The schema may contain a list of examples demonstrating how to use the
schema.  It is a list where each item is a pair.  The first item in
the pair is a prose description of the example, and the second item is
YAML content (as a string) containing the example.

For example::

  examples:
    -
      - Complex number: 1 real, -1 imaginary
      - "!complex 1-1j"

This keyword is purely for informational purposes, and while the examples
may contain YAML, there is otherwise nothing YAML-specific about it.  This
keyword can help in generation of nice documentation for schema, as well as
writing automated tests of the schema in-line with the schema definition
itself.


.. rubric:: Footnotes

.. [#f1] `Extending the JSON Schema core definition <http://json-schema.org/latest/json-schema-core.html#anchor20>`_
.. [#f2] `JSON Schema Meta Core Meta-Schema <https://github.com/Julian/jsonschema/blob/4baff2178f4ade789cb6049f2b6bcd9031c8f89f/jsonschema/schemas/draft4.json>`_ (on GitHub for ease of viewing)


.. only:: html

   There is also a `print version of this document
   <http://spacetelescope.github.io/yaml-schema-standard/YAMLSchemaStandard-0.1.0.dev0.pdf>`__.

.. only:: html

    * :ref:`genindex`
    * :ref:`search`
