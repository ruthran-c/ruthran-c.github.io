---
title: Multi-layer Interactive Maps in Tableau
date: 2024-02-27 15:50:00 -0500
categories: [Visuals]
tags: [tableau, dataviz]
---
> A common approach to storytelling is to "**Drill Down**" and to "**Zoom Out**".
{: .prompt-info}

This is the idea of starting with the larger picture before getting into the finer
details and vice versa.

We're going to build a map drill down with dynamic zone visibility. 
This is by stacking multiple geo encoded maps one on top of the other in a dashboard and controlling each
map's visibility using parameters.

## Case Objective
We have a tree census dataset of New York City's 5 boroughs. Each tree has location information on it's
1. Borough.
2. Zip Code.
3. NTA - Neighborhood tabulation area.

The objective is to build a 3-layer interactive map using Tableau.

## Methodology

|   What we need?   | How Many? |
|:-----------------:|:---------:|
|    Parameters     |     5     |
| Calculated fields |     3     |
| Dashboard actions |     5     |

> The multilayer interactive map are just 3 maps positioned in the same dashboard container with specific rules
> on when they are in/visible.<br>
> So the rules are set to make the current map <span style="color:red">disappear</span> and a deeper 
> leveled map <span style="color:green">visible</span> when a point on the map is selected.
{: .prompt-info}

### Map 1 - The Boroughs
The map contains the Boroughs.

#### Parameter - Borough
This parameter is populated only when a point on the Borough map is selected and otherwise becomes `empty`.
> Create a string type parameter and set NO current value.

#### Parameter - Borough Filter
> Create a string type parameter and set current value to '**Queens**'.

#### Calculated Field - DZV Borough 
**DZV - Dynamic Zone Visibility**.
The Borough map should be displayed when:
 - any point on the final map (NTA map) is selected, or
 - when any point outside one of the maps is selected.
```
(
    [Borough Parameter] = ''
    AND 
    [Zip Parameter] = ''
    AND
    [NTA Parameter] != ''
)
OR
(
    [Borough Parameter] = ''
    AND 
    [Zip Parameter] = ''
    AND 
    [NTA Parameter] = ''
)
```

#### Dashboard Actions - Update Borough Parameter
The Borough parameter is used to figure out when to replace the Borough map with the selected Borough's Zipcode map.
> If `Manhattan` is selected, the Borough Parameter is updated to `Manhattan` and 
> back to `empty` when the selection is cleared. 

The selection is cleared by:
1. Selecting an area/ point off map - Double click with a pause between clicks.
2. Selecting an area on a different map - Selecting a Zip or NTA on a deeper level map.

#### Dashboard Actions - Update Borough Filter
The Borough filter is used to understand which Borough is selected and to make invisible all other datapoints at the
deeper level maps.

> If `Manhattan` is selected, we only wish for Manhattan's Zipcodes to be populated in the deeper Zipcode map.

| ![Update Borough Parameter](viz/20240227-parameter.png) | ![Update Borough Filter](viz/20240227-filter.png) |

## Map 2 to Map N-1
Follow the same steps as for the top layer map (Borough) with 2 parameters, 2 dashboard actions to update those
parameters and 1 calculated field to control map visibility.

## Final Map N
The final map does not have a filter parameter and it's associated update filter action. But the rest of the steps
remain the same as above.

## Dynamic Zone Visibility
Dynaic zone visibility or DZV is the interactive mode of these multi layer maps where the focus of the map changes
with user interaction.

We do this by stacking all of these maps onto the same **dashboard container** and controlling the visibility
of each map using a `calculated field` per map.
![DZV](viz/20240227-dzv.png)


## Dashboard
> Double-clicking an area in the dashboard zooms in the area.<br>
> **Pausing** for a second between the first and second click resets to the Borough View.
{: .prompt-tip}

{% include tableau/2024-02-27-multilayer-maps.html %}

## References:
1. [Andy Kriebel - Mastering 4-Level Map Drill Downs in Tableau](https://youtu.be/w4vlyXajJCU?si=6FB1Sua88Y-yMAOA)
2. [Bob Gale's Blog - Tableau Public embed test](https://www.bawbgale.com/tableau-public-embed-test/)