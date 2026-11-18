# tpt-nova-viz Progress

License: `MIT OR Apache-2.0` · Owner: TPT Solutions · Spec: [spec.txt](spec.txt) (Draft v0.1)

> Deviations from spec.txt: dual license (spec says MIT only); Apache-2.0 deps allowed; ffmpeg stays an external process only.

## [ ] Phase 0: Project Setup
- [x] Read spec and clarify requirements.
- [x] Add `LICENSE-MIT` and `LICENSE-APACHE` (Copyright (c) 2026 TPT Solutions).
- [x] Add `README.md` with license and dependency-policy notes.
- [ ] `git init`, `.gitignore` (Rust), default branch, first commit.
- [ ] **Resolve upstream dependency sources** (crates.io name or git URL + version) for `tpt-nova`, `tpt-math`, `tpt-media`.
- [ ] Confirm `tpt-nova` version range matches manifest (`>=0.4.0,<0.6.0`).
- [ ] Decide handling of `tpt-nova-drivers` and `tpt-eve` (spec references them; not listed as deps).
- [ ] Create Cargo workspace (`resolver = "2"`, `license = "MIT OR Apache-2.0"`, shared `[workspace.package]`).
- [ ] Create 8 crates, all named per the rule: `tpt-nova-viz`, `-pointcloud`, `-cad`, `-measure`, `-annotate`, `-volume`, `-camera`, `-export`.
- [ ] Add CI check that rejects any crate not named `tpt-nova-viz[-*]`.
- [ ] Add `vectis-domain.toml` (domain `viz`, version `0.1.0`, nova `>=0.4.0,<0.6.0`).
- [ ] Add `schemas/components.nova.json` and `schemas/events.nova.json`.
- [ ] Add `drivers/` directory.
- [ ] Choose MSRV and Rust edition; add `rust-toolchain.toml`.
- [ ] `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`.

## [ ] Phase 0b: Licensing and Dependency Policy
- [ ] `deny.toml`: allow MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, ISC, Zlib, BSL-1.0.
- [ ] `deny.toml`: deny GPL-*, AGPL-*, LGPL-*, MPL-*, SSPL.
- [ ] `cargo-deny` runs in CI (licenses, bans, advisories, sources).
- [ ] Add `license = "MIT OR Apache-2.0"` to every crate manifest.
- [ ] SPDX header (`// SPDX-License-Identifier: MIT OR Apache-2.0`) on source files.
- [ ] Audit each third-party format crate (las, dicom, printpdf, image) for license compatibility.

## [ ] Phase 1: Point Cloud Foundation (`tpt-nova-viz-pointcloud`)
- [ ] `PointCloud`, `PointCloudSource`, `PointCloudFormat`, `PointChunk`, `ColorMode` components.
- [ ] `PointGenerator` trait (for generated sources).
- [ ] Basic LAS parser (MIT/Apache-compatible).
- [ ] LAZ, PTS, XYZ parsers.
- [ ] E57 parser.
- [ ] Out-of-core streaming (`pointcloud_stream_system`).
- [ ] Octree chunking / preprocessing (for datasets larger than RAM).
- [ ] LOD selection by screen-space error (`pointcloud_lod_system`).
- [ ] Instanced point-sprite rendering (`pointcloud_render_system`).
- [ ] Chunk unloading and GPU memory budget (`pointcloud_cleanup_system`).
- [ ] Frustum culling; occlusion culling.
- [ ] Seamless LOD transitions.
- [ ] Color mapping: uniform, by height, intensity, classification, RGB.
- [ ] Point size attenuation by distance.
- [ ] Drivers: `pointcloud_loader_driver`, `pointcloud_lod_driver` (quadtree/octree/k-d tree), `pointcloud_render_driver` (sprites/splatting/raycasting).
- [ ] Hot-swap between streaming and bulk loader drivers by dataset size.

## [ ] Phase 2: CAD Visualization (`tpt-nova-viz-cad`)
- [ ] `CadModel`, `CadSource`, `CadMesh`, `CadMaterial`, `CadMetadata`, `CadUnits`.
- [ ] OBJ parser.
- [ ] glTF parser.
- [ ] STL parser.
- [ ] Async parsing (`cad_parse_system`).
- [ ] PBR rendering (`cad_render_system`).
- [ ] Hierarchical assembly structure (parts, sub-assemblies).
- [ ] Part selection and isolation (`cad_select_system`).
- [ ] Exploded view animation (`cad_explode_system`).
- [ ] Cross-section cutting planes.
- [ ] Metadata extraction (author, units, properties).
- [ ] IFC parser (BIM).
- [ ] STEP parser (mesh-level; full B-rep tessellation deferred to v0.2).
- [ ] Drivers: `cad_parser_driver`, `cad_material_driver` (Phong/PBR), `cad_tessellation_driver`.

## [ ] Phase 3: Measurement Tools (`tpt-nova-viz-measure`)
- [ ] `Measurement`, `MeasurementKind`, `MeasurementUnit`, `MeasurementTool`.
- [ ] Distance calculation.
- [ ] Angle calculation (3-point and 2-line).
- [ ] Area (polygon) and volume (closed mesh).
- [ ] Radius and diameter.
- [ ] `f64` math throughout; unit conversion tests.
- [ ] Real-time update (`measurement_update_system`).
- [ ] Rendering of lines, arcs, labels (`measurement_render_system`).
- [ ] Mouse/touch point placement (`measurement_input_system`).
- [ ] Snap-to-surface.
- [ ] Measurement history and export.
- [ ] Drivers: `measurement_calc_driver` (Euclidean vs geodesic), `measurement_render_driver` (arrows/lines/dashed).

## [ ] Phase 4: Annotation System (`tpt-nova-viz-annotate`)
- [ ] `Annotation`, `AnnotationKind`, `AnnotationStyle`, `AnnotationLayer`.
- [ ] 3D text with billboarding.
- [ ] Arrow and callout rendering.
- [ ] Cloud and polyline markup.
- [ ] Depth-tested rendering (`annotation_render_system`).
- [ ] Create/edit/delete input (`annotation_input_system`).
- [ ] Layer visibility and locking (`annotation_layer_system`).
- [ ] Annotation locking to prevent accidental edits.
- [ ] Export annotations to JSON.
- [ ] Export annotations to XML.
- [ ] Drivers: `annotation_render_driver` (atlas/SDF/vector), `annotation_layout_driver`.

## [ ] Phase 5: Volumetric Rendering (`tpt-nova-viz-volume`)
- [ ] `VolumeData`, `VolumeDataSource`, `VolumeFormat`, `TransferFunction`.
- [ ] Raw (8/16-bit, float32) loader.
- [ ] NRRD loader.
- [ ] DICOM loader.
- [ ] 3D texture upload (`volume_upload_system`).
- [ ] Raycasting DVR with transfer function (`volume_render_system`).
- [ ] Transfer function UI/editing.
- [ ] Window/level adjustment.
- [ ] Multi-slice views (axial, coronal, sagittal).
- [ ] Clipping planes.
- [ ] Marching-cubes isosurface (`volume_isosurface_system`).
- [ ] Drivers: `volume_loader_driver`, `volume_render_driver`, `volume_transfer_driver`.

## [ ] Phase 6: Precision Camera (`tpt-nova-viz-camera`)
- [ ] `VizCamera`, `VizCameraMode`, `CameraConstraints`.
- [ ] Orbit, pan, zoom.
- [ ] Orthographic projection.
- [ ] Fly and walk modes.
- [ ] Sub-millimeter precision math (`f64`, floating-origin / camera-relative rendering for huge scenes).
- [ ] Input handling (`viz_camera_input_system`).
- [ ] Zoom-to-fit and frame-selection (`viz_camera_fit_system`).
- [ ] Constraints (distance, pitch, roll).
- [ ] Smooth damping.
- [ ] Drivers: `viz_camera_control_driver`, `viz_camera_projection_driver` (perspective/ortho/fisheye).

## [ ] Phase 7: Export System (`tpt-nova-viz-export`)
- [ ] `ExportJob`, `ExportFormat`, `ExportStatus`, `ExportSettings`.
- [ ] Framebuffer/render-pass capture (`export_capture_system`).
- [ ] PNG and JPEG export (via `tpt-media` or `image`).
- [ ] High-resolution tiled capture.
- [ ] Background export that does not block the UI.
- [ ] Progress reporting and cancellation (`export_progress_system`).
- [ ] PDF vector export.
- [ ] glTF, OBJ, STL scene export.
- [ ] MP4 video via external `ffmpeg` process (no linked dependency).
- [ ] Detect missing `ffmpeg` and report a clear error.
- [ ] Drivers: `export_encoder_driver`, `export_scene_driver`.

## [ ] Phase 8: Facade, Integration, Quality
- [ ] Root `tpt-nova-viz` facade re-exports all subcrates (feature flags per subsystem).
- [ ] Register components, systems and drivers with tpt-nova.
- [ ] Driver hot-swap integration test.
- [ ] Unit tests for each crate.
- [ ] Golden-file tests for parsers.
- [ ] Benchmarks (point cloud throughput, measurement accuracy).
- [ ] CI matrix: Linux, Windows, macOS; `fmt`, `clippy`, `test`, `deny`.
- [ ] API docs (`cargo doc`), per-crate READMEs, examples.

## [ ] Phase 9: Success Criteria (spec section 9)
- [ ] 10-billion-point LiDAR dataset loads and navigates at 30+ FPS on a mid-range GPU.
- [ ] STEP file parsed and rendered with correct materials and hierarchy.
- [ ] CAD distance measurement accurate to 0.01 mm.
- [ ] 3D annotation placed, edited and exported to JSON.
- [ ] DICOM CT scan rendered with interactive transfer function adjustment.
- [ ] Camera orbits, pans and zooms with sub-millimeter precision.
- [ ] High-resolution PNG export completes without blocking the UI.
- [ ] Dependency tree passes `cargo-deny` against the dual-license policy.

## Non-Goals for v0.1
- Photorealistic rendering.
- Real-time multi-user collaboration.
- Full STEP/IGES B-rep tessellation (v0.2).
- Native mobile (v0.1 targets desktop Linux/Windows/macOS).
- Proprietary CAD kernels (Parasolid, ACIS).

## Open Questions
- [ ] Upstream sources/versions for `tpt-nova`, `tpt-math`, `tpt-media`.
- [ ] Is a pure-Rust MP4 encoder worth investigating later to drop the ffmpeg runtime requirement?
- [ ] 10B-point target: what reference hardware counts as "mid-range GPU"?
- [ ] Spec's "Layer 5" naming vs. its 7 internal "Layers": rename internal ones to phases (done here).
