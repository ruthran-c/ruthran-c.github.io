---
title: Multi-layer Dynamic Zone Visibility Maps in Tableau
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

> In progress...👷🏗.
{: .prompt-warning}

## Dashboard
{% include tableau/2024-02-27-multilayer-maps.html %}

## References:
1. [Andy Kriebel - Mastering 4-Level Map Drill Downs in Tableau](https://youtu.be/w4vlyXajJCU?si=6FB1Sua88Y-yMAOA)
2. [Bob Gale's Blog - Tableau Public embed test](https://www.bawbgale.com/tableau-public-embed-test/)