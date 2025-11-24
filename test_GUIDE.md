## GUIDE Test Report – Baoyi Lin

## 运行环境
- Apple M1 Max 
- Apple GPU 使用 Metal 框架 做加速，而 不支持 CUDA。因此，wanglabhkust/guide:v0.1 在 本设备 上 **GPU 加速无法使用，只能退回 CPU**。

<img width="280" height="499" alt="image" src="https://github.com/user-attachments/assets/549689b0-93e0-4449-b272-c5151a494254" />
<img width="699" height="229" alt="image" src="https://github.com/user-attachments/assets/da09f4f2-033f-48e8-b93f-c2e30c409824" />

## 遇到的问题/建议
1. GUIDE 可以增加 R package 版本，降低使用门槛。
2. **问题**：安装Docker后直接运行，Docker 内存不足， Docker 容器崩溃退出:```time="2025-11-14T13:41:47+08:00" level=error msg="error waiting for container: unexpected EOF"```。\
   **建议**：建议在`GUIDE Docker Testing Manual`教程最开始处，指导仅支持CPU的设备修改Docker Memory Limit，调大到至少12GB(默认Docker Memory Limit< 10 GB)。\
   *参考：一张片子（CGGA_P87.svs，～1G），运行时占用的内存峰值（RAM）～32GB, 允许最多用 10 个 CPU 核的情况下CPU 峰值占用率～90%。* \
   **解决步骤**：
	1.	打开 Docker Desktop
	2.	Settings → Resources
	3.	调整：
 	  ```
    Memory: 12 GB（越大越好）
    CPUs: 8 以上
    ```
<img width="1270" height="721" alt="image" src="https://github.com/user-attachments/assets/fc9be386-4c00-4332-bb6b-6a001c781066" />

3. **问题**：omics+一张片子（CGGA_2103.svs, ~1.5G）仅在CPU模式下运行时，程序到达 “保存 .h5 文件”之后就挂起，没有继续执行到 Starting Image Prediction（ResNet 模型推理阶段）。 \
遇到的error：
```
(base) baoyilin@dy149-115 ~ % docker run --shm-size 12G \                                
           -v /Users/baoyilin/Downloads/guide_test_data_2/:/home/guide/data \
           wanglabhkust/guide:v0.1 \
           /home/guide/data \
           simple \
           1  # FORCE_CPU
docker: invalid reference format

Run 'docker run --help' for more information
zsh: command not found: -v
(base) baoyilin@dy149-115 ~ % docker run --shm-size 12G \
  -v /Users/baoyilin/Downloads/guide_test_data_2/:/home/guide/data \
  wanglabhkust/guide:v0.1 \
  /home/guide/data \
  simple \
  1
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
Data path: /home/guide/data
Output level: simple
=== Using Images ===
=== Device Check ===
Force CPU mode (FORCE_CPU=1)
Selected device: cpu
Running in CPU mode
WSI files path: /home/guide/data/wsi
=== Starting Image Preprocessing ===
Found 1 files
Number of processes: 1
Number of training images: 1
Task #1: Process slide 0
Opening Slide #0: /home/guide/data/wsi/CGGA_2103.svs
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
Saving image to: /home/guide/data/mask/training_png/CGGA_2103.svs-32x-149504x94743-4672x2960.png
Done converting slide 0
Time elapsed: 0:00:06.687004
Applying filters to images (multiprocess)

Number of processes: 1
Number of training images: 1
Task #0: Process slide 0
Processing slide #0
RGB                  | Time: 0:00:00.332533  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.998859  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-001-rgb.png
Save Thumbnail       | Time: 0:00:00.036954  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-001-rgb.jpg
Filter Green Channel | Time: 0:00:00.014981  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.018634  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.700987  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-002-rgb-not-green.png
Save Thumbnail       | Time: 0:00:00.033153  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-002-rgb-not-green.jpg
Filter Grays         | Time: 0:00:00.034900  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.018907  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.714801  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-003-rgb-not-gray.png
Save Thumbnail       | Time: 0:00:00.032630  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-003-rgb-not-gray.jpg
Filter Red Pen       | Time: 0:00:00.188184  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.018786  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.957293  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-004-rgb-no-red-pen.png
Save Thumbnail       | Time: 0:00:00.033334  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-004-rgb-no-red-pen.jpg
Filter Green Pen     | Time: 0:00:00.314878  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.019837  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.967809  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-005-rgb-no-green-pen.png
Save Thumbnail       | Time: 0:00:00.033252  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-005-rgb-no-green-pen.jpg
Filter Blue Pen      | Time: 0:00:00.256740  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.020208  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.973138  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-006-rgb-no-blue-pen.png
Save Thumbnail       | Time: 0:00:00.032766  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-006-rgb-no-blue-pen.jpg
Mask RGB             | Time: 0:00:00.020127  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.715086  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-007-rgb-no-gray-no-green-no-pens.png
Save Thumbnail       | Time: 0:00:00.033027  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-007-rgb-no-gray-no-green-no-pens.jpg
Remove Small Objs    | Time: 0:00:00.167526  Type: bool    Shape: (2960, 4672)
Mask RGB             | Time: 0:00:00.019016  Type: uint8   Shape: (2960, 4672, 3)
Save Image           | Time: 0:00:00.775434  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-008-rgb-not-green-not-gray-no-pens-remove-small.png
Save Thumbnail       | Time: 0:00:00.033109  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-008-rgb-not-green-not-gray-no-pens-remove-small.jpg
Save Image           | Time: 0:00:00.763445  Name: /home/guide/data/mask/filter_png/CGGA_2103.svs-32x-149504x94743-4672x2960-filtered.png
Save Thumbnail       | Time: 0:00:00.034141  Name: /home/guide/data/mask/filter_thumbnail_jpg/CGGA_2103.svs-32x-149504x94743-4672x2960-filtered.jpg
Slide #000 processing time: 0:00:09.459493

Done filtering slide 0
Time to apply filters to all images (multiprocess): 0:00:09.485391

Input path:  /home/guide/data/wsi
Output path:  /home/guide/data/h5
Number of processes: 1
Number of training images: 1
Task #0: Process slide 0
  0%|          | 0/1 [00:00<?, ?it/s]Open CGGA_2103... Size  1410.8173723220825
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
Downsampling with factor  1
Given magnification 20.0, best level=1, best mag=20.0
Opening image  2025-11-24 09:23:24.165616
TIFFReadDirectoryCheckOrder: Warning, Invalid TIFF directory; tags are not sorted in ascending order.
TIFFFetchNormalTag: Warning, ASCII value for tag "Artist" contains null byte in value; value incorrectly truncated during reading due to implementation limitations.
JPEGFixupTagsSubsamplingSec: Warning, Auto-corrected former TIFF subsampling values [2,2] to match subsampling values inside JPEG compressed data [2,1].
Finished reading image  2025-11-24 09:29:56.490317
Finished reading high mag image
Small mask shape:  (2960, 4672)
High mag size:  (47616, 74752, 3)
Level dims:  ((149504, 94743), (74752, 47371), (37376, 23685), (18688, 11842), (9344, 5921), (4672, 2960), (2336, 1480), (1168, 740), (584, 370))
Mask rate:  0.21954955695075445
Start extracting features  2025-11-24 09:30:29.220512
Finished extracting features  2025-11-24 09:30:37.536516
Start staining normalization
100%|██████████| 10297/10297 [00:33<00:00, 308.69it/s]
Start saving as .h5 files  2025-11-24 09:31:10.908353]
(10297, 3, 256, 256)
```
   <img width="655" height="735" alt="image" src="https://github.com/user-attachments/assets/8b52987e-5108-425a-b824-6a559a14588d" />
   
   **原因**： Docker RAM(内存峰值)达到～62GB，接近限额，被程序 silent kill。\
   <img width="809" height="79" alt="image" src="https://github.com/user-attachments/assets/74179055-6a8b-435f-8acc-60312ad4a21a" />
   <img width="808" height="65" alt="image" src="https://github.com/user-attachments/assets/32ea9889-181a-489e-b170-7f8cc12c9822" />

   **解决办法**：


## File path
```plaintext
.
├── guide_test_data
    ├──wsi/
       └── CGGA_P87.csv
```
```plaintext
.
├── guide_test_data_2
	├── omics/
	│   ├── gene.csv
	│   ├── methyl.csv
	│   └── protein.csv
	└── wsi/
	    └── CGGA_2103.svs
```

## 运行结果
### 1. 一张片子（~1G）
运行时间10～12分钟

	•	WSI decode → 约 7 分钟
	•	Patch extraction → 秒级
	•	Normalization → 25 秒
	•	ResNet inference → 2 分钟
	•	Integration → 秒级
	
一张片子（CGGA_P87.svs，～1G），运行时占用的内存峰值（RAM）～32GB, 允许最多用 10 个 CPU 核的情况下CPU 峰值占用率～90%。

**Code**
```
(base) baoyilin@dy149-115 ~ % docker run --shm-size 12G \                                
           -v /Users/baoyilin/Downloads/guide_test_data/:/home/guide/data \
           wanglabhkust/guide:v0.1 \
           /home/guide/data \
           simple \
           1  # FORCE_CPU
```

**Ful report**
```
(base) baoyilin@dy149-115 ~ % docker run --shm-size 12G \
  -v /Users/baoyilin/Downloads/guide_test_data/:/home/guide/data \
  wanglabhkust/guide:v0.1 \
  /home/guide/data \
  simple \
  1
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
Data path: /home/guide/data
Output level: simple
=== Using Images ===
=== Device Check ===
Force CPU mode (FORCE_CPU=1)
Selected device: cpu
Running in CPU mode
WSI files path: /home/guide/data/wsi
=== Starting Image Preprocessing ===
Found 1 files
Number of processes: 1
Number of training images: 1
Task #1: Process slide 0
Opening Slide #0: /home/guide/data/wsi/CGGA_P87.svs
Saving image to: /home/guide/data/mask/training_png/CGGA_P87.svs-32x-77400x56523-2418x1766.png
Done converting slide 0
Time elapsed: 0:00:02.447820
Applying filters to images (multiprocess)

Number of processes: 1
Number of training images: 1
Task #0: Process slide 0
Processing slide #0
Done filtering slide 0
Time to apply filters to all images (multiprocess): 0:00:00.020823

Input path:  /home/guide/data/wsi
Output path:  /home/guide/data/h5
Number of processes: 1
Number of training images: 1
Task #0: Process slide 0
  0%|          | 0/1 [00:00<?, ?it/s]Open CGGA_P87... Size  945.9670896530151
Downsampling with factor  0
Given magnification 20.0, best level=0, best mag=40.0
Opening image  2025-11-14 06:09:36.415984
Finished reading image  2025-11-14 06:16:00.988796
Downsampling with factor 2
Finished reading high mag image
Small mask shape:  (1766, 2418)
High mag size:  (28416, 38912, 3)
Level dims:  ((77400, 56523), (19350, 14130), (4837, 3532), (2418, 1766))
Mask rate:  0.4777990524776743
Start extracting features  2025-11-14 06:16:42.523766
Finished extracting features  2025-11-14 06:16:46.169882
Start staining normalization
100%|██████████| 7729/7729 [00:25<00:00, 302.41it/s]
Start saving as .h5 files  2025-11-14 06:17:11.739459
(7729, 3, 256, 256)
Done
100%|██████████| 1/1 [08:04<00:00, 484.26s/it]
Done converting slide 0
Done!
=== Complete Preprocessing Image ===
=== Starting Image Prediction ===
1
Downloading: "https://download.pytorch.org/models/resnet18-f37072fd.pth" to /root/.cache/torch/hub/checkpoints/resnet18-f37072fd.pth
100%|██████████| 44.7M/44.7M [00:03<00:00, 14.3MB/s]
  0%|          | 0/1 [00:00<?, ?it/s][2025-11-14 06:17:52,407] - [main_test_wsi_h5.py file line:55] - INFO: wsi_name: CGGA_P87.h5
[2025-11-14 06:18:08,618] - [trainer.py file line:27] - INFO: Current path: /home/guide
[2025-11-14 06:18:08,699] - [trainer.py file line:51] - INFO: # para: 11177538
[2025-11-14 06:18:08,699] - [trainer.py file line:87] - INFO: load_model_path: GUIDE/pretrained.pth
cpu
[2025-11-14 06:18:08,738] - [trainer.py file line:194] - INFO: Epoch 0 evaluation on test...
[2025-11-14 06:18:08,739] - [trainer.py file line:202] - INFO: Total number of batches: 31
31it [02:03,  3.98s/it]
[2025-11-14 06:20:12,271] - [trainer.py file line:220] - INFO: [1943] positive patches out of [7729]
100%|██████████| 1/1 [02:19<00:00, 139.87s/it]
=== Complete Image Prediction ===
=== Starting Multi-Omics Integration ===
          P_IDHm_IME used_omics  IME_positive
CGGA_P87    0.532119      image          True

Results saved to: /home/guide/data/results/guide_results_simple.csv
=== Complete Multi-Omics Integration ===
=== Results saved to /home/guide/data/results/guide_results.csv ===
```
### 2. omics + 一张片子（～1.5G）
一张片子（CGGA_2103.svs，～1.5G），运行时占用的内存峰值（RAM）～62GB（Limit 62.68GiB）, 允许最多用 10 个 CPU 核的情况下CPU 峰值占用率～100%。

<img width="806" height="70" alt="image" src="https://github.com/user-attachments/assets/8636108c-f66b-44d2-8a1e-91599964dd0c" />
<img width="809" height="71" alt="image" src="https://github.com/user-attachments/assets/12b88e45-88fa-4d81-8690-7a8aa0e0a4d4" />
<img width="809" height="79" alt="image" src="https://github.com/user-attachments/assets/74179055-6a8b-435f-8acc-60312ad4a21a" />
<img width="808" height="65" alt="image" src="https://github.com/user-attachments/assets/32ea9889-181a-489e-b170-7f8cc12c9822" />

**Code**
```
(base) baoyilin@dy149-115 ~ % docker run --shm-size 12G \                                
           -v /Users/baoyilin/Downloads/guide_test_data_2/:/home/guide/data \
           wanglabhkust/guide:v0.1 \
           /home/guide/data \
           simple \
           1  # FORCE_CPU
```

**Full Report**
```

```

 
