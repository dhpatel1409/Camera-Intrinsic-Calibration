# 📷 Camera Intrinsic Calibration via DLT



Estimates a camera's **intrinsic matrix K** from a set of checkerboard images using the **Direct Linear Transform (DLT)** method with least-squares minimisation via **SVD**.



## 🔭 Theory

### Camera Projection Model

A 3-D world point **X** = (X, Y, Z, 1)ᵀ projects to image point **x** = (u, v, 1)ᵀ via:

```
λ x = P X
```

where **P** is the **3 × 4 projection matrix**:

```
P = K [R | t]
```

| Symbol | Meaning |
|--------|---------|
| **K** | 3 × 3 intrinsic matrix |
| **R** | 3 × 3 rotation matrix (≈ I here) |
| **t** | 3 × 1 translation vector (≈ 0 here) |

### Intrinsic Matrix

Assuming **no skew** (θ = 90°):

```
    ┌ fx   0   cx ┐
K = │  0  fy   cy │
    └  0   0    1 ┘
```

| Parameter | Meaning |
|-----------|---------|
| `fx`, `fy` | Focal lengths (pixels) |
| `cx`, `cy` | Principal point (pixels) |

### DLT Pipeline

1. **Corner detection** — Harris corner detector on each checkerboard image  
2. **Coordinate mapping** — Map detected pixel corners to real-world (X, Y, Z) coordinates using known square size (25 mm)  
3. **Least-squares system** — Build overdetermined system **A p = 0** (2 equations per point per view)  
4. **SVD solve** — Find **p** = right singular vector of **A** corresponding to the smallest singular value  
5. **Extract K** — Decompose **P = K [I | 0]** → K = P[:, :3] (normalised, skew zeroed)  












## 📚 References

- Hartley & Zisserman, *Multiple View Geometry in Computer Vision*, 2nd ed.  
- Zhang, Z. (2000). *A Flexible New Technique for Camera Calibration*. IEEE TPAMI.  
- OpenCV Harris Corner Documentation: https://docs.opencv.org/

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.
