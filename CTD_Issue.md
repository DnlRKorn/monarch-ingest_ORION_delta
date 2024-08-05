```
        # if this is not a good amount of evidence
        if therapeutic_count == marker_count and therapeutic_count < 3:
            # nothing is usable
            return None

        # if there are no markers but there is evidence
        if marker_count == 0 and therapeutic_count > 0:
            return self.therapeutic_predicate

        # if there is no therapeutic evidence but there are markers
        if therapeutic_count == 0 and marker_count > 0:
            return self.marker_predicate

        # get the marker flag
        marker = (therapeutic_count == 1 and marker_count > 1) or (marker_count / therapeutic_count > 2)

        # get the therapeutic flag
        therapeutic = (marker_count == 1 and therapeutic_count > 1) or (therapeutic_count / marker_count > 2)
```

This code in ORION's load_CTD.py basically has a system to resolve conflicts between "marker" and "therapeutic" predicates.

Monarch-Ingest/Koza produces only edges of type "biolink:treats_or_applied_or_studied_to_treat". It produces 38527 edges.

ORION contains edges of type "CTD:contributes_to" and "biolink:treats_or_applied_or_studied_to_treat".
CTD:contributes_to                               64355
biolink:treats_or_applied_or_studied_to_treat    34766

ORION is missing 3,761 "biolink:treats" edges which Koza ingested. Koza is missing all "CTD:contributes_to" edges.
