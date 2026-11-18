# tpt-nova-viz

Visualization domain extension for [tpt-nova](#upstream-dependencies), by **TPT Solutions**.

Where `tpt-nova-games` prioritizes real-time interactivity and `tpt-nova-sim` prioritizes determinism, `tpt-nova-viz` prioritizes **precision, scale, and professional-grade data representation** for engineering, architecture, scientific research and industrial data analysis.

> Status: Draft v0.1 — planning stage. See [TODO.md](TODO.md) for progress and [spec.txt](spec.txt) for the design spec.

## Planned crates

| Crate | Purpose |
|---|---|
| `tpt-nova-viz` | Root facade crate |
| `tpt-nova-viz-pointcloud` | Massive point cloud rendering with LOD streaming (LAS/LAZ/PTS/XYZ/E57) |
| `tpt-nova-viz-cad` | CAD/BIM parsing and visualization (OBJ, glTF, STL in v0.1; STEP/IFC later) |
| `tpt-nova-viz-measure` | Distance, angle, area, volume measurement |
| `tpt-nova-viz-annotate` | 3D text, arrows, callouts, layers |
| `tpt-nova-viz-volume` | Volumetric rendering (DICOM, NRRD, raw) |
| `tpt-nova-viz-camera` | Sub-millimeter precision camera controls |
| `tpt-nova-viz-export` | PNG/JPEG/PDF/MP4/glTF/OBJ/STL export |

Every crate in the workspace must be named `tpt-nova-viz-*` (except the root facade).

## Upstream dependencies

`tpt-nova` (core runtime), `tpt-math` and `tpt-media`. Sources are still to be resolved; see Phase 0 in [TODO.md](TODO.md).

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or <https://www.apache.org/licenses/LICENSE-2.0>)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or <https://opensource.org/licenses/MIT>)

at your option.

### Dependency policy (differs from spec.txt)

`spec.txt` v0.1 states "MIT only" with Apache-2.0-only dependencies banned. This project is instead dual-licensed `MIT OR Apache-2.0`, and the dependency policy is relaxed accordingly:

- **Allowed:** MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, ISC, Zlib, BSL-1.0
- **Banned:** GPL, AGPL, LGPL, MPL, SSPL
- Video encoding: no linked ffmpeg bindings; MP4 export shells out to an external `ffmpeg` binary.

Enforced with `cargo-deny`.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
