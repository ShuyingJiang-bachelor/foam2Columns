# foam2Columns

[![OpenFOAM version](https://img.shields.io/badge/OpenFOAM-7-brightgreen)](https://github.com/OpenFOAM/OpenFOAM-7)
[![OpenFOAM version](https://img.shields.io/badge/OpenFOAM-8-brightgreen)](https://github.com/OpenFOAM/OpenFOAM-8)

## Original Version

It supports any number of fields and transforms them to this format:

```
L1: x y z var1 var2 var3_x var3_y var3_z ...
```

Scalar and vector fields examples:

```c++
foam2Columns -fields "(p T)"
foam2Columns -vectorFields "(U)"
foam2Columns -fields "(p T)" -vectorFields "(U)"
```

Results are saved in `$FOAM_CASE/postProcessing/foam2Columns/$time/Eulerian_*`.

---

## Extended Version

This modified version additionally supports **Lagrangian fields** (both scalar and vector), making it easier to post-process particle data.

### Key Features

- ✅ Eulerian fields (same as original)  
- ✅ Lagrangian fields (newly added)  
  - Scalar: `-lagrangianFields "(d T)"`  
  - Vector: `-lagrangianFields "(u)"`  
  - Mixed: `-lagrangianFields "(d T u)"`  

Output format for Lagrangian fields:

```
x y z origId origProc field1 field2_x field2_y field2_z ...
```

### Example Usage

```bash
foam2columns -vectorFields "(U)"
foam2columns -lagrangianFields "(d T)"
foam2columns -lagrangianFields "(u)"
foam2columns -lagrangianFields "(d T u)"
```

### Output

Results are written under:

```
postProcessing/foam2Columns/<time>/
```

Example file naming:
- `Eulerian_p_U`
- `Lagrangian_parcel_d_T_u`

### Notes

- Each vector field is expanded into three columns (`_x`, `_y`, `_z`).  
- Missing fields at a given time step are skipped.  
- Tested with OpenFOAM v7.

**Modifications by Yongnan Liu (1565510924@qq.com), 2025.08.27.**
