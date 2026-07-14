********
Concepts
********

.. index::
	single: Concepts; MasterMap Framework
	single: MasterMap Framework, Concept
	see: Topographical identifier; TOID
	see: Fragment; Fragment ID

.. _data_structure:

Data Components
===============

Due to the number and complexity of data attributes and the need to minimise data duplication and reduce data volumes the spatial data and attribute data are separated into separate components. The HLU Tool provides an interface that links the spatial and attribute data and presents them to the user as a single entity.

Spatial Data
------------
The spatial data is stored in one or more GIS layers together with a minimal set of attributes that uniquely identifies and summarises each spatial feature. Separating the spatial data from the attribute data reduces the number of attributes required for the spatial layer which improves performance in ArcGIS Pro.

Attribute Data
--------------
The attribute data is stored in a relational database in a 'normalised' relational structure (i.e. groups of related attributes are divided into smaller, separate tables and relationships are defined between the tables). A normalised relational database enables the attributes to be retrieved and maintained in a very logical, and universal, way whilst simultaneously reducing the data storage requirements and improving the data structure and integrity.

.. index::
	single: Concepts; Habitat Framework
	single: Habitat Framework, Concept

.. _habitat_framework:

Habitat Framework
=================

Although most habitat surveys performed in the last 20 years are typically available as GIS layers, the spatial accuracy of the feature boundaries can be very variable. The quality will typically depend upon a range of factors, such as:

	* The quality of the original field survey maps and notes.
	* The scale and age of the base digital mapping.
	* The quality and age of any aerial photography layers.
	* The skill and patience of the GIS user digitising the data.

This variability can make it very difficult to combine habitat layers and to compare changes between surveys from different years. Moreover, unless the GIS user was very skilled or geospatial topology [2]_ was employed there will be overlaps and gaps between features which can bring problems when using the data in spatial or statistical queries.

.. [2] Geospatial topology is the arrangement for how point, line, and polygon features share geometry and is often used to define and enforce data integrity rules (e.g. no gaps should exist between polygons, there should be no overlapping features, etc).

One solution to these problems is to integrate all the habitat layers into a single framework based on Ordnance Survey's MasterMap dataset. MasterMap is the largest scale national mapping produced by the Ordnance Survey and provides highly detailed and seamless coverage.

All OS MasterMap features have a TOpographic IDentity or 'TOID' that uniquely identifies each object. OS MasterMap Topographic Area features also have a number of attributes (chiefly the Descriptive Group and Descriptive Term) that provide information about the real world object that the feature represents and these can provide basic habitat and land use information that can supplment any available habitat survey data.

Apart from the spatial representation of the features, the habitat framework only retains the TOID from OS MasterMap because all other attributes can be retrieved using this if necessary. Where OS MasterMap features need to be sub-divided into smaller units in order to represent habitat survey details that are not already shown these still retain the original TOID but are also assigned a fragment identifier so that each fragment can be uniquely identified.

.. note::
	TOIDs are now **optional**. Features can be added directly to the active HLU layer by users (drawn using ArcGIS Pro editing tools) without reference to OS MasterMap. Such features will have a blank TOID and must be **registered** using the **Insert Feature** function (see :ref:`insert_feature`) before they can be assigned habitat attributes. Fragment identifiers are still assigned to these features and relate to their INCID rather than a TOID.

.. index::
	single: Concepts; INCID
	single: INCID, Concept

.. _incid:

INCremental IDentifier (INCID)
==============================

Every feature in the GIS layer, and associated attributes in the relational database, is assigned to an INCID (\ **INC**\ remental **ID**\ entifier). An INCID can be thought of as a logical grouping of features that share a common set of attributes and are spatially related (i.e. neighbouring or proximate) [3]_. Each INCID can relate to one or more features. Grouping features with common attributes in this way reduces the number of database records required and allows the features and their attributes to all be maintained together.

In order to amend the attributes for one or more features in a larger group of features (i.e. in the same INCID as other features) without updating the remaining features, the features must first be split into their own logical grouping - i.e. they must be assigned to a new INCID (see :ref:`logical_split` for more details.)

Similarly, features from different INCIDs that are actually related and should share the same common set of attributes can be merged into the same INCID (see :ref:`logical_merge` for more details.)

.. [3] Features in the same INCID do not have to be adjacent but it is recommended that they are at least spatially associated with one-another (e.g. they are within the same site or either side of the same road/railway).

.. note::
	An ``ihs_summary`` field is maintained in the INCID table containing a concatenated string of all IHS habitat and multiplex codes. This field enables efficient querying and filtering of INCIDs based on IHS classifications.

.. raw:: latex

	\newpage

.. index::
	single: Concepts; Priority Habitats
	single: Priority Habitats, Concept

.. _priority_habitats:

Priority Habitats
=================

Some primary and secondary Habitat codes are equivalent to, or more distinct than, priority habitats [4]_. When any such codes are selected in the main window :ref:`habitats_tab` the tool automatically adds the associated priority habitats to the 'Priority Habitats' section of the :ref:`priority_tab`.

However, if priority habitat associated codes are changed or removed in the :ref:`habitats_tab` the tool does **not** automatically remove existing priority habitats from the 'Priority Habitats' section of the :ref:`details_tab`. Instead they are moved to the 'Potential Priority Habitats' section and the :ref:`determination_quality` is set to 'Previously present, but may no longer exist'.

.. note::
	Existing priority habitats that have been automatically moved to the 'Potential Priority Habitats' section, but are no longer required, must be deleted by the user (see :ref:`details_tab`).

.. [4] Priority habitats are habitats identified as habitats of principle importance for the conservation of biodiversity in England according to Section 41 of the National Environment and Rural Communities (NERC) Act. There are 56 habitats of principle importance (previously called UKBAP priority habitats) included on the S41 list.

.. index::
	single: Concepts; Potential Priority Habitats
	single: Potential Priority Habitats, Concept

.. _potential_priority_habitats:

Potential Priority Habitats
---------------------------

If a habitat area is close to, but does not currently meet, the definition of a priority habitat (but may do so with appropriate management or following habitat restoration work) then the appropriate priority habitat can be added to the 'Potential Priority Habitats' section of the :ref:`priority_tab` with the :ref:`determination_quality` set to 'Not present but close to definition'.

If a priority habitat was known to have been present but it may no longer exist then it can be added to the 'Potential Priority Habitats' section of the :ref:`priority_tab` with the :ref:`determination_quality` set to 'Previously present, but may no longer exist'.

.. raw:: latex

	\newpage

.. index::
	single: Concepts; Determination Quality
	single: Determination Quality, Concept

.. _determination_quality:

Determination Quality
---------------------

Every priority habitat and potential priority habitat must be assigned a determination quality [5]_. This categorises the accuracy with which the priority habitat has been determined and can be very useful when there is not a direct translation between the UKHab primary and secondary codes and the priority habitat, or when the original survey source(s) are not as spatially accurate as the OS MasterMap features in the framework and hence there is some uncertainty of the exact position of the priority habitat.

.. tabularcolumns:: |L|C|

.. table:: Determination Quality values and usage

	+----------------------------------------------------------+----------------------------+
	|                  Determination Quality                   |         Usage              |
	+==========================================================+============================+
	| Definitely is this habitat                               | Priority Habitat           |
	+----------------------------------------------------------+----------------------------+
	| Habitat is in polygon, but not accurately mappable       | Priority Habitat           |
	+----------------------------------------------------------+----------------------------+
	| Habitat probably in polygon, but not accurately mappable | Priority Habitat           |
	+----------------------------------------------------------+----------------------------+
	| Probably is, but some uncertainty                        | Priority Habitat           |
	+----------------------------------------------------------+----------------------------+
	| Not present but close to definition                      | Potential Priority Habitat |
	+----------------------------------------------------------+----------------------------+
	| Previously present, but may no longer exist              | Potential Priority Habitat |
	+----------------------------------------------------------+----------------------------+

.. [5] A determination quality can now also be assigned to the INCID as a whole to categorise the accuracy with which the UKHab primary and secondary codes have been determined from the original survey source(s).

.. index::
	single: Concepts; Interpretation Quality
	single: Interpretation Quality, Concept

.. _interpretation_quality:

Interpretation Quality
----------------------

Every priority habitat and potential priority habitat must be assigned an interpretation quality [6]_. This is selected based on an assessment of the quality of the original habitat type and it's relationship between it and the priority habitat type and also the age of the original habitat source(s).

.. tabularcolumns:: |L|C|C|C|

.. table:: Interpretation Quality matrix for different survey types and ages

	+------------------------------------------+-----------------------------------------+
	|               Survey Type                | Age of Survey                           |
	|                                          +---------------+------------+------------+
	|                                          | < 5 years     | 5-10 years | > 10 years |
	+==========================================+===============+============+============+
	| NVC quadrat                              | High (1)      | Medium (2) | Medium (3) |
	+------------------------------------------+---------------+------------+------------+
	| NVC rapid                                | Medium (2)    | Medium (3) | Medium (4) |
	+------------------------------------------+---------------+------------+------------+
	| Phase 1 and target notes                 | Medium (3)    | Medium (4) | Low (5)    |
	+------------------------------------------+---------------+------------+------------+
	| Phase 1 map only                         | Low (5)       | Low (5)    | Low (6)    |
	+------------------------------------------+---------------+------------+------------+
	| ESA/ SSSI site description/ species list | Medium (3)    | Medium (3) | Medium (4) |
	+------------------------------------------+---------------+------------+------------+
	| Aerial Photo, Landcover                  | Low (5)       | Low (6)    | Low (7)    |
	+------------------------------------------+---------------+------------+------------+
	| Expert knowledge of site quality         | Medium (4)    | Medium (4) | Low (5)    |
	+------------------------------------------+---------------+------------+------------+

.. [6] An interpretation quality can now also be assigned to the INCID as a whole to assign a quality to the relationship between the primary and secondary codes and the survey type and age of the original habitat source(s).

.. raw:: latex

	\newpage

.. _split:

Splitting Features
==================

There are two ways to split features depending upon the filter active in the tool - **logical split** and **physical split**.

.. index::
	single: Concepts; Logical Split
	single: Split Features; Logical Split, Concept

.. _logical_split:

Logical Split
-------------

Logical split is used to create a new INCID in the database based upon a subset of features selected from a single INCID in the GIS layer. Logically splitting one or more features assigns them to a different INCID than the other features in the current INCID which then allows them to be updated independently of the remaining features in the original INCID.

For example, a group of adjacent permanent pasture features may be 'logically' grouped by being assigned to the same INCID because they share a common set of UKHab primary and secondary codes, sources and other attributes. However, it may be later recognised that one or more of the features are actually being managed differently to the remaining features. By logically splitting those features from the original INCID to form a new INCID those features can then be assigned a different management secondary code.

.. note::
	Logical split rules

		* Only if one or more features from a single INCID are present in the current filter will the tool allow a logical split to be performed.
		* The selected features must all belong to the same INCID.

.. index::
	single: Concepts; Physical Split
	single: Split Features; Physical Split, Concept

.. _physical_split:

Physical Split
--------------

Physical split is used to create one or more new fragments in the database based upon a single feature that has already been split in the GIS layer. Physically splitting a feature into fragments allows them to be updated independently of each other (once they have also been assigned to different INCIDs - see :ref:`logical_split`.)

For example, a woodland may appear as a single feature, but compartments within the woodland may be managed differently and/or may have different characteristics. By physically splitting the woodland feature along the compartment boundaries each compartment can then be assigned to its own INCID (by performing a :ref:`logical_split`) so that they can be assigned different matrix, formation and management codes.

.. note::
	Physical split rules

		* Only if two or more fragments from the same INCID with the same Fragment ID are present in the current filter will the tool allow a physical split to be performed.
		* Only one feature should be split in a single operation. Splitting multiple features will cause database synchronisation issues.
		* If several features have been split, select the fragments for one original feature and split using the tool. Repeat this operation for the remaining features.
		* Ensure that the physical split is completed in the database prior to commencing any other operations such as 'Select by attributes …' to avoid database synchronisation issues.
		* Physical split is not available for **point** layers, as a single point feature cannot be geometrically subdivided.

.. note::
	If two or more fragments from the same INCID and with the same Fragment ID are selected in the GIS and **Get Map Selection** is clicked then the tool will recognise that the fragments must have been split by the user in the GIS layer and will inform the user that a physical split can be performed.

.. raw:: latex

	\newpage

.. _merge:

Merging Features
================

There are two ways to merge features depending upon the filter active in the tool - **logical merge** and **physical merge**.

.. index::
	single: Concepts; Logical Merge
	single: Merge Features; Logical Merge, Concept

.. _logical_merge:

Logical Merge
-------------

Logical merge combines all the features selected in the GIS into a single INCID chosen from from the selected features. This assigns the attributes from the chosen INCID to all the other selected features and logically groups the features into a single INCID so that they can be updated together in the future.

.. index::
	single: Concepts; Physical Merge
	single: Merge Features; Physical Merge, Concept

.. _physical_merge:

Physical Merge
--------------

Physical merge combines fragments of a single feature, that share the same INCID, into a single larger feature in the GIS layer. As the fragments must already belong to the same INCID there are no attribute updates but the boundaries between adjacent features will be removed.

.. note::
	Physical merge rules

		* Only fragments belonging to the same INCID can be merged in a single physical merge operation.
		* If fragments for several groups need to be merged, the operation must be repeated for each group.
		* Physical merge is not available for **point** layers.

.. index::
	single: Concepts; Attribute Updates
	single: Updates; Attribute Updates, Concept

.. _attribute_update:

Attribute Updates
=================

Attribute updates are the main mechanism for updating existing INCID details. Typically attribute changes can only be applied to one INCID at a time, and any changes attributes applied to the INCID are also held in the GIS layer (e.g. primary and secondary codes) then they are also applied to any features for the current INCID selected in the active GIS layer (or to all features for the current INCID if no features are selected).

.. index::
	single: Concepts; Bulk Updates
	single: Updates; Bulk Updates, Concept

.. _bulk_update:

Bulk Updates
============

Attribute updates can also be applied in bulk to multiple INCID records at the same time. Any changes made will be applied to all INCIDs in the active filter and will also be reflected in the active GIS layer if any of the changed attributes are also held in the GIS layer (e.g. primary and secondary codes).

.. note::
	This function is only available to users who have been given bulk update permissions. For details on configuring users see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_.

.. index::
	single: Concepts; Feature Insert
	single: Feature Insert, Concept

.. _insert_feature:

Feature Inserts
===============

New features can be added to the active HLU layer at any time using the standard ArcGIS Pro editing tools. Newly drawn features do not initially have an INCID or fragment identifier assigned to them — they must be **registered** against the database before they can be attributed.

TOIDs are **optional**. Features do not need to originate from or be aligned with OS MasterMap. Once drawn and selected, new features are registered using the **Insert Feature** function in the :ref:`feature_insert_group` of the HLU Tool ribbon, which creates new INCID and fragment identifier records in the database. Two modes are available:

* **Same INCID** — all selected new features are assigned to a single new INCID, each with a sequential fragment identifier. Use this when the features represent multiple fragments of the same habitat record.
* **Separate INCIDs** — each selected new feature receives its own new INCID. Use this when each feature represents a distinct, independent habitat record.

The HLU layer supports a set of optional attribute columns (``habprimary``, ``habsecond``, ``determqty`` and ``interpqty``) that can be pre-populated before registering new features. When present and valid, the tool reads these columns and uses their values to initialise the corresponding database attributes for the new INCID record, reducing the amount of manual data entry required afterwards. Any values that fail validation are ignored and the GIS columns are updated on success to remove them. Further attributes — such as priority habitats, boundary and digitisation details, site reference, condition, comments and sources — will typically need to be completed in the dockpane after the insert.

See :ref:`function_insert_feature` for full details and step-by-step instructions.

.. index::
	single: Concepts; Bulk Unload
	single: Bulk Unload, Concept

.. _bulk_unload:

Bulk Unload
===========

Bulk unload is used to remove selected registered features from the active HLU layer and clean up their associated database records. This operation is useful for:

* Removing features that were incorrectly loaded
* Removing features that will be replaced during a bulk load operation
* Cleaning up test or temporary data

The bulk unload operation permanently removes features from one or more HLU layers and deletes their associated INCID records from the database (if not referenced by any remaining features). This ensures that both the spatial and attribute data remain synchronized.

.. note::
	Bulk unload rules

		* Only features that are currently selected in one or more HLU layers can be unloaded.
		* Features are only removed from the layers selected by the user.
		* Database records (INCIDs) are only deleted if all associated features are removed from all layers.
		* If an INCID has features in multiple layers, unloading features from one layer will not delete the INCID record unless all features from all layers are unloaded.
		* The operation cannot be undone — ensure you have selected the correct features before proceeding.

See :ref:`bulk_unload_function` for full details and step-by-step instructions.

.. index::
	single: Concepts; Bulk Load
	single: Bulk Load, Concept

.. _bulk_load:

Bulk Load
=========

Bulk load is used to register multiple new features against new INCIDs in a single operation using OSMM (Ordnance Survey MasterMap) attributes matched against the OSMM cross-reference table. This operation provides a fast and efficient way to load large numbers of features into the habitat framework.

The bulk load operation automatically:

* Creates a staging layer to hold the newly loaded features
* Copies selected features from an OSMM source layer to the staging layer
* Matches the OSMM attributes (Make, Descriptive Group, Descriptive Term, Theme, Feature Code) against the cross-reference table to determine appropriate habitat codes
* Creates new INCID records in the database for each feature with the matched habitat codes
* Assigns unique fragment identifiers to each feature
* Updates the staging layer features with the new INCID, fragment identifiers and habitat codes

Each feature in the source layer is assigned to its own new INCID, allowing the features to be independently attributed and maintained. Features can be subsequently reassigned to other layers using the Reassign Features function, or logically merged if they should share the same INCID.

.. note::
	Bulk load rules

		* Each feature in the input layer is assigned to its own new INCID.
		* The source layer must contain OSMM features with the required attributes (Make, Descriptive Group, Descriptive Term, Theme, Feature Code).
		* TOID is optional but recommended for tracking features back to their OS MasterMap origin.
		* Features that cannot be matched against the OSMM cross-reference table will still be loaded but their habitat attributes will be null and must be assigned manually.
		* The staging layer is a temporary working layer — features should be moved to permanent layers using the Reassign Features function.
		* The OSMM cross-reference table (``lut_osmm_habitat_xref``) must be populated in the database with appropriate habitat mappings.

See :ref:`bulk_load_function` for full details and step-by-step instructions.

.. index::
	single: Concepts; OSMM Updates
	single: Updates; OSMM Updates, Concept

.. _osmm_update:

OSMM Updates
============

If the habitat framework has been externally processed against a more recent OS MasterMap (OSMM) update there may be proposed OSMM updates to review and apply. Any proposed updates are INCID specific and will appear at the top of the main interface (if one of the options to display them is configured in the user options) for the current INCID. Proposed updates can be reviewed one INCID at a time where they can either be accepted (when they become pending updates) or rejected. Pending updates can then be applied in bulk in a method similar to the bulk update process.

.. note::
	This function is only available to configured users who have been given bulk update permissions. For details on configuring users see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_.
