# OSM transportation tag reference

Compiled 2026-11-03 from the [OpenStreetMap wiki](https://wiki.openstreetmap.org/wiki/Map_features) for bike, pedestrian, roadway, crossing, transit, parking and related mapping. 284 entries in 16 groups. The spreadsheet version (`osm_transportation_tags.xlsx`) has the same rows with filters.

**How to read it.** Values separated by " / " are alternatives. `<side>` is `left`, `right` or `both` (relative to the way's drawing direction). Placeholders like `<number>` mean free values. ⚠️ marks deprecated or discouraged tags you will still see in existing data but should not add.

**US conventions worth remembering:** give units on speeds (`maxspeed=25 mph`); use `sidewalk=separate` / `cycleway:<side>=separate` on the road when the facility is drawn as its own way; Caltrans bikeway classes map roughly as Class I = `highway=cycleway`, Class II = `cycleway:<side>=lane`, Class III = `cycleway:<side>=shared_lane` (with sharrows) or a signed route relation, Class IV = `cycleway:<side>=track` or a separate `highway=cycleway`.

## Contents

- [Road classification](#road-classification)
- [Road attributes](#road-attributes)
- [Access](#access)
- [Bicycle](#bicycle)
- [Pedestrian](#pedestrian)
- [Crossings](#crossings)
- [Intersections & control](#intersections--control)
- [Traffic calming](#traffic-calming)
- [Transit](#transit)
- [Rail](#rail)
- [Parking](#parking)
- [Shared mobility & charging](#shared-mobility--charging)
- [Barriers](#barriers)
- [Routes & relations](#routes--relations)
- [Lifecycle & meta](#lifecycle--meta)
- [Aviation & water](#aviation--water)

## Road classification

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=motorway) | `motorway` | way | Restricted-access divided freeway (Interstates, CA freeways such as SR 1 north of Morrissey) | Use with oneway=yes, one way per direction |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=trunk) | `trunk` | way | Most important non-motorway roads; in US usually expressways or major highways | US usage varies by state; check local wiki guidance |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=primary) | `primary` | way | Major arterials / important state routes | In US, typically principal arterials or state highways |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=secondary) | `secondary` | way | Minor arterials / routes linking towns | Roughly minor arterial in US practice |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=tertiary) | `tertiary` | way | Collector roads linking smaller places or neighborhoods | Roughly major collector in US practice |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=unclassified) | `unclassified` | way | Minor through roads above residential; in rural US often local through roads | Not "unknown"; for unknown use highway=road |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=residential) | `residential` | way | Local streets serving housing |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=living_street) | `living_street` | way | Shared streets where pedestrians have priority and speeds are very low | Rare in US; woonerf-style streets |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=service) | `service` | way | Access roads: driveways, parking aisles, alleys, drive-throughs | Refine with service=* |
| [`service`](https://wiki.openstreetmap.org/wiki/Key:service) | `driveway / parking_aisle / alley / drive-through / emergency_access` | way | Subtype of highway=service |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Key:highway) | `motorway_link / trunk_link / primary_link / secondary_link / tertiary_link` | way | Ramps and slip lanes connecting roads of that class | Class of the link = higher road it connects |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=track) | `track` | way | Agricultural/forestry roads | Add tracktype=grade1..grade5 |
| [`tracktype`](https://wiki.openstreetmap.org/wiki/Key:tracktype) | `grade1 / grade2 / grade3 / grade4 / grade5` | way | Track surface firmness, grade1 = paved/solid to grade5 = soft |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=road) | `road` | way | Road of unknown classification, temporary until surveyed |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=busway) | `busway` | way | Roadway dedicated to buses (BRT busways) |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=bus_guideway) | `bus_guideway` | way | Guided busway not usable by other traffic |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=escape) | `escape` | way | Runaway truck ramp |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=raceway) | `raceway` | way | Motor racing course |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=construction) | `construction` | way | Road under construction | Put future class in construction=* |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=proposed) | `proposed` | way | Planned road | Put planned class in proposed=*; often discouraged unless officially approved |
| [`motorroad`](https://wiki.openstreetmap.org/wiki/Key:motorroad) | `yes` | way | Motorway-like restrictions (no peds/bikes) on a non-motorway road |  |
| [`expressway`](https://wiki.openstreetmap.org/wiki/Key:expressway) | `yes` | way | Marks a road as an expressway (US: high-speed limited access arterial) | In use, mostly North America |
| [`junction`](https://wiki.openstreetmap.org/wiki/Key:junction) | `roundabout / circular / yes` | way, node | Roundabout (implies oneway); circular = traffic circle without roundabout priority rules |  |

## Road attributes

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`name`](https://wiki.openstreetmap.org/wiki/Key:name) | `<text>` | any | Name of the street/feature; spell out full name (Street, not St) |  |
| [`ref`](https://wiki.openstreetmap.org/wiki/Key:ref) | `<text>` | way | Route reference number, e.g. CA 1, US 101, I 280 | In US, routes better carried on route relations |
| [`lanes`](https://wiki.openstreetmap.org/wiki/Key:lanes) | `<number>` | way | Total number of marked travel lanes (both directions) | Excludes bike lanes, parking, shoulders |
| [`lanes:forward / lanes:backward`](https://wiki.openstreetmap.org/wiki/Key:lanes) | `<number>` | way | Lanes in/against direction of the way |  |
| [`lanes:both_ways`](https://wiki.openstreetmap.org/wiki/Key:lanes) | `<number>` | way | Center two-way left-turn lanes (TWLTL) |  |
| [`lanes:bus / lanes:psv`](https://wiki.openstreetmap.org/wiki/Key:lanes) | `<number>` | way | Number of bus/transit lanes |  |
| [`turn:lanes`](https://wiki.openstreetmap.org/wiki/Key:turn) | `left / through / right / slight_left / merge_to_left / reverse / none ...` | way | Turn arrows per lane, lanes separated by \| and values by ; | e.g. left\|through\|through;right |
| [`turn:lanes:forward / turn:lanes:backward`](https://wiki.openstreetmap.org/wiki/Key:turn) | `same as turn:lanes` | way | Turn lanes by direction on two-way roads |  |
| [`change:lanes`](https://wiki.openstreetmap.org/wiki/Key:change) | `yes / no / not_left / not_right / only_left / only_right` | way | Whether lane changes are allowed (solid vs dashed lines) |  |
| [`width`](https://wiki.openstreetmap.org/wiki/Key:width) | `<metres>` | way | Width of the carriageway (meters unless unit given) | Use "12 ft" or 3.7 |
| [`maxspeed`](https://wiki.openstreetmap.org/wiki/Key:maxspeed) | `<number> mph / <number>` | way | Legal speed limit | US: always include unit, e.g. "25 mph"; bare numbers = km/h |
| [`maxspeed:advisory`](https://wiki.openstreetmap.org/wiki/Key:maxspeed:advisory) | `<number> mph` | way, node | Advisory (yellow sign) speed |  |
| [`maxspeed:type / source:maxspeed`](https://wiki.openstreetmap.org/wiki/Key:source:maxspeed) | `sign / US:urban / US:CA:...` | way | Source of the speed limit (posted vs. statutory) |  |
| [`minspeed`](https://wiki.openstreetmap.org/wiki/Key:minspeed) | `<number> mph` | way | Minimum speed limit |  |
| [`maxspeed:conditional`](https://wiki.openstreetmap.org/wiki/Conditional_restrictions) | `<speed> @ (<condition>)` | way | Speed limit applying only under conditions (e.g. school zone hours) |  |
| [`oneway`](https://wiki.openstreetmap.org/wiki/Key:oneway) | `yes / -1 / no / reversible / alternating` | way | One-way traffic; -1 = opposite to drawing direction |  |
| [`surface`](https://wiki.openstreetmap.org/wiki/Key:surface) | `asphalt / concrete / paved / paving_stones / sett / compacted / fine_gravel / gravel / unpaved / dirt / ground / grass / wood / metal / sand` | way, area | Surface material |  |
| [`smoothness`](https://wiki.openstreetmap.org/wiki/Key:smoothness) | `excellent / good / intermediate / bad / very_bad / horrible / very_horrible / impassable` | way | Physical usability for wheeled vehicles (wheelchair/road bike → 4x4) |  |
| [`lit`](https://wiki.openstreetmap.org/wiki/Key:lit) | `yes / no / automatic / limited` | way | Street lighting present |  |
| [`shoulder`](https://wiki.openstreetmap.org/wiki/Key:shoulder) | `no / left / right / both` | way | Paved shoulder presence |  |
| [`shoulder:width / shoulder:surface`](https://wiki.openstreetmap.org/wiki/Key:shoulder) | `<metres> / <surface>` | way | Shoulder dimensions/material |  |
| [`placement`](https://wiki.openstreetmap.org/wiki/Key:placement) | `transition / left_of:N / right_of:N / middle_of:N` | way | Where the way is drawn relative to lanes (used on divided/complex roads) |  |
| [`dual_carriageway`](https://wiki.openstreetmap.org/wiki/Key:dual_carriageway) | `yes` | way | Way is one side of a divided road | In use |
| [`overtaking`](https://wiki.openstreetmap.org/wiki/Key:overtaking) | `yes / no / caution / forward / backward` | way | Passing allowed |  |
| [`toll`](https://wiki.openstreetmap.org/wiki/Key:toll) | `yes / no` | way | Toll road |  |
| [`maxweight / maxheight / maxwidth / maxlength`](https://wiki.openstreetmap.org/wiki/Key:maxheight) | `<value>` | way, node | Physical/legal vehicle dimension limits | maxheight="13'6\"" |
| [`hgv`](https://wiki.openstreetmap.org/wiki/Key:hgv) | `yes / no / designated / destination / delivery` | way | Truck access; designated = truck route |  |
| [`hazmat`](https://wiki.openstreetmap.org/wiki/Key:hazmat) | `yes / no / designated` | way | Hazardous materials routing |  |
| [`bridge`](https://wiki.openstreetmap.org/wiki/Key:bridge) | `yes / viaduct / boardwalk / cantilever / movable` | way | Way is on a bridge; split the way at bridge ends | Add layer=1 |
| [`tunnel`](https://wiki.openstreetmap.org/wiki/Key:tunnel) | `yes / building_passage / culvert / avalanche_protector` | way | Way goes through tunnel or under building | Add layer=-1 (except building_passage) |
| [`layer`](https://wiki.openstreetmap.org/wiki/Key:layer) | `-5 … 5` | way | Vertical ordering for crossing ways (not elevation) |  |
| [`level`](https://wiki.openstreetmap.org/wiki/Key:level) | `<number>` | node, way | Floor level inside buildings/stations |  |
| [`embankment / cutting`](https://wiki.openstreetmap.org/wiki/Key:embankment) | `yes` | way | Road on raised embankment / in a cut |  |
| [`incline`](https://wiki.openstreetmap.org/wiki/Key:incline) | `up / down / <percent>` | way | Slope along the way direction | e.g. 8% on steep paths, ramps |
| [`lane_markings`](https://wiki.openstreetmap.org/wiki/Key:lane_markings) | `yes / no` | way | Whether centre/lane lines are painted |  |
| [`divider`](https://wiki.openstreetmap.org/wiki/Key:divider) | `no / dashed_line / solid_line / double_solid_line` | way | Painted separation between directions of travel | Experimental per wiki; check taginfo for other values |
| [`sidewalk`](https://wiki.openstreetmap.org/wiki/Key:sidewalk) | `both / left / right / no / separate` | way | Sidewalk tagged on the road; separate = mapped as own footway | See Pedestrian |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `lane / track / shared_lane / no / separate ...` | way | Bike facilities tagged on the road | See Bicycle |
| [`parking:left/right/both`](https://wiki.openstreetmap.org/wiki/Street_parking) | `lane / street_side / on_kerb / no / separate ...` | way | On-street parking tagged on the road | See Parking |

## Access

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`access`](https://wiki.openstreetmap.org/wiki/Key:access) | `yes / no / private / permissive / destination / delivery / customers / agricultural / forestry / permit / unknown` | any | General access for all modes; mode keys override it |  |
| [`motor_vehicle / motorcar / motorcycle / moped / mofa`](https://wiki.openstreetmap.org/wiki/Key:access) | `yes / no / destination / private ...` | any | Access for motorized vehicle types |  |
| [`foot`](https://wiki.openstreetmap.org/wiki/Key:foot) | `yes / no / designated / permissive / private / use_sidepath / discouraged` | any | Pedestrian access; designated = signed for pedestrians |  |
| [`bicycle`](https://wiki.openstreetmap.org/wiki/Key:bicycle) | `yes / no / designated / permissive / dismount / use_sidepath / optional_sidepath / discouraged` | any | Bicycle access; use_sidepath = must use adjacent path; dismount = must walk |  |
| [`horse`](https://wiki.openstreetmap.org/wiki/Key:horse) | `yes / no / designated` | any | Equestrian access |  |
| [`psv / bus / taxi / minibus`](https://wiki.openstreetmap.org/wiki/Key:psv) | `yes / no / designated / only via lanes` | any | Public service vehicle access |  |
| [`emergency`](https://wiki.openstreetmap.org/wiki/Key:emergency) | `yes / no / designated` | any | Emergency vehicle access |  |
| [`wheelchair`](https://wiki.openstreetmap.org/wiki/Key:wheelchair) | `yes / limited / no / designated` | any | Wheelchair accessibility of path or facility |  |
| [`electric_bicycle / kick_scooter / mobility_scooter`](https://wiki.openstreetmap.org/wiki/Key:access) | `yes / no / designated` | any | Access for e-bikes, scooters, mobility devices | In use |
| [`<mode>:conditional`](https://wiki.openstreetmap.org/wiki/Conditional_restrictions) | `<value> @ (<condition>)` | any | Time/condition-dependent access, e.g. motor_vehicle:conditional=no @ (Sa,Su 08:00-18:00) |  |
| [`<mode>:lanes`](https://wiki.openstreetmap.org/wiki/Lanes) | `<value>\|<value>...` | way | Per-lane access, e.g. bus:lanes=designated\|yes\|yes |  |
| [`opening_hours`](https://wiki.openstreetmap.org/wiki/Key:opening_hours) | `Mo-Fr 07:00-19:00 ...` | any | Opening hours of facility or path |  |
| [`oneway:bicycle`](https://wiki.openstreetmap.org/wiki/Key:oneway:bicycle) | `no / yes` | way | Bike-specific oneway; oneway:bicycle=no = contraflow allowed |  |
| [`oneway:bus / oneway:psv`](https://wiki.openstreetmap.org/wiki/Key:oneway) | `no` | way | Buses may go both ways on one-way street |  |

## Bicycle

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=cycleway) | `cycleway` | way | Path designated for bikes (Class I bike path / separated track mapped as own way) | Add foot=* and segregated=* if shared |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `lane` | way | Painted bike lane (Class II) on the road |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `track` | way | Physically separated bike lane tagged on the road (Class IV), when not mapped separately |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `shared_lane` | way | Sharrows / shared lane markings (Class III with markings) | Add cycleway:*:lane=pictogram if desired |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `share_busway` | way | Bus lane that bikes may use |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `shoulder` | way | No bike facility, but rideable shoulder | In use |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `separate` | way | Bike facility exists but is mapped as its own way |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `no` | way | Surveyed: no bike facility |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `asl` | node | Advanced stop line / bike box |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `crossing` | way | Bike crossing segment |  |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `opposite / opposite_lane / opposite_track / opposite_share_busway` | way | Contraflow variants | ⚠️ Discouraged: use cycleway:left/right=* + oneway:bicycle=no |
| [`cycleway:left / cycleway:right / cycleway:both`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `lane / track / shared_lane / share_busway / separate / no` | way | Side-specific bike facility (left/right relative to way direction) | Preferred over plain cycleway=* |
| [`cycleway:<side>:lane`](https://wiki.openstreetmap.org/wiki/Key:cycleway:lane) | `exclusive / advisory / pictogram` | way | Lane type: exclusive (solid line), advisory (dashed), pictogram (sharrow) |  |
| [`cycleway:<side>:oneway`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `yes / -1 / no` | way | Direction of the bike facility (no = two-way) |  |
| [`cycleway:<side>:width`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `<metres>` | way | Width of bike lane |  |
| [`cycleway:<side>:buffer`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `yes / no / <metres>` | way | Painted buffer between bike lane and traffic/parking (buffered bike lane) | In use |
| [`cycleway:<side>:separation`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `bollard / flex_post / kerb / parking_lane / planter / jersey_barrier / solid_line / dashed_line / no` | way | Physical/painted separation type | Proposed/in use |
| [`cycleway:<side>:surface / :smoothness / :surface:colour`](https://wiki.openstreetmap.org/wiki/Key:cycleway) | `<value>` | way | Surface details of the bike lane (e.g. green paint) |  |
| [`segregated`](https://wiki.openstreetmap.org/wiki/Key:segregated) | `yes / no` | way | On shared paths: are bike and foot sections separated by line/marking |  |
| [`bicycle_road`](https://wiki.openstreetmap.org/wiki/Key:bicycle_road) | `yes` | way | Bicycle street where bikes have priority (mostly EU) |  |
| [`cyclestreet`](https://wiki.openstreetmap.org/wiki/Key:cyclestreet) | `yes` | way | Cycle street (Belgium/Netherlands style) |  |
| [`ramp:bicycle`](https://wiki.openstreetmap.org/wiki/Key:ramp:bicycle) | `yes / no` | way | Wheel channel on stairs |  |
| [`mtb:scale`](https://wiki.openstreetmap.org/wiki/Key:mtb:scale) | `0–6` | way | Mountain bike difficulty |  |
| [`mtb:scale:imba`](https://wiki.openstreetmap.org/wiki/Key:mtb:scale:imba) | `0–4` | way | IMBA trail difficulty (green circle to double black) |  |
| [`route`](https://wiki.openstreetmap.org/wiki/Tag:route=bicycle) | `bicycle / mtb` | relation | Bike route relation |  |
| [`network`](https://wiki.openstreetmap.org/wiki/Key:network) | `lcn / rcn / ncn / icn` | relation | Local / regional / national / international bike route network (USBRS = ncn) |  |
| [`cycle_network`](https://wiki.openstreetmap.org/wiki/Key:cycle_network) | `<text>` | relation | Identifier of the bike network, e.g. US:CA:SCC | In use |
| [`lcn / rcn / ncn`](https://wiki.openstreetmap.org/wiki/Key:lcn) | `yes` | way | Way is part of a bike route (when no relation exists) | Prefer route relations |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_parking) | `bicycle_parking` | node, area | Bike rack / bike parking |  |
| [`bicycle_parking`](https://wiki.openstreetmap.org/wiki/Key:bicycle_parking) | `stands / wall_loops / rack / lockers / shed / building / bollard / ground_slots / two-tier / safe_loops` | node, area | Type of bike parking (inverted-U = stands) |  |
| [`capacity`](https://wiki.openstreetmap.org/wiki/Key:capacity) | `<number>` | node, area | Number of bikes that fit |  |
| [`covered`](https://wiki.openstreetmap.org/wiki/Key:covered) | `yes / no` | node, area | Covered from weather |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_rental) | `bicycle_rental` | node, area | Bike share station / rental |  |
| [`bicycle_rental`](https://wiki.openstreetmap.org/wiki/Key:bicycle_rental) | `docking_station / dropoff_point / shop` | node | Type of rental (docked bikeshare vs. dockless hub) |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_repair_station) | `bicycle_repair_station` | node | Public repair stand / pump |  |
| [`service:bicycle:pump / :tools / :repair`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_repair_station) | `yes / no` | node | Services at repair station or shop |  |
| [`shop`](https://wiki.openstreetmap.org/wiki/Tag:shop=bicycle) | `bicycle` | node, area | Bike shop |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_wash) | `bicycle_wash` | node | Bike wash station | In use |
| [`cycleway`](https://wiki.openstreetmap.org/wiki/Tag:cycleway=crossing) | `crossing` | way | Bike path segment crossing a road: highway=cycleway + cycleway=crossing + crossing=* |  |

## Pedestrian

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=footway) | `footway` | way | Path designated for pedestrians (sidewalks, walkways) | Refine with footway=* |
| [`footway`](https://wiki.openstreetmap.org/wiki/Tag:footway=sidewalk) | `sidewalk` | way | Sidewalk mapped as its own way beside a road | Set sidewalk=separate on the road |
| [`footway`](https://wiki.openstreetmap.org/wiki/Tag:footway=crossing) | `crossing` | way | Crosswalk segment across a road | Add crossing=* matching the node |
| [`footway`](https://wiki.openstreetmap.org/wiki/Tag:footway=access_aisle) | `access_aisle` | way | Marked access aisle beside accessible parking | In use |
| [`footway`](https://wiki.openstreetmap.org/wiki/Tag:footway=traffic_island) | `traffic_island` | way | Footway segment across a median/refuge island | In use |
| [`footway`](https://wiki.openstreetmap.org/wiki/Tag:footway=link) | `link` | way | Short connector between sidewalk and crossing or street | In use |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=pedestrian) | `pedestrian` | way, area | Pedestrian street / plaza (pedestrian mall like Pacific Ave segments if closed to cars) | Area: add area=yes |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=path) | `path` | way | Generic multi-use or trail path; refine with foot/bicycle/horse=* |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=steps) | `steps` | way | Stairs; draw in upward direction for incline=up |  |
| [`step_count`](https://wiki.openstreetmap.org/wiki/Key:step_count) | `<number>` | way | Number of steps |  |
| [`handrail / handrail:left / handrail:right`](https://wiki.openstreetmap.org/wiki/Key:handrail) | `yes / no` | way | Handrails on steps or ramps |  |
| [`ramp / ramp:wheelchair / ramp:stroller`](https://wiki.openstreetmap.org/wiki/Key:ramp) | `yes / no` | way | Ramp alongside stairs |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=elevator) | `elevator` | node | Elevator connecting levels |  |
| [`conveying`](https://wiki.openstreetmap.org/wiki/Key:conveying) | `yes / forward / backward / reversible` | way | Escalator / moving walkway |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=corridor) | `corridor` | way | Indoor hallway route |  |
| [`sidewalk`](https://wiki.openstreetmap.org/wiki/Key:sidewalk) | `both / left / right / no / separate` | way | Sidewalk presence on a road |  |
| [`sidewalk:left / sidewalk:right / sidewalk:both`](https://wiki.openstreetmap.org/wiki/Key:sidewalk) | `yes / no / separate` | way | Side-specific sidewalk (preferred newer form) |  |
| [`sidewalk:<side>:surface / :width / :smoothness`](https://wiki.openstreetmap.org/wiki/Key:sidewalk) | `<value>` | way | Sidewalk attributes when tagged on the road |  |
| [`kerb`](https://wiki.openstreetmap.org/wiki/Key:kerb) | `raised / lowered / flush / rolled / no` | node | Curb type at a crossing/curb ramp (lowered/flush = curb ramp) |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Tag:barrier=kerb) | `kerb` | node, way | Curb as barrier; add kerb=* for type |  |
| [`kerb:height`](https://wiki.openstreetmap.org/wiki/Key:kerb:height) | `<metres>` | node | Curb height |  |
| [`tactile_paving`](https://wiki.openstreetmap.org/wiki/Key:tactile_paving) | `yes / no / incorrect` | node, way | Truncated domes / detectable warning surface |  |
| [`width`](https://wiki.openstreetmap.org/wiki/Key:width) | `<metres>` | way | Path/sidewalk width (ADA clear width analysis) |  |
| [`incline`](https://wiki.openstreetmap.org/wiki/Key:incline) | `<percent>` | way | Grade (running slope) |  |
| [`informal`](https://wiki.openstreetmap.org/wiki/Key:informal) | `yes` | way | Informal / social trail or desire path |  |
| [`sac_scale`](https://wiki.openstreetmap.org/wiki/Key:sac_scale) | `hiking / mountain_hiking / demanding_mountain_hiking / alpine_hiking ...` | way | Hiking difficulty |  |
| [`trail_visibility`](https://wiki.openstreetmap.org/wiki/Key:trail_visibility) | `excellent / good / intermediate / bad / horrible / no` | way | How visible the trail is |  |
| [`route`](https://wiki.openstreetmap.org/wiki/Tag:route=hiking) | `foot / hiking` | relation | Walking/hiking route relation (e.g. California Coastal Trail segments) |  |
| [`network`](https://wiki.openstreetmap.org/wiki/Key:network) | `lwn / rwn / nwn / iwn` | relation | Local / regional / national / international walking network |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bench) | `bench` | node | Bench |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=drinking_water) | `drinking_water` | node | Drinking fountain |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=toilets) | `toilets` | node, area | Public restroom |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=shelter) | `shelter` | node, area | Shelter; shelter_type=public_transport for bus shelters |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=street_lamp) | `street_lamp` | node | Street light |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=trailhead) | `trailhead` | node | Trailhead |  |
| [`area:highway`](https://wiki.openstreetmap.org/wiki/Key:area:highway) | `footway / pedestrian / cycleway / ...` | area | Micromapped outline of a path or road surface (does not replace the centerline) | In use |

## Crossings

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=crossing) | `crossing` | node | Crossing point where a path crosses a road (node on the road) | Pair with crossing=* |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `traffic_signals` | node, way | Signal-controlled crossing |  |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `uncontrolled` | node, way | Marked crosswalk without signals |  |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `unmarked` | node, way | Legal/likely crossing without markings or signals (e.g. unmarked US intersection crosswalk) |  |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `marked` | node, way | Marked crossing without signals; duplicates uncontrolled | In use, regionally preferred by some |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `no` | node | Crossing not possible/legal here |  |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `informal` | node | Informal crossing point |  |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `zebra` | node, way | Striped crossing | ⚠️ Deprecated: use crossing=uncontrolled + crossing:markings=zebra |
| [`crossing`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `island` | node, way | Crossing with refuge island | ⚠️ Obsolete: use crossing:island=yes |
| [`crossing:markings`](https://wiki.openstreetmap.org/wiki/Key:crossing:markings) | `yes / no / zebra / lines / ladder / dashes / dots / surface / ladder:skewed / lines:paired` | node, way | Type of painted crosswalk (US "continental" ≈ zebra; "standard" two lines = lines; "ladder") |  |
| [`crossing:signals`](https://wiki.openstreetmap.org/wiki/Key:crossing:signals) | `yes / no` | node, way | Signal control, independent of markings | Proposed / in use |
| [`crossing:island`](https://wiki.openstreetmap.org/wiki/Key:crossing:island) | `yes / no` | node, way | Refuge island in the crossing |  |
| [`crossing_ref`](https://wiki.openstreetmap.org/wiki/Key:crossing_ref) | `zebra / toucan / pelican / pegasus / tiger / puffin` | node, way | Regional (mainly UK) crossing type names | Not well suited to US |
| [`crossing:continuous`](https://wiki.openstreetmap.org/wiki/Key:crossing:continuous) | `yes` | node, way | Continuous sidewalk across a side street | In use |
| [`button_operated`](https://wiki.openstreetmap.org/wiki/Key:button_operated) | `yes / no` | node | Push button (beg button) for pedestrian signal |  |
| [`traffic_signals:sound`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals:sound) | `yes / no / locate` | node | Accessible pedestrian signal audible cues |  |
| [`traffic_signals:vibration`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals:vibration) | `yes / no` | node | Vibrotactile button |  |
| [`traffic_signals:countdown`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals) | `yes / no` | node | Countdown pedestrian signal | In use |
| [`traffic_signals:minimap`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals) | `yes / no` | node | Tactile map on push button | In use |
| [`supervised`](https://wiki.openstreetmap.org/wiki/Key:supervised) | `yes / no` | node | Crossing guard present |  |
| [`traffic_calming`](https://wiki.openstreetmap.org/wiki/Key:traffic_calming) | `table` | node | Raised crosswalk/table at the crossing |  |
| [`bicycle / foot / horse`](https://wiki.openstreetmap.org/wiki/Key:crossing) | `yes / no / designated` | node | Who may use the crossing (e.g. bicycle=yes for crossbike) |  |
| [`railway`](https://wiki.openstreetmap.org/wiki/Tag:railway=level_crossing) | `level_crossing` | node | Road–rail crossing |  |
| [`railway`](https://wiki.openstreetmap.org/wiki/Tag:railway=crossing) | `crossing` | node | Path (foot/bike)–rail crossing |  |
| [`crossing:barrier`](https://wiki.openstreetmap.org/wiki/Key:crossing:barrier) | `no / yes / half / double_half / full / gate` | node | Gates/barriers at rail crossings |  |
| [`crossing:bell / crossing:light`](https://wiki.openstreetmap.org/wiki/Tag:railway=level_crossing) | `yes / no` | node | Warning bell / lights at rail crossings |  |

## Intersections & control

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=traffic_signals) | `traffic_signals` | node | Traffic signal (on intersection node or at stop lines) |  |
| [`traffic_signals`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals) | `signal / traffic_lights / emergency / ramp_meter / blinker / continuous_green` | node | Signal type |  |
| [`traffic_signals:direction`](https://wiki.openstreetmap.org/wiki/Key:traffic_signals:direction) | `forward / backward / both` | node | Which direction the signal applies to (when not on intersection) |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=stop) | `stop` | node | Stop sign; place on road node before intersection (or on intersection with stop=all) |  |
| [`stop`](https://wiki.openstreetmap.org/wiki/Key:stop) | `all / minor` | node | All-way stop vs minor-road stop |  |
| [`direction`](https://wiki.openstreetmap.org/wiki/Key:direction) | `forward / backward` | node | Direction a stop/give_way applies along the way |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=give_way) | `give_way` | node | Yield sign |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=mini_roundabout) | `mini_roundabout` | node | Small roundabout drawn as a node |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=turning_circle) | `turning_circle` | node | Cul-de-sac bulb |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=turning_loop) | `turning_loop` | node | Turnaround loop with island |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=motorway_junction) | `motorway_junction` | node | Freeway exit; add ref=exit number |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:restriction) | `restriction` | relation | Turn restriction (from way, via node/way, to way) |  |
| [`restriction`](https://wiki.openstreetmap.org/wiki/Relation:restriction) | `no_left_turn / no_right_turn / no_straight_on / no_u_turn / only_left_turn / only_right_turn / only_straight_on / no_entry / no_exit` | relation | Turn restriction type |  |
| [`restriction:<mode> / except`](https://wiki.openstreetmap.org/wiki/Relation:restriction) | `<type> / bicycle;psv` | relation | Mode-specific restriction or exemptions |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:connectivity) | `connectivity` | relation | Lane-to-lane connectivity at junctions | In use |
| [`destination / destination:ref / destination:lanes`](https://wiki.openstreetmap.org/wiki/Key:destination) | `<text>` | way | Sign destinations on ramps/lanes (guide signs) |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=speed_camera) | `speed_camera` | node | Speed camera |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:enforcement) | `enforcement` | relation | Enforcement relation (red-light / speed cameras) |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=traffic_mirror) | `traffic_mirror` | node | Traffic mirror |  |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=speed_display) | `speed_display` | node | Driver feedback sign | In use |
| [`traffic_sign`](https://wiki.openstreetmap.org/wiki/Key:traffic_sign) | `US:R1-1 / US:R2-1 / ...` | node, way | Sign code (MUTCD codes in US) | Use country prefix |

## Traffic calming

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`traffic_calming`](https://wiki.openstreetmap.org/wiki/Key:traffic_calming) | `bump / hump / table / cushion / chicane / choker / island / rumble_strip / dip / painted_table / yes` | node, way | Speed bump, hump, raised table, speed cushion, chicane, neckdown, median island, rumble strip |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Tag:barrier=bollard) | `bollard / planter (diverter)` | node, way | Modal filter / diverter blocking cars |  |

## Transit

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`public_transport`](https://wiki.openstreetmap.org/wiki/Tag:public_transport=platform) | `platform` | node, way, area | Where passengers wait/board (bus stop pole or platform) | PTv2 |
| [`public_transport`](https://wiki.openstreetmap.org/wiki/Tag:public_transport=stop_position) | `stop_position` | node | Point on the road/track where the vehicle stops | PTv2 |
| [`public_transport`](https://wiki.openstreetmap.org/wiki/Tag:public_transport=station) | `station` | node, area | Transit station/center (e.g. Santa Cruz Metro Center) |  |
| [`public_transport`](https://wiki.openstreetmap.org/wiki/Tag:public_transport=stop_area) | `stop_area` | relation | Groups platforms, stop positions, station | Relation type=public_transport |
| [`highway`](https://wiki.openstreetmap.org/wiki/Tag:highway=bus_stop) | `bus_stop` | node | Bus stop (legacy and still expected alongside public_transport=platform) |  |
| [`bus / tram / train / light_rail / subway / ferry`](https://wiki.openstreetmap.org/wiki/Key:bus) | `yes` | node | Which modes serve the stop |  |
| [`shelter / bench / bin / lit / tactile_paving`](https://wiki.openstreetmap.org/wiki/Tag:highway=bus_stop) | `yes / no` | node | Bus stop amenities |  |
| [`departures_board`](https://wiki.openstreetmap.org/wiki/Key:departures_board) | `realtime / timetable / no` | node | Real-time display / printed schedule at stop |  |
| [`route_ref`](https://wiki.openstreetmap.org/wiki/Key:route_ref) | `<text>` | node | Routes serving the stop, ; separated |  |
| [`ref / local_ref / gtfs:stop_id`](https://wiki.openstreetmap.org/wiki/Key:gtfs:stop_id) | `<text>` | node | Stop number / GTFS stop ID |  |
| [`operator / network`](https://wiki.openstreetmap.org/wiki/Key:network) | `<text>` | node, relation | Operator (e.g. Santa Cruz METRO) and network |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:route) | `route` | relation | Single variant/direction of a transit route; members = stops/platforms then ways |  |
| [`route`](https://wiki.openstreetmap.org/wiki/Key:route) | `bus / trolleybus / tram / light_rail / train / subway / monorail / ferry / share_taxi / coach` | relation | Mode of the route relation |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:route_master) | `route_master` | relation | Groups all variants of a route |  |
| [`public_transport:version`](https://wiki.openstreetmap.org/wiki/Key:public_transport:version) | `2` | relation | Route follows PTv2 scheme |  |
| [`from / to / via / colour / gtfs:route_id / interval / duration / opening_hours`](https://wiki.openstreetmap.org/wiki/Relation:route) | `<value>` | relation | Route metadata |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bus_station) | `bus_station` | node, area | Bus terminal (often paired with public_transport=station) |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=ferry_terminal) | `ferry_terminal` | node, area | Ferry terminal |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=taxi) | `taxi` | node, area | Taxi stand |  |
| [`busway`](https://wiki.openstreetmap.org/wiki/Key:busway) | `lane / opposite_lane` | way | Bus lane tagged on the road (older scheme) | Prefer bus:lanes / lanes:bus |
| [`bus:lanes / psv:lanes`](https://wiki.openstreetmap.org/wiki/Lanes) | `designated \| yes \| ...` | way | Bus-only lane by lane position |  |
| [`park_ride`](https://wiki.openstreetmap.org/wiki/Key:park_ride) | `yes / bus / train / no` | node, area | Park & ride lot |  |
| [`railway`](https://wiki.openstreetmap.org/wiki/Key:railway) | `station / halt / tram_stop / platform / subway_entrance / train_station_entrance` | node, area | Rail stop features |  |

## Rail

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`railway`](https://wiki.openstreetmap.org/wiki/Key:railway) | `rail / light_rail / tram / subway / narrow_gauge / monorail / funicular / disused / abandoned / construction / proposed` | way | Rail line types (e.g. Santa Cruz Branch Line = railway=rail or disused) |  |
| [`usage`](https://wiki.openstreetmap.org/wiki/Key:usage) | `main / branch / industrial / tourism / military / freight` | way | Use of the rail line |  |
| [`service`](https://wiki.openstreetmap.org/wiki/Key:service) | `siding / spur / yard / crossover` | way | Secondary track type |  |
| [`operator / owner`](https://wiki.openstreetmap.org/wiki/Key:operator) | `<text>` | way | Rail operator/owner (e.g. SCCRTC owns the Branch Line) |  |
| [`electrified / gauge / maxspeed / tracks`](https://wiki.openstreetmap.org/wiki/Key:railway) | `<value>` | way | Rail line attributes |  |
| [`route`](https://wiki.openstreetmap.org/wiki/Tag:route=railway) | `railway / train` | relation | Rail infrastructure line vs train service route |  |
| [`highway / railway`](https://wiki.openstreetmap.org/wiki/Key:railway) | `… + railway=abandoned` | way | Rails-to-trails: trail is highway=cycleway/path; old line as railway=abandoned only if traces remain |  |

## Parking

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=parking) | `parking` | node, area | Parking lot or garage |  |
| [`parking`](https://wiki.openstreetmap.org/wiki/Key:parking) | `surface / multi-storey / underground / rooftop / carports / garage_boxes / sheds / lane / street_side` | area | Type of parking facility |  |
| [`access`](https://wiki.openstreetmap.org/wiki/Key:access) | `yes / customers / private / permit / ...` | area | Who may park |  |
| [`fee`](https://wiki.openstreetmap.org/wiki/Key:fee) | `yes / no` | area | Paid parking |  |
| [`capacity / capacity:disabled / capacity:charging`](https://wiki.openstreetmap.org/wiki/Key:capacity) | `<number>` | area | Spaces total / accessible / EV |  |
| [`maxstay`](https://wiki.openstreetmap.org/wiki/Key:maxstay) | `<duration>` | area | Time limit |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=parking_space) | `parking_space` | area | Individual parking stall |  |
| [`parking_space`](https://wiki.openstreetmap.org/wiki/Key:parking_space) | `disabled / charging / loading / normal / ...` | area | Stall type |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=parking_entrance) | `parking_entrance` | node | Entrance to garage |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=motorcycle_parking) | `motorcycle_parking` | node, area | Motorcycle parking |  |
| [`parking:<side>`](https://wiki.openstreetmap.org/wiki/Street_parking) | `no / yes / lane / street_side / on_kerb / half_on_kerb / shoulder / separate` | way | On-street parking position (side = left/right/both) |  |
| [`parking:<side>:orientation`](https://wiki.openstreetmap.org/wiki/Street_parking) | `parallel / diagonal / perpendicular` | way | Parking arrangement |  |
| [`parking:<side>:restriction`](https://wiki.openstreetmap.org/wiki/Street_parking) | `no_parking / no_stopping / no_standing / loading_only / charging_only / none` | way | Restrictions (red curb ≈ no_stopping) |  |
| [`parking:<side>:access / :fee / :maxstay / :zone / :markings / :staggered`](https://wiki.openstreetmap.org/wiki/Street_parking) | `<value>` | way | Access, fee, time limit, permit zone, marked stalls |  |
| [`parking:<side>:reason / :restriction:reason`](https://wiki.openstreetmap.org/wiki/Street_parking) | `narrow / cycleway / turn_lane / bus_stop / driveway / crossing / fire_lane / ...` | way | Physical or legal reason parking isn't allowed |  |
| [`parking:<side>:<subkey>:conditional`](https://wiki.openstreetmap.org/wiki/Street_parking) | `<value> @ (<condition>)` | way | Time-based parking rules (street cleaning, meters) |  |
| [`parking:lane:* / parking:condition:*`](https://wiki.openstreetmap.org/wiki/Street_parking) | `(old scheme)` | way | Old street parking scheme | ⚠️ Deprecated: convert to parking:<side>=* |

## Shared mobility & charging

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=charging_station) | `charging_station` | node, area | EV charging station |  |
| [`socket:<type> / capacity / fee / authentication:* / network / operator`](https://wiki.openstreetmap.org/wiki/Tag:amenity=charging_station) | `<value>` | node | Charger connectors (socket:type1_combo, socket:tesla_supercharger, socket:nacs), number, payment |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=car_sharing) | `car_sharing` | node, area | Car share pickup (e.g. Zipcar) |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=kick-scooter_rental) | `kick-scooter_rental` | node, area | E-scooter share hub | In use |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=bicycle_rental) | `bicycle_rental` | node, area | Bike share (see Bicycle) |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=fuel) | `fuel` | node, area | Gas station |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=car_rental) | `car_rental` | node, area | Car rental |  |
| [`amenity`](https://wiki.openstreetmap.org/wiki/Tag:amenity=car_wash) | `car_wash` | node, area | Car wash |  |
| [`shop`](https://wiki.openstreetmap.org/wiki/Tag:shop=car_repair) | `car_repair / tyres / car` | node, area | Vehicle services/sales |  |

## Barriers

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`barrier`](https://wiki.openstreetmap.org/wiki/Tag:barrier=bollard) | `bollard` | node, way | Post(s) blocking vehicles |  |
| [`bollard`](https://wiki.openstreetmap.org/wiki/Key:bollard) | `fixed / removable / rising / flexible / foldable` | node | Bollard type |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Key:barrier) | `gate / lift_gate / swing_gate / sliding_gate` | node, way | Gates (lift_gate = boom/arm) |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Tag:barrier=cycle_barrier) | `cycle_barrier` | node | Staggered/chicane barrier slowing bikes |  |
| [`cycle_barrier`](https://wiki.openstreetmap.org/wiki/Key:cycle_barrier) | `single / double / triple / diagonal / tilted / squeeze_gate` | node | Cycle barrier style |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Key:barrier) | `block / chain / jersey_barrier / kissing_gate / stile / turnstile / height_restrictor / toll_booth / entrance` | node, way | Other barriers on paths/roads |  |
| [`maxwidth:physical / maxheight:physical`](https://wiki.openstreetmap.org/wiki/Key:maxwidth:physical) | `<metres>` | node | Physical clearance at barrier (trailers, cargo bikes, wheelchairs) |  |
| [`locked / opening`](https://wiki.openstreetmap.org/wiki/Key:barrier) | `yes / no` | node | Whether gate is locked / opening width |  |
| [`barrier`](https://wiki.openstreetmap.org/wiki/Key:barrier) | `fence / wall / guard_rail / retaining_wall / hedge / kerb` | way | Linear barriers (guard_rail along roads) |  |

## Routes & relations

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`route`](https://wiki.openstreetmap.org/wiki/Tag:route=road) | `road` | relation | Numbered road route |  |
| [`network`](https://wiki.openstreetmap.org/wiki/United_States_roads_tagging) | `US:I / US:US / US:CA / US:CA:<county>` | relation | US road networks (Interstate, US route, state route, county route) |  |
| [`ref / modifier`](https://wiki.openstreetmap.org/wiki/Tag:route=road) | `<number> / Business / Alternate` | relation | Route number and banner |  |
| [`direction (on member role)`](https://wiki.openstreetmap.org/wiki/United_States_roads_tagging) | `north / south / east / west` | relation member | Cardinal direction roles on US route relations |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:multipolygon) | `multipolygon` | relation | Complex areas (e.g. plazas/parking with holes) |  |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:street) | `street / associatedStreet` | relation | Groups parts of a street or its addresses | Rare |
| [`type`](https://wiki.openstreetmap.org/wiki/Relation:site) | `site` | relation | Groups parts of a facility (e.g. station complex) | Proposed |

## Lifecycle & meta

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`construction:<key> / proposed:<key>`](https://wiki.openstreetmap.org/wiki/Lifecycle_prefix) | `<value>` | any | Lifecycle prefixes for features under construction/proposed |  |
| [`disused:<key> / abandoned:<key> / demolished:<key> / razed:<key>`](https://wiki.openstreetmap.org/wiki/Lifecycle_prefix) | `<value>` | any | Disused/abandoned features (demolished/razed usually removed from OSM) |  |
| [`check_date / check_date:<key>`](https://wiki.openstreetmap.org/wiki/Key:check_date) | `YYYY-MM-DD` | any | Date the feature or a tag was last verified on the ground |  |
| [`survey:date`](https://wiki.openstreetmap.org/wiki/Key:survey:date) | `YYYY-MM-DD` | any | Date of survey | Older, check_date preferred |
| [`source / source:<key>`](https://wiki.openstreetmap.org/wiki/Key:source) | `survey / Bing / Esri / local_knowledge / <text>` | any, changeset | Data source (prefer on changeset) |  |
| [`note / fixme / description`](https://wiki.openstreetmap.org/wiki/Key:fixme) | `<text>` | any | Note to mappers / flagged problem / public description |  |
| [`tiger:reviewed / tiger:*`](https://wiki.openstreetmap.org/wiki/TIGER_fixup) | `no / yes` | way | US TIGER import metadata; tiger:reviewed=no means not yet checked | Can remove after review |
| [`<key>:conditional`](https://wiki.openstreetmap.org/wiki/Conditional_restrictions) | `<value> @ (<condition>)` | any | Generic syntax for time/vehicle conditions |  |

## Aviation & water

| Key | Value(s) | On | Description | Notes |
|---|---|---|---|---|
| [`aeroway`](https://wiki.openstreetmap.org/wiki/Key:aeroway) | `aerodrome / runway / taxiway / apron / terminal / helipad / gate` | node, way, area | Airports and airfield features (e.g. Watsonville Municipal) |  |
| [`route`](https://wiki.openstreetmap.org/wiki/Tag:route=ferry) | `ferry` | way, relation | Ferry route |  |
| [`waterway`](https://wiki.openstreetmap.org/wiki/Key:waterway) | `canal / dock / lock_gate` | way, node | Navigable waterway features |  |
| [`leisure`](https://wiki.openstreetmap.org/wiki/Tag:leisure=slipway) | `marina / slipway` | node, area | Marina; slipway = boat launch ramp |  |

## Further reading

- [Map features](https://wiki.openstreetmap.org/wiki/Map_features) (master list)
- [Bicycle](https://wiki.openstreetmap.org/wiki/Bicycle) and [Bicycle tags map](https://wiki.openstreetmap.org/wiki/Bicycle_tags_map)
- [Sidewalks](https://wiki.openstreetmap.org/wiki/Sidewalks) and [Crossings](https://wiki.openstreetmap.org/wiki/Key:crossing)
- [Lanes](https://wiki.openstreetmap.org/wiki/Lanes)
- [Street parking](https://wiki.openstreetmap.org/wiki/Street_parking)
- [Public transport (PTv2)](https://wiki.openstreetmap.org/wiki/Public_transport)
- [United States roads tagging](https://wiki.openstreetmap.org/wiki/United_States_roads_tagging)
- [Taginfo](https://taginfo.openstreetmap.org) for real-world usage counts
