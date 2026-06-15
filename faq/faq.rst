***
FAQ
***

.. index::
	single: FAQ
	see: Frequently asked questions; FAQ

Frequently Asked Questions
==========================

This is a list of Frequently Asked Questions about the HLU Tool. Feel free to suggest new entries!


**How do I get a copy of the tool?**

	The source code can be downloaded from GitHub at `github.com/HabitatFramework/HLUTool-ArcPro <https://github.com/HabitatFramework/HLUTool-ArcPro>`_ and the latest add-in installer for ArcGIS Pro can be downloaded from GitHub at `github.com/HabitatFramework/HLUTool-ArcPro/releases <https://github.com/HabitatFramework/HLUTool-ArcPro/releases>`_.

**Do I have to use UKHab with the tool?**

	No, UKHab is not an integral part of the tool or its data structure. The tool and data structure support the concept of primary and secondary habitat codes but these could be configured in the data for any suitable habitat classification including IHS and UKHab.

**Why does the tool title bar show [READONLY]?**

	This shows that the data cannot currently be edited. This is either because your userid has not been added to the database or has been added incorrectly (see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_ for details), or an edit session has not been started in ArcGIS Pro, or the active HLU layer is not editable. To enable editing, go to the ArcGIS Pro **Edit** tab and click :guilabel:`Edit` (if editing is not configured to be automatic). Once all conditions have been met the [READONLY] indicator in the dockpane header should disappear.

**Can I use data that isn't snapped to OS MasterMap?**

	Yes, TOIDs are now **optional** - features do not need to originate from or be aligned with OS MasterMap. New features can be drawn directly in the active HLU layer using the standard ArcGIS Pro editing tools and then **registered** against the database using the **Insert Feature** function (see :ref:`function_insert_feature`). Fragment identifiers are still assigned to all features, but they relate to the INCID rather than a TOID. Using OS MasterMap still brings benefits such as improved positional accuracy and a consistent national framework, but it is no longer a requirement. See :ref:`habitat_framework` and :ref:`insert_feature` for more details.

**How do I convert my existing data into the required format?**

	There are two approaches depending on whether you wish to work with or without an OS MasterMap framework:

	**Without an OS MasterMap framework (direct digitising)**

	Features can be created directly in the active HLU layer using the standard ArcGIS Pro editing tools and then **registered** against the database using the **Insert Feature** function. Each registered feature is assigned a new INCID and fragment identifier and can then be attributed in the dockpane. This approach is simpler to set up but does not bring the positional accuracy or topology benefits of an OS MasterMap framework. See :ref:`function_insert_feature` for details.

	**With an OS MasterMap framework**

	The conversion of one or more existing habitat layers into a state that can be used with the HLU Tool via an OS MasterMap framework is not simple, but the process brings all the benefits of having an OS MasterMap framework, and once completed the benefits of using the HLU Tool. There are up to 3 steps required to convert existing habitat layer(s) so that it can be used by the HLU Tool:

		1. Create an OS MasterMap framework for your habitat data.
		2. Assign the OS MasterMap framework the required attributes to format them to match the required data standards.
		3. Load the attribute data into the target relational database and save the spatial and minimum attribute data in one or more GIS layers in the required format.

	It is recommended that the conversion is performed by someone familiar with the OS MasterMap framework, expert in the configuration of the HLU Tool, experienced in advanced GIS geospatial processing, and ideally expert in SQL Server and developing data conversion routines. Enquiries can be made via the ALERC forum at `forum.lrcs.org.uk/viewforum.php?id=24 <http://forum.lrcs.org.uk/viewforum.php?id=24>`_.

**Can I hide habitat types that don't occur in my region from the drop-down lists?**

	You can currently hide primary and secondary habitats from all of the habitat-related lists in the dockpane (see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_ for details).

**Can several people use the tool at the same time?**

	Any number of users can use the tool for read-only access if they have the add-in installed. Multiple users can also use the tool in edit mode but only within the limits of the database system and ArcGIS Pro used by the tool. The HLU layers and database would also have to be configured to support multiple concurrent users.

**Does the tool work with QGIS or MapInfo?**

	This edition of the tool supports ArcGIS Pro only. An older edition of the tool supporting MapInfo (and ArcGIS Desktop) is available at `github.com/HabitatFramework/HLUTool <https://github.com/HabitatFramework/HLUTool>`_ but it does not support UKHab. If funding was available the tool could be adapted to support UKHab in MapInfo and to fully support QGIS.

**How do I report a new bug or propose a change in the tool?**

	Please check the existing known issues and change requests on GitHub at `github.com/HabitatFramework/HLUTool-ArcPro/issues <https://github.com/HabitatFramework/HLUTool-ArcPro/issues>`_ before reporting/proposing new issues or changes. New issues or proposed changes can be posted on the Knowledge Hub forum at `khub.net/group/association-of-local-environmental-records-centres/group-forum <https://khub.net/group/association-of-local-environmental-records-centres/group-forum>`_


.. raw:: latex

	\newpage

.. index::
	single: What Happened?

.. _what_happened:

What Happened?
==============

* The HLU Tool dockpane does not appear or the HLU Tool ribbon tab is missing.

	* Solution 1: The add-in may not have been loaded. Open ArcGIS Pro, go to **Project > Add-In Manager** and verify the HLU Tool add-in is listed and enabled.
	* Solution 2: No map view is open. The HLU Tool tab only appears when a map view is active. Open or create a map in the ArcGIS Pro project.

* The Bulk Update tool errors and fails to create history if the bulk update is applied to database records which do not have corresponding features in the acive HLU layer.

	* Ensure that the database and HLU layer are kept in sync so this situation does not occur.


.. raw:: latex

    \newpage

.. index::
    single: Appendix; Do's and Don't's
	single: Do's and Don't's

.. _dos_and_donts:

DO's and DON'T's
================

It is essential that the following guidelines are followed to ensure that the tool runs smoothly:

**DO's:**

	* :strong:`DO` use a file geodatabase to store the HLU GIS layers rather than shapefiles.
	* :strong:`DO` ensure the HLU layer is in an editable state in ArcGIS Pro before attempting to apply any updates, splits or merges.
	* :strong:`DO` use the **Insert Feature** function to register any newly drawn features against the database before attempting to attribute them (see :ref:`function_insert_feature`).
	* :strong:`DO` complete a physical split operation in the database immediately after performing it in the map, before commencing any other operations.

**DO NOT's:**

	* :strong:`DO NOT` remove the HLU layers from the map while the tool is running.
	* :strong:`DO NOT` switch to a different ArcGIS Pro project while the tool is running.
	* :strong:`DO NOT` use a shapefile as the HLU layer as this affects performance and imposes field name length restrictions.
	* :strong:`DO NOT` attempt to apply **Physical Split** or **Physical Merge** on a point layer - these operations are only available for line and polygon layers.
