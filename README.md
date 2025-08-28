# foam2Columns

[![OpenFOAM version](https://img.shields.io/badge/OpenFOAM-7-brightgreen)](https://github.com/OpenFOAM/OpenFOAM-7)
[![OpenFOAM version](https://img.shields.io/badge/OpenFOAM-8-brightgreen)](https://github.com/OpenFOAM/OpenFOAM-8)

## Usage

It supports any number of fields and transforms them to this format:
```
L1: x y z var1 var2 var3_x var3_y var3_z ...
L2: x y z var1 var2 var3_x var3_y var3_z ...
.
.
.
Ln: x y z var1 var2 var3_x var3_y var3_z ...
```
where `n` is the cell number, and `var1(p)`, `var2(T)` `var3(U)`are the input variables:

```c++
foam2Columns -fields "(p T)"
```

Yes, it supports volVectorField:
```c++
foam2Columns -vectorFields "(U)"
```

Or together:
```c++
foam2Columns -fields "(p T)" -vectorFields "(U)"
```

Thanks for ZmengXu.
With his help, it supports lagrangian fields:

```c++
foam2Columns -lagrangianFields "(d T)"
```

Or together:
```c++
foam2Columns -fields "(p T)" -vectorFields "(U)" -lagrangianFields "(d T)"
```

The results are save in `$FOAM_CASE/postProcessing/foam2Columns/$time/Eulerian_*`, and `$FOAM_CASE/postProcessing/foam2Columns/$time/Lagrangian_*` for lagrangian fields.



# foam2columns (extended version)

This repository provides an extended version of the **foam2columns** utility for OpenFOAM.  
The original tool was capable of extracting **Eulerian scalar fields** and **Eulerian vector fields** into a tabular (columns) format.  

This modified version additionally supports **Lagrangian fields** (both scalar and vector), making it easier to post-process particle data from OpenFOAM.

---

## Key Features

- ✅ **Eulerian fields**  
  - Scalar fields via `-fields "(p T)"`  
  - Vector fields via `-vectorFields "(U)"`

- ✅ **Lagrangian fields** (newly added)  
  - Scalar fields via `-lagrangianFields "(d T)"`  
  - Vector fields via `-lagrangianFields "(u)"`  
  - Mixed scalar and vector fields via `-lagrangianFields "(d T u)"`

- Output format for Lagrangian fields includes particle information:  
```
 x y z origId origProc field1 field2_x field2_y field2_z ...
```
---

  ## Example Usage

  Extract Eulerian vector field `U`:
  ```bash
  foam2columns -vectorFields "(U)"
  ```

  Extract Lagrangian scalar fields `d` and `T`:
  ```bash
  foam2columns -lagrangianFields "(d T)"
  ```

  Extract Lagrangian vector field `u`:
  ```bash
  foam2columns -lagrangianFields "(u)"
  ```

  Extract Lagrangian fields with both scalars and vectors:
  ```bash
  foam2columns -lagrangianFields "(d T u)"
  ```

---

  ## Output

  Results are written under:

  ```
  postProcessing/foam2Columns/<time>/
  ```

  Example file naming:
  - `Eulerian_p_U`
  - `Lagrangian_parcel_d_T_u`

---

  ## Notes

  - Currently supports only scalar and vector Lagrangian fields.
  - Each vector field is expanded into three columns (`_x`, `_y`, `_z`).
  - If fields are missing for a given time step, the tool skips processing for that time.
  - Tested with **OpenFOAM v7**.

This extended version adds Lagrangian scalar/vector field support. Modifications by Yongnan Liu (1565510924@qq.com), 2025.08.27.