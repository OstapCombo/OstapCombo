# Keeping AI answers connected to sources

By Igor Grigoryev · Design note

An AI interface should preserve the difference between a retrieved fact, a calculation and an interpretation. This matters when a polished answer could conceal a missing source.

## Store the claim with its origin

A useful claim record contains the source identifier, retrieval time, relevant excerpt or field, transformation method and verification state. Store the source version or digest when it can change.

For example, if a dataset reports an area and a geometry calculation produces another value, keep both. Name the method and units. Do not silently replace one with the other.

## Treat tool output as bounded evidence

| Output | Supports | Does not establish by itself |
| --- | --- | --- |
| Search result | A candidate record exists | That it is the intended record |
| Bounding box | A spatial extent | A parcel boundary |
| Calculated area | An area under a stated method and CRS | Legal title area |
| Price observation | A price at a stated time and source | Current availability or market value |
| Generated summary | A reading of the supplied evidence | Independent verification |

## Handle missing evidence explicitly

An empty search is different from an unavailable source. A partial page is different from a complete export. A successful extraction is different from a verified identity match.

The interface should tell the user which case occurred and what evidence would resolve it. Keep uncertainty attached to the claim as it moves from a tool result to a card, comparison or report.

## Publish reproducible examples

Use synthetic or explicitly cleared data. Include the input, method, expected output and known limits. Credit collaborators and upstream projects. Share the general method without exposing customer records or private infrastructure.

This is an engineering approach to source handling, not legal or cadastral verification.

[Back to profile](../README.md)
