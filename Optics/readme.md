# OpenOCT Spectrometer Optical Design

This directory contains the optical design reference files for the OpenOCT
Spectro-800 system. The design is documented using a Zemax prescription-data
export and a STEP model so that the optical layout and mechanical envelope can
be reviewed without requiring a particular Zemax release.

## Repository contents

| File | Description |
| :--- | :--- |
| `Zemax_Prescription_Data.md` | Reformatted export of the Zemax System/Prescription Data. It contains the system settings, wavelength and field definitions, surface sequence, materials, spacings, and selected first-order results. |
| `OpenOCT_spec_3D.STP` | STEP representation of the spectrometer design for CAD inspection and mechanical integration. |

## Design overview

The prescription describes a sequential, on-axis optical system with a single
design wavelength of 0.840 um and one on-axis field. The optical path contains
three functional sections:

1. **Input objective:** a compact refractive group using N-SF57 and N-SSK2,
	followed by the system stop.
2. **Spectral section:** a fused-silica substrate assembly containing a
	diffractive grating surface. The grating is represented by the `DGRATING`
	surface in the prescription.
3. **Relay and image-forming optics:** a long free-space section followed by a
	multi-element relay using SFL6, LAKN22, and silica elements, ending at the
	image surface.

The prescription uses millimeters for lens units. The object-space numerical
aperture is 0.13, and the system aperture stop is surface 6, immediately before
the grating assembly.

## Key prescription values

| Parameter | Value |
| :--- | :--- |
| Number of surfaces | 21, including object, stop, and image surfaces |
| Primary wavelength | 0.840 um |
| Field definition | One field, 0.0 deg, weight 1.0 |
| Object-space NA | 0.13 |
| Image-space NA | 0.07215254 |
| Effective focal length | 64.70061 mm |
| Image-space F/# | 2.721626 |
| Working F/# | 7.002377 |
| Entrance pupil diameter | 23.77278 mm |
| Exit pupil diameter | 27.54368 mm |
| Total track | 251.4813 mm |
| Stop radius | 7.903976 mm |

The complete surface-by-surface data, including radii, thicknesses, glass
types, clear diameters, and component comments, is maintained in
[`Zemax_Prescription_Data.md`](Zemax_Prescription_Data.md).

## Optical sequence

The following is a functional reading of the exported surface sequence. Exact
surface locations and signs should be taken from the prescription table.

| Surfaces | Function | Notable data |
| :--- | :--- | :--- |
| OBJ to 4 | Input objective | N-SF57 and N-SSK2; clear diameters approximately 20.25 to 22.25 mm |
| 5 to STO | Stop and coordinate transition | Surface 6 is the system stop |
| 7 to 11 | Grating assembly | Fused silica, two thin coded layers, and one `DGRATING` surface |
| 12 | Coordinate transition and spacing | 102 mm nominal following the grating section |
| 13 to 18 | Relay group | SFL6 and LAKN22 elements with 50.8 mm mechanical diameters |
| 19 to IMA | Final imaging group | Silica and LC1582 element; 3.553457 mm image clear diameter |

## Zemax file availability

The native Zemax project file (`.ZMX`/`.ZEMAX`) is intentionally not included.
Zemax project files can be affected by software-version and catalog
compatibility differences, which may prevent another user from opening the
file reliably. Instead, this repository includes the version-neutral
prescription-data export in Markdown form. It preserves the numerical
prescription needed for review and reconstruction while avoiding a forced
Zemax version dependency.

The export does not replace every part of a native Zemax project. In
particular, users should verify grating-specific settings, coating data,
aperture definitions, tolerances, optimization operands, and catalog versions
in the originating Zemax project before using the design for final performance
claims or fabrication.

## Reconstructing or reviewing the design

1. Start with [`Zemax_Prescription_Data.md`](Zemax_Prescription_Data.md) and
	enter the system units, wavelength, field, aperture, and surface sequence
	into the target Zemax release.
2. Confirm the glass catalogs and material names available in that release.
3. Re-enter and verify the `DGRATING` surface parameters from the source design;
	the prescription summary identifies the surface but does not list all
	grating parameters.
4. Use [`OpenOCT_spec_3D.STP`](OpenOCT_spec_3D.STP) to review the physical
	arrangement and mechanical diameters.
5. Re-run the optical analyses in the target Zemax version before treating the
	reconstructed model as equivalent to the source project.

