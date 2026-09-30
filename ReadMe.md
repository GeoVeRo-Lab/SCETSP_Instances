# SCETSP Numerical Instances and Solutions

This directory contains the instances and solution files used in the computational study of the segment close-enough traveling salesman problem (SCETSP) and the SCETSP without Steiner-visits (SCETSP-N). The data comprise 200 geometric layouts. Each layout is tested with close-enough radii 3, 5, and 7, yielding 600 test instances and 2,370 algorithm runs.

## Instances

The `Instance` directory contains the `Uniform` and `Directed` instance sets. Both sets use the depot at `(50, 50)`. One end of each segment is sampled uniformly from `[0, 100]^2`, and the segment length is sampled from `[15, 40]`. Segment orientations span a half-circle in `Uniform` instances and a 15-degree range in `Directed` instances.

Each set contains 10 layouts for every number of segments in `{5, 6, 7, 8, 9, 10, 20, 30, 40, 50}`. An instance filename follows

```text
<Layout>_Num_<NumberOfSegments>_ID_<LayoutID>.txt
```

For example, `Directed_Num_20_ID_4.txt` is the fourth `Directed` layout with 20 segments. The radius is not included in an instance file because the same geometry is reused for all three radii.

The first line of an instance file gives the depot coordinates.

```text
xDepot  yDepot
```

Every remaining line defines one segment by the coordinates of its two ends.

```text
xStart  yStart  xEnd  yEnd
```

Segments are indexed in their file order, beginning with segment 0.

## Solutions

The `Solution` directory contains one text file for each recorded algorithm run. A solution filename follows

```text
<Layout>_Num_<NumberOfSegments>_ID_<LayoutID>_R_<Radius>_<Method>.txt
```

For example, `Directed_Num_20_ID_4_R_5_SCETSP_Heuristic.txt` reports the two-stage heuristic result for the fourth 20-segment `Directed` layout with radius 5.

The method identifiers correspond to the following methods and tested instance sets.

| Method identifier | Method | Tested instances | Files |
| --- | --- | --- | ---: |
| `SCETSP_MISOCP` | Direct MISOCP formulation for the SCETSP | `Uniform`, 5–7 segments | 90 |
| `SCETSP_GBD` | SCETSP GBD without partial logic-based Benders cuts | `Uniform`, 5–10 segments | 180 |
| `SCETSP_GBDandLBBD` | SCETSP GBD with partial logic-based Benders cuts | `Uniform` and `Directed`, 5–10 segments | 360 |
| `SCETSP_Heuristic` | SCETSP two-stage heuristic | Both sets, 5–10 and 20–50 segments | 600 |
| `NoSteiner_PDTSPN` | GBD method of Gao et al. modified for the SCETSP-N | `Uniform`, 5–10 segments | 180 |
| `NoSteiner_GBD` | SCETSP GBD restricted to solutions without Steiner-visits | `Uniform` and `Directed`, 5–10 segments | 360 |
| `NoSteiner_LBGBD` | GBD method developed for the SCETSP-N | Both sets, 5–10 and 20–50 segments | 600 |

Each solution file contains the fields available for that run.

| Field | Description |
| --- | --- |
| `OFV` | Length of the reported route |
| `Runtime` | Computation time in seconds |
| `Gap` | Relative optimality gap reported at termination. The value is `None` when an optimality gap is not applicable |
| `repPt` | Representative coordinates selected for the depot and end-neighborhood visits, indexed by their node identifiers |
| `solType` | Solution status reported by the optimization method |
| `lowerBound` | Best lower bound available at termination |
| `upperBound` | Best feasible objective value available at termination |
| `Path` | Ordered route coordinates. Each subsequent line contains one `x y` pair, and the first and last pairs are the depot |

Fields not produced by a method are omitted. Coordinates and route lengths use the same Euclidean units as the instance files.
