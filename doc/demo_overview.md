OpenPose Demo - Overview
====================================

Forget about the OpenPose library code, just compile the library and use the demo `./build/examples/openpose/openpose.bin`.

In order to learn how to use it, run `./build/examples/openpose/openpose.bin --help` in your bash and read all the available flags (check only the flags for `examples/openpose/openpose.cpp` itself, i.e. the section `Flags from examples/openpose/openpose.cpp:`). We detail some of them in the following sections.



## All Flags
Each flag is divided into flag name, default value, and description.

1. Debugging
- DEFINE_int32(logging_level,             3,              "The logging level. Integer in the range [0, 255]. 0 will output any log() message, while 255 will not output any. Current OpenPose library messages are in the range 0-4: 1 for low priority messages and 4 for important ones.");
2. Producer
- DEFINE_int32(camera,                    0,              "The camera index for cv::VideoCapture. Integer in the range [0, 9].");
- DEFINE_string(camera_resolution,        "1280x720",     "Size of the camera frames to ask for.");
- DEFINE_string(video,                    "",             "Use a video file instead of the camera. Use `examples/media/video.avi` for our default example video.");
- DEFINE_string(image_dir,                "",             "Process a directory of images. Use `examples/media/` for our default example folder with 20 images.");
- DEFINE_uint64(frame_first,              0,              "Start on desired frame number.");
- DEFINE_uint64(frame_last,               -1,             "Finish on desired frame number. Select -1 to disable this option.");
- DEFINE_bool(frame_flip,                 false,          "Flip/mirror each frame (e.g. for real time webcam demonstrations).");
- DEFINE_int32(frame_rotate,              0,              "Rotate each frame, 4 possible values: 0, 90, 180, 270.");
- DEFINE_bool(frames_repeat,              false,          "Repeat frames when finished.");
3. OpenPose
- DEFINE_string(model_folder,             "models/",      "Folder where the pose models (COCO and MPI) are located.");
- DEFINE_string(resolution,               "1280x720",     "The image resolution (display and output). Use \"-1x-1\" to force the program to use the default images resolution.");
- DEFINE_int32(num_gpu,                   -1,             "The number of GPU devices to use. If negative, it will use all the available GPUs in your machine.");
- DEFINE_int32(num_gpu_start,             0,              "GPU device start number.");
- DEFINE_int32(keypoint_scale,            0,              "Scaling of the (x,y) coordinates of the final pose data array, i.e. the scale of the (x,y) coordinates that will be saved with the `write_keypoint` & `write_keypoint_json` flags. Select `0` to scale it to the original source resolution, `1`to scale it to the net output size (set with `net_resolution`), `2` to scale it to the final output size (set with `resolution`), `3` to scale it in the range [0,1], and 4 for range [-1,1]. Non related with `num_scales` and `scale_gap`.");
4. OpenPose Body Pose
- DEFINE_string(model_pose,               "COCO",         "Model to be used (e.g. COCO, MPI, MPI_4_layers).");
- DEFINE_string(net_resolution,           "656x368",      "Multiples of 16. If it is increased, the accuracy usually increases. If it is decreased, the speed increases.");
- DEFINE_int32(num_scales,                1,              "Number of scales to average.");
- DEFINE_double(scale_gap,                0.3,            "Scale gap between scales. No effect unless num_scales>1. Initial scale is always 1. If you want to change the initial scale, you actually want to multiply the `net_resolution` by your desired initial scale.");
- DEFINE_bool(heatmaps_add_parts,         false,          "If true, it will add the body part heatmaps to the final op::Datum::poseHeatMaps array (program speed will decrease). Not required for our library, enable it only if you intend to process this information later. If more than one `add_heatmaps_X` flag is enabled, it will place then in sequential memory order: body parts + bkg + PAFs. It will follow the order on POSE_BODY_PART_MAPPING in `include/openpose/pose/poseParameters.hpp`.");
- DEFINE_bool(heatmaps_add_bkg,           false,          "Same functionality as `add_heatmaps_parts`, but adding the heatmap corresponding to background.");
- DEFINE_bool(heatmaps_add_PAFs,          false,          "Same functionality as `add_heatmaps_parts`, but adding the PAFs.");
5. OpenPose Face
- DEFINE_bool(face,                       false,          "Enables face keypoint detection. It will share some parameters from the body pose, e.g. `model_folder`.");
- DEFINE_string(face_net_resolution,      "368x368",      "Multiples of 16. Analogous to `net_resolution` but applied to the face keypoint detector. 320x320 usually works fine while giving a substantial speed up when multiple faces on the image.");
6. OpenPose Hand
7. OpenPose Rendering
- DEFINE_int32(part_to_show,              0,              "Part to show from the start.");
- DEFINE_bool(disable_blending,           false,          "If blending is enabled, it will merge the results with the original frame. If disabled, it will only display the results.");
8. OpenPose Rendering Pose
- DEFINE_bool(no_render_pose,             false,          "If false, it will fill both `outputData` and `cvOutputData` with the original image + desired part to be shown. If true, it will leave them empty.");
- DEFINE_double(alpha_pose,               0.6,            "Blending factor (range 0-1) for the body part rendering. 1 will show it completely, 0 will hide it.");
- DEFINE_double(alpha_heatmap,            0.7,            "Blending factor (range 0-1) between heatmap and original frame. 1 will only show the heatmap, 0 will only show the frame.");
9. OpenPose Rendering Face
- DEFINE_bool(no_render_face,             false,          "Analogous to `no_render_pose` but applied to the face keypoints and heat maps.");
- DEFINE_double(alpha_face,               0.6,            "Blending factor (range 0-1) for the body part rendering. 1 will show it completely, 0 will hide it.");
- DEFINE_double(alpha_heatmap_face,       0.7,            "Blending factor (range 0-1) between heatmap and original frame. 1 will only show the heatmap, 0 will only show the frame.");
10. Display
- DEFINE_bool(fullscreen,                 false,          "Run in full-screen mode (press f during runtime to toggle).");
- DEFINE_bool(process_real_time,          false,          "Enable to keep the original source frame rate (e.g. for video). If the processing time is too long, it will skip frames. If it is too fast, it will slow it down.");
- DEFINE_bool(no_gui_verbose,             false,          "Do not write text on output images on GUI (e.g. number of current frame and people). It does not affect the pose rendering.");
- DEFINE_bool(no_display,                 false,          "Do not open a display window.");
11. Result Saving
- DEFINE_string(write_images,             "",             "Directory to write rendered frames in `write_images_format` image format.");
- DEFINE_string(write_images_format,      "png",          "File extension and format for `write_images`, e.g. png, jpg or bmp. Check the OpenCV function cv::imwrite for all compatible extensions.");
- DEFINE_string(write_video,              "",             "Full file path to write rendered frames in motion JPEG video format. It might fail if the final path does not finish in `.avi`. It internally uses cv::VideoWriter.");
- DEFINE_string(write_keypoint,           "",             "Directory to write the people body pose keypoint data. Desired format on `write_keypoint_format`.");
- DEFINE_string(write_keypoint_format,    "yml",          "File extension and format for `write_keypoint`: json, xml, yaml and yml. Json not available for OpenCV < 3.0, use `write_keypoint_json` instead.");
- DEFINE_string(write_keypoint_json,      "",             "Directory to write people pose data with *.json format, compatible with any OpenCV version.");
- DEFINE_string(write_coco_json,          "",             "Full file path to write people pose data with *.json COCO validation format.");
- DEFINE_string(write_heatmaps,           "",             "Directory to write heatmaps with *.png format. At least 1 `add_heatmaps_X` flag must be enabled.");
- DEFINE_string(write_heatmaps_format,    "png",          "File extension and format for `write_heatmaps`, analogous to `write_images_format`. Recommended `png` or any compressed and lossless format.");

## Multiple Scales
Running at multiple scales might drastically slow down the speed, but it will increase the accuracy. Given the CNN input size (set with `net_resolution`), `num_scales` and `scale_gap` configure the number of scales to use and the gap between them, respectively. For instance, `--num_scales 3 --scale_gap 0.15` means using 3 scales at resolution: (1), (1-0.15) and (1-2*0.15) times the `net_resolution`.

## Heat Maps Storing
The following command will save all the body part heat maps, background heat map and Part Affinity Fields (PAFs) in the folder `output_heatmaps_folder`. It will save them on PNG format. Instead of individually saving each of the 67 heatmaps (18 body parts + background + 2 x 19 PAFs) individually, the library concatenate them vertically into a huge (width x #heatmaps) x (height) matrix. The PAFs channels are multiplied by 2 because there is one heatmpa for the x-coordinates and one for the y-coordinates. The order is body parts + bkg + PAFs. It will follow the sequence on POSE_BODY_PART_MAPPING in [include/openpose/pose/poseParameters.hpp](../include/openpose/pose/poseParameters.hpp).
```
./build/examples/openpose/openpose.bin --video examples/media/video.avi --heatmaps_add_parts --heatmaps_add_bkg --heatmaps_add_PAFs --write_heatmaps output_heatmaps_folder/
```



## Some Important Configuration Flags
Please, in order to check all the real time pose demo options and their details, run `./build/examples/openpose/openpose.bin --help`. We describe here some of the most important ones.

- `--face`: If enabled, it will also detect the faces on the image. Note that this will considerable slow down the performance and increse the required GPU memory. In addition, the greater number of people on the image, the slower OpenPose will be.
- `--video input.mp4`: Input video. If omitted, it will use the webcam.
- `--camera 3`: Choose webcam number (default: 0). If `--camera`, `--image_dir` and `--write_video` are omitted, it is equivalent to use `--camera 0`.
- `--image_dir path_to_images/`: Run on all images (jpg, png, bmp, etc.) in `path_to_images/`. You can test the program with the image directory `examples/media/`.
- `--write_video path.avi`: Render images with this prefix: `path.avi`. You can test the program with the example video `examples/media/video.avi`.
- `--write_images folder_path`: Render images on the folder `folder_path`.
- `--write_keypoint path/`: Output JSON, XML or YML files with the people pose data on the `path/` folder.
- `--process_real_time`: It might skip frames in order to keep the final output displaying frames on real time.
- `--disable_blending`: If selected, it will only render the pose skeleton or desired heat maps, while blocking the original background. Also related: `part_to_show`, `alpha_pose`, and `alpha_pose`.
- `--part_to_show`: Select the prediction channel to visualize (default: 0). 0 to visualize all the body parts, 1-18 for each body part heat map, 19 for the background heat map, 20 for all the body part heat maps together, 21 for all the PAFs, 22-69 for each body part pair PAF.
- `--no_display`: Display window not opened. Useful if there is no X server and/or to slightly speed up the processing if visual output is not required.
- `--num_gpu 2 --num_gpu_start 0`: Parallelize over this number of GPUs starting by the desired device id. Default is 1 and 0, respectively.
- `--num_scales 3 --scale_gap 0.15`: Use 3 scales, 1, (1-0.15), (1-0.15*2). Default is one scale. If you want to change the initial scale, you actually want to multiply your desired initial scale by the `net_resolution`.
- `--net_resolution 656x368 --resolution 1280x720`: For HD images and video (default values).
- `--net_resolution 496x368 --resolution 640x480`: For VGA images and video.
- `--model_pose MPI`: It will use MPI (15 body keypoints). Default: COCO (18 body keypoints). MPI is slightly faster. The variation `MPI_4_layers` sacrifies accuracy in order to further increase speed.
- `--logging_level 3`: Logging messages threshold, range [0,255]: 0 will output any message & 255 will output none. Current messages in the range [1-4], 1 for low priority messages and 4 for important ones.



## Rendering Face without Pose
```
./build/examples/openpose/openpose.bin --face --no_render_pose
```



## Example
The following example runs the video `vid.mp4`, renders image frames on `output/result.avi`, and outputs JSON files as `output/%12d.json`, parallelizing over 2 GPUs:
```
./build/examples/openpose/openpose.bin --video examples/media/video.avi --num_gpu 2 --write_video output/result.avi --write_json output/
```
