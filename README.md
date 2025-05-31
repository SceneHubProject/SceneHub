# SceneHub

## Dataset Access

A partial version of the SceneHub dataset is available for public download:

**📦 Download link**: [SceneHubData](https://bit.ly/SceneHubData)

To ensure ease of access, we provide:
- **100 RGB-D frames** per scene (instead of the full 1000+)
- **Example geometry outputs** (1 frame per scene) including Gaussian Splatting, mesh, and point cloud

This partial set is sufficient for prototyping and evaluating pipeline compatibility.

⚠️ The **full dataset**, including all RGB-D frames, will be made available soon once long-term hosting is arranged. Stay tuned!

---

## Datset structure
📌 **Note**: 
Scene labels differ slightly from the paper for clarity.(`lab area → arena`, `factory → mill19`).  
The directory structure here differs slightly from the original layout presented in the paper, for structural simplicity:


```bash
MM_release/
├── camera_pose/                # camera pose metadata
├── geometry/                   # 3D reconstruction outputs
├── photogrammetry/             # high-res background meshes
├── rgbd_data/                  # raw RGB-D frames
└── dataset_layout.txt          # detailed layout of the dataset structure
```

### RGBD data
```bash
dataset-paper/rgbd_data/
└── <scene>/                      # scene ∈ {arena, couch, kitchen, mill19, whiteboard}
    └── <scene>_scene<id>_100/    # id ∈ {0,1,2,…}
        └── rgbd/
            └── cam<cam_id>/      # cam_id ∈ {0,1,2,3}
                ├── rgb/          # color frames (.png)
                └── trans_depth/  # aligned depth maps (.png)
```

### Camera Pose
```bash
camera_pose/
├── cam_views/                    # per-scene view files ∈ {original, shifted, interpolated, random}
│       └── <scene>/              # scene ∈ {arena, couch, kitchen, mill19, whiteboard}
│               ├── <scene>_original.npy
│               ├── <scene>_shifted.npy
│               ├── <scene>_interpolated.npy
│               └── <scene>_random_extrinsics_seed42_sample50.npy
├── extrinsics/                   # camera extrinsic matrices (world to camera)
│       └── extrinsics_<scene>.npy                     
└── intrinsics/                   # camera factory intrinsics, optimal intrinsics parameters
    └── <scene>_config.json                     
```

### Geometry Output
```bash
geometry/
└── <scene>/                          # scene ∈ {arena, couch, kitchen, mill19, 
        └── <scene>_scene<id>_100/    # id ∈ {0,1,2,…}
            ├── 3dgs/                 # Gaussian splatting outputs
            │   └── point_cloud/
            │       └── iteration_30000/point_cloud_<frame_idx>.ply 
            ├── mesh/                 # textured meshes
            │   ├── <frame_idx>.obj
            │   ├── <frame_idx>.mtl
            │   └── <frame_idx>.png        
            └── ptcl/                 # raw point clouds
                 <frame_idx>.pcl
```

### Photogrammetry
```bash
photogrammetry/
└── <scene>/                      # scene-specific photogrammetry
    ├── <scene>.obj               # mesh file
    ├── <scene>.mtl               # mesh file
    └── <scene>.png               # mesh file
```
