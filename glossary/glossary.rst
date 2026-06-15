********
Glossary
********

.. index::
	single: Glossary

.. glossary::

	Accept
		Accept the proposed outstanding Ordnance Survey MasterMap update for the current INCID. Once accepted, the update will be 'Pending' and must then be applied. See :ref:`review_osmm_window` for more information.

	Apply
		Commits any changes made by the user to all of the features for the current INCID in the active HLU layer when in the dockpane. See :ref:`main_window` for more details.

	Boundary Importance
		The relative importance of each source when determining the boundary location of all the features in an INCID (e.g. of 'Primary' or 'Secondary' importance).

	Bulk Update
		Enables updates to the attributes for multiple selected INCIDs simultaneously. See :ref:`bulk_update_window` and :ref:`bulk_updates` for more details.

	Bulk Load
		Registers new GIS features against new INCIDs using OSMM attributes matched against the OSMM cross-reference table. Each feature is automatically assigned its own INCID based on habitat codes derived from OSMM descriptive attributes (Make, Descriptive Group, Descriptive Term, Theme, and Feature Code). See :ref:`bulk_load_function` for more details.

	Bulk Unload
		Removes selected registered features from the active HLU layer and cleans up their associated database records. Used to remove features that were incorrectly loaded or will be replaced during a bulk load operation. See :ref:`bulk_unload_function` for more details.

	Change Flag
		For outstanding Ordnance Survey MasterMap updates this indicates whether the proposed habitat category (e.g. 'WB') is the same as the original habitat category and whether it is a higher or lower level in the habitat hierarchy. See :ref:`review_osmm_section` for more details.

	Determination Quality
		Categorises the accuracy with which a priority habitat has been determined (e.g. 'Definitely is the priority habitat'). See :ref:`determination_quality` for more details.

	Export
		Combines spatial data for the selected features from the active HLU layer with the associated attribute data from the database into a single new GIS layer based upon a pre-defined export format. See :ref:`export_window` and :ref:`export_function` for more details.

	Feature Insert
		The process of registering one or more newly drawn GIS features - features that exist in the active HLU layer but have not yet been assigned an INCID - against new database records. Two modes are available: **Same INCID** (all selected features share a single new INCID) and **Separate INCIDs** (each selected feature receives its own new INCID). See :ref:`function_insert_feature` and :ref:`feature_insert_group` for more details.

	Fragment ID
		An incremental number used as a unique reference to individual features (fragments) within a single INCID. Where a feature has been physically split, each resulting fragment is assigned a unique fragment identifier so that the fragments can be independently updated. See :ref:`habitat_framework` for more details.

	Habitat Class
		One of the habitat classification systems used in the UK to record or describe an area of habitat (e.g. 'Phase 1', 'NVC', 'UKHab', 'IHS', BAP Priority').

	Habitat Importance
		The relative importance of each source when determining the primary and secondary habitat codes for all the features in an INCID (e.g. of 'Primary' or 'Secondary' importance).

	Habitat Type
		The code and/or descriptive term of a habitat classification system that best represents an area of habitat (e.g. 'B312', 'CG2', 'Lowland Calcareous Grassland').

	IHS
		Integrated Habitat System - a hierarchical integration of existing habitat and land use classifications used in the UK. IHS was devised by the Somerset Environmental Records Centre.

	INCID
		An **INC**\ remental **ID**\ entifier used as a unique reference to a logical group of one or more features. See :ref:`incid` for more details.

	Interpretation Comment
		A free text field to explain or provide additional reasoning behind the priority habitat determination and interpretation.

	Interpretation Quality
		A combination of the assessment of the quality and age of the original source habitat identification and the relationship between the original habitat type and the priority habitat type. See :ref:`interpretation_quality` for more details.

	Legacy Habitat
		A code and/or descriptive term that best represents an area of habitat using an alternative (legacy) habitat classification system (e.g. 'B312', 'CG2', 'Lowland Calcareous Grassland').

	Logical Merge
		Combines all the attributes for the features selected in the map into a single INCID record of one of the selected features. See :ref:`logical_merge` for more details.

	Logical Split
		Creates a single new INCID record in the database for the features selected from an existing INCID in the map. See :ref:`logical_split` for more details.

	Merge Feature
		The tool can perform two types of merge, Logical Merge or Physical Merge, depending upon the filter active in the tool. See :ref:`merge` for more details.

	Multiplex Code
		Matrix, Formation, Management and Complex codes (known collectively as 'Multiplex' codes) recorded alongside an IHS Habitat code.

	OSMM Update
		An outstanding proposed update based on recent OS MasterMap external processing. See :ref:`osmm_update` for more details.

	Physical Split
		Creates one or more new fragments in the database based upon a single feature that has been split in the map. Each resulting fragment is assigned a new fragment identifier so that they can be independently updated. See :ref:`physical_split` for more details.

	Physical Merge
		Combines two or more fragments of a single feature, that are associated with the same INCID, into a single larger feature in the map. See :ref:`physical_merge` for more details.

	Potential Priority Habitat
		Habitat areas that are close to, but do not currently meet, priority habitat definitions but may do with appropriate management or following habitat restoration work.

	Priority Habitat
		Habitats identified as requiring action in the UK Biodiversity Action Plan (UK BAP) and continue to be regarded as conservation priorities in the UK Post-2010 Biodiversity Framework.

	Process
		The activity being undertaken that has lead to applying this change to the spatial or attribute data of the current INCID. See :ref:`reason_section` for more details.

	Process Flag
		For outstanding Ordnance Survey updates this represents the type of change in the primary habitat group from the original incid feature to the new incid feature, as well as the number of sources assigned to the original incid feature.  See :ref:`review_osmm_section` for more details.

	Reason
		The underlying explanation for the change in habitat or land use. See :ref:`reason_section` for more details.

	Reassign Features
		Moves features from the active HLU layer to one or more target HLU layers based on configurable rules that match primary and secondary habitat codes. Each rule consists of a rule name and a SQL WHERE clause that selects which features should be moved. Used to ensure features are stored in the correct layer after habitat attribute updates. See :ref:`reassign_features_function` for more details.

	Registration
		The process of linking a newly created GIS feature (one with no INCID assigned) to a new record in the database. Registration assigns a new INCID and fragment identifier to the feature so that it becomes a fully managed habitat record. See :ref:`function_insert_feature` for more details.

	Reject
		Reject the proposed outstanding Ordnance Survey MasterMap update for the current INCID. See :ref:`review_osmm_window` for more information.

	Skip
		Skip the proposed outstanding Ordnance Survey MasterMap update for the current INCID so it can be reviewed again later. See :ref:`review_osmm_window` for more information.

	Source
		A dataset, document or reference used as the source of habitat or land use information. Up to three sources can be defined for each INCID. See :ref:`source_tab` for more details.

	Spatial Flag
		For outstanding Ordnance Survey MasterMap updates this indicates whether part of the new feature has been changed compared to the original framework, with An 'X' denotes when a new feature overlaps two or more features in the original framework and hence a portion of the new feature may now be assigned to a different INCID than it was originally. See :ref:`review_osmm_section` for more details.

	Split Feature
		The tool can perform two types of split, Logical Split or Physical Split, depending upon the features selected. See :ref:`split` for more details.

	TOID
		A unique **TO** \pographical **ID**\ entifier applied to features in Ordnance Survey's MasterMap product. See :ref:`habitat_framework` for more details.

	UKHab
		The UK Habitat Classification System - a new, free-to-use, unified and comprehensive approach to classifying habitats, designed to provide a simple and robust approach to survey and monitoring for the 21st century. See `ukhab.org/ <https://ukhab.org/>`_ for more information.

	Vague Date
		A specific date, range of dates or imprecise date that can be specified in a variety of formats (e.g. '23 Mar 1987', 'Mar 1987 - Jun 1987', 'Spring 1987').
