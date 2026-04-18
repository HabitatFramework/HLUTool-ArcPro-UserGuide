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

**Do I have to use IHS with the tool?**

	Yes, IHS is an integral part of the tool and data structure. It is likely that your existing habitat data can be translated into IHS and, once in IHS, it can easily be exported as IHS habitats, Broad habitats or Priority habitats.

**Why does the tool title bar show [READ ONLY]?**

	This shows that the data cannot currently be edited. This is either because your userid has not been added to the database or has been added incorrectly (see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_ for details), or the active HLU layer is not editable in ArcGIS Pro. To enable editing, go to the ArcGIS Pro **Edit** tab and click :guilabel:`Edit`. Once both conditions have been met the [READ ONLY] indicator in the dockpane header should disappear.

**Can I use data that isn't snapped to OS MasterMap?**

	Technically you could but only by providing dummy unique TOID values to every feature in your data. This is because the tool is designed to use the TOID to determine when a physical split or merge is to be performed and to manage the TOID_Fragment_IDs. Without dummy unique TOIDs the tool would assume all the features in your data are fragments of the same 'blank' TOID which would heavily impact on performance. However, integrating habitat data with OS MasterMap also brings other benefits such as providing spatial accuracy to your data and providing a framework within which more recent or comprehensive habitat and land use data can be applied. See :ref:`habitat_framework` for more details.

**How do I convert my existing data into the required format?**

	The conversion of one or more existing habitat layers into a state that can be used with the HLU Tool is not simple, but the process brings all the benefits of having an OS MasterMap framework, and once completed the benefits of using the HLU Tool. There are up to 4 steps required to convert existing habitat layer(s) so that it can be used by the HLU Tool:

		1. Translate the habitat code(s) to IHS.
		2. Create an OS MasterMap framework for your regional extent and load with the IHS habitat data.
		3. Assign the OS MasterMap framework the required attributes to format them to match the required standards.
		4. Load the attribute data into the target relational database and save the spatial and minimum attribute data in a valid HLU GIS layer format.

	It is recommended that the conversion is performed by someone familiar with IHS and the OS MasterMap framework, expert in the configuration of the HLU Tool, experienced in advanced GIS geospatial processing, and ideally expert in SQL Server and developing data conversion routines. Enquiries can be made via the ALERC forum at `forum.lrcs.org.uk/viewforum.php?id=24 <http://forum.lrcs.org.uk/viewforum.php?id=24>`_.

**Can I hide IHS habitats that don't occur in my region from the drop-down lists?**

	You can currently hide IHS habitats from the `Habitat` list on the IHS tab in the dockpane (see 'Lookup Tables' in the HLU Tool Technical Guide at `readthedocs.org/projects/hlutool-arcpro-technicalguide <https://readthedocs.org/projects/hlutool-arcpro-technicalguide/>`_ for details). There is also a planned change request to enable non-local IHS Habitats to be hidden from the `Habitat Type` list on the `Sources` tab in the dockpane.

**Can several people use the tool at the same time?**

	Any number of users can use the tool for read-only access if they have the add-in installed. Multiple users can also use the tool in edit mode but only within the limits of the database system and ArcGIS Pro used by the tool. The HLU layer and database would also have to be configured to support multiple concurrent users.

**Does the tool work with QGIS or MapInfo?**

	This edition of the tool supports ArcGIS Pro only. A separate edition supporting MapInfo (and ArcGIS Desktop) is available at `github.com/HabitatFramework/HLUTool <https://github.com/HabitatFramework/HLUTool>`_. If funding was available the tool could be adapted to also support QGIS.

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

* The HLU Tool stops responding to map requests.

	* Solution 1: The active HLU layer has been removed from the map or ArcGIS Pro has been closed while the tool was running. Close and relaunch the tool.
	* Solution 2: The active HLU layer is no longer selected in the **Active Layer** drop-down in the Edit group of the HLU Tool ribbon. Re-select the correct layer.

* The Bulk Update tool errors and fails to create history if the bulk update is applied to database records which do not have corresponding features in the HLU layer.

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

	* :strong:`DO` use a file geodatabase or personal geodatabase to store the HLU spatial data rather than a shapefile.
	* :strong:`DO` ensure the HLU layer is in an editable state in ArcGIS Pro before attempting to apply any updates, splits or merges.

**DO NOT's:**

	* :strong:`DO NOT` remove the HLU layer from the map while the tool is running.
	* :strong:`DO NOT` close ArcGIS Pro while the tool is running, otherwise the tool will display an error message.
	* :strong:`DO NOT` switch to a different ArcGIS Pro project while the tool is running.
	* :strong:`DO NOT` use a shapefile as the HLU layer as this affects performance and imposes field name length restrictions.
