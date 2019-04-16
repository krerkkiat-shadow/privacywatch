# How many different ways are there to write image or video files to hard disks?

* [`cv::imwrite()`](https://docs.opencv.org/3.0-beta/modules/imgcodecs/doc/reading_and_writing_images.html)
* [`ofstream`](http://www.cplusplus.com/reference/fstream/ofstream/)
* [`cv::imencode()`](https://docs.opencv.org/3.0-beta/modules/imgcodecs/doc/reading_and_writing_images.html)
* [`cyber::Writer write()`](https://github.com/ApolloAuto/apollo/blob/r3.5.0/cyber/node/writer.h)
* [`fprintf()`](http://www.cplusplus.com/reference/cstdio/fprintf/)

(We believe that if the program stores content such as images and texts, the program may be suspected of revealing privacy. cv::imwrite() is the code provided by the OpenCv library to store images into a file，cv::imencode() is the code provided by the OpenCv library to store images into memory buffer.ofstream and fprintf is the code provided by the OpenCv library to store texts into file.)

# About FLAGS

* https://github.com/drchangliu/vital/blob/master/notes/perception_checking.md

 # Search of "cv::imwrite()" #

 `cv::imwrite()` ()

Saves an image to a specified file.


| File (.cc)     | Line | Function Name | Usage | Flags involved | Potential for Privacy Leak |
| ----------- | ----------- |----------- |----------- |----------- |----------- |
| [visualization_engine.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc#L589) | 589-679 |GenerateMutiResolutionImages |Generate Multi Resolution Images | flag set as false, depends on apollo::common::util::PathExists(ss) -> Check if the directory specified by directory_path exists and is indeed a directory. | depends on what is in "%s/%08d/%08d_%d.png", the call of the function go back to the init of this file at the end, this function will be called every time when the file is called|
| [camera_common_io_util.h](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/test/camera_common_io_util.h#L30) | 30-37 | save_image | Save the image | No flag in the file | Not use in the file, depends on path, not find in the program |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L40) | 40-70 |void show_detect_point_set(const cv::Mat& image, const std::vector<std::vector<LanePointInfo> >& detect_laneline_point_set, const std::string& save_path) | show the point set | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#188) FLAGS_lane_line_debug, not find the initial value for the flag | only use cv::circle(draw_mat, draw_point, draw_size, color, 4), circle function will not destroy the image, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#197) |
 | [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L71) | 71-87 |show_all_infer_point_set | show the infer point set | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#188) FLAGS_lane_line_debug | only use cv::circle function, circle function will not destroy the image, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#193) |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L88) | 88-164 | show_lane_lines | output the lane line | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#209) FLAGS_lane_line_debug | use cv::circle, putText function, these two function is used to show the line in the image, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#212) |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L165) | 165-216 | show_lane_ccs | output the lane ccs | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#203) FLAGS_lane_cc_debug | | only use cv::circle function, circle function will not destroy the image, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#206) |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L337) | 337-352 | show_detect_point_set(const cv::Mat& image, const std::vector<base::Point2DF>& img_laneline_point_set, const std::string& save_path) | show the detect point | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#188) FLAGS_lane_line_debug | not call in this file, depends on the file that calls this function, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#197) |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L354) | 354-386 | show_neighbor_point_set | show the neighbor point | No flag in the file |not call in this file, depends on the file that calls this function; only use cv:circle, not find in the program |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L388) | 388-408 | void show_detect_point_set(const cv::Mat& image, const std::vector<base::Point2DF>& img_laneline_point_set, const std::vector<float>& point_score_vec, const std::string& save_path) | output the detect point set | No flag in the file, find flag in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#188) FLAGS_lane_line_debug |not call in this file, the function is used in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#197); use cv:circle, cv:putText |
| [obstacle_detection.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/obstacle_detection/obstacle_detection.cc#L342) | 342-345 | In the main function | output the detect obstacle image | if (FLAGS_vis_dir != "") not define in this file | the cv::write function use in the main part, the potential for privacy leak depends on the value of flag |
 | [offline_obstacle_pipeline.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/offline/offline_obstacle_pipeline.cc#L50) | 50-57 | save_image | save distortion images | if (FLAGS_do_undistortion && (FLAGS_undistortion_save_dir != "") && apollo::common::util::PathExists(save_dir)) | Both flags do not set in the file, not find in the program |
| [visualizer.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/offline/visualizer.cc#L146) | 146-191 | ShowResult | show the result of visualizer | if (frame.timestamp - last_timestamp_ > 0.02)   last_timestamp_ = 0; In Init | Depends on the timestamp of the frame, the function is used in [offline_obstacle_pipeline.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/offline/offline_obstacle_pipeline.cc#270), the frame.timestamp is also define in this file |


 # Search of "ofstream" #

 `ofstream` ()

 Output stream class to operate on files.

| File (.cc)     | Line | Function Name | Usage | Flags involved | Potential for Privacy Leak |
| ----------- | ----------- |----------- |----------- |----------- |----------- |
| [calibration.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/drivers/velodyne/parser/calibration.cc#L224) | 224-230 |write(const std::string& calibration_file) |Uses ofstream to output calibration file |No flag in the file|not called in this file, depends on the file that calls this function; no changed file in the function |
| [compare_poses.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/localization/msf/local_tool/data_extraction/compare_poses.cc#L249) | 249-256 |  std::ofstream file(compare_file.c_str()); |Compare pose and output the result | In the main function, no flags | output the idx, timestamp, x_diff, y_diff, roll_diff, pitch_diff, and yaw_diff of vec; Does not seem to pose any threat to privacy |
| [debug_info.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/app/debug_info.cc#L44) | 44-63 | WriteCamera2World | output the pose | No flag, find flag in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc#429) if (perception_param_.has_debug_param()) {if (perception_param_.debug_param().has_camera2world_out_file()) { |not call in this file, is called in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc#429) ; not change frame in the function |
| [debug_info.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/app/debug_info.cc#L64) | 64-101 | WriteTracking | output the tracking object | No flag, find flag in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc#433) if (perception_param_.debug_param().has_track_out_file()) |not call in this file, is called in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc#434) ; not change frame in the function; output the information of the truck such as truck id |
| [debug_info.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/app/debug_info.cc#L103) | 103-188 | WriteDetections | output the all the detections( use in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc)) | No flag |not call in this file, use in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc); output the information of detection such as left turn vision, right turn vision; might leak privacy |
| [debug_info.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/app/debug_info.cc#L189) | 189-223 | WriteDetections(Frame) | output the all the detection frame | No flag |not call in this file, ( use in [obstacle_camera_perception.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/app/obstacle_camera_perception.cc); output the information of detection such as frame id, detected object |
| [debug_info.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/app/debug_info.cc#L327) | 327-398 | WriteFusionTracking | output the tracking result | No flag |not call in this file, depends on the file that calls this function; output the information depends on the camera name :front_12mm/front_6mm, not find in the program |
| [util.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/inference/utils/util.cc#L40) | 40-51 | write_result | output the result of util | No flag |not call in this file, depends on the file that calls this function, used in 1.[yolo_sample.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/inference/tools/yolo_sample.cc#96) 2. [denseline_sample.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/inference/tools/denseline_sample.cc#146) 3.[lane_sample.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/inference/tools/lane_sample.cc#135) |
| [entropy_calibrator.h](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/inference/tensorrt/entropy_calibrator.h#L106) | 106-111 | writeCalibrationCache | write the result of Calibration Cache | No flag |not call in this file, depends on the file that calls this function, not find in the program|
| [perception.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/lidar/tools/offline_lidar_obstacle_perception.cc#L208) | 208-306 | Write Objects For New Benchmark | Write Objects output(Frame ID, object, object ID, etc.) For New Benchmark | No flag | call by the run() function in this file, output all the information about the object |

 # Search of "cyber::Writer write()" #

 `write()` ()
 (Found in [write.h](https://github.com/ApolloAuto/apollo/blob/r3.5.0/cyber/node/writer.h) -> Transmit function in [transmitter.h](https://github.com/ApolloAuto/apollo/blob/r3.5.0/cyber/transport/transmitter/transmitter.h) -> AddTransportEvent function in [perf_event_cache.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/cyber/event/perf_event_cache.cc). -> Enqueue function in [bounded_queue.h](https://github.com/ApolloAuto/apollo/blob/r3.5.0/cyber/base/bounded_queue.h) Stuck in here

| File (.cc)     | Line | Function Name | Usage | Flags involved | Potential for Privacy Leak |
| ----------- | ----------- |----------- |----------- |----------- |----------- |
| [camera_component.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/drivers/camera/camera_component.cc#L84) | 84-111 |void CameraComponent::run() |convert row_image to pb_image than use apollo::cyber::Writer |No flag |not call in this file, depends on the file that calls this function |
| [compress_component.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/drivers/camera/compress_component.cc#L50) | 50-80 |writer_->Write(compressed_image) |write compress image |No flags |not call in this file, depends on the file that calls this function |
| [conti_radar_message_manager.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/drivers/radar/conti_radar/conti_radar_message_manager.cc#L72) | 72-143 |ContiRadarMessageManager |write the radar message |    if (sensor_data_.contiobs_size() <= sensor_data_.object_list_status().nof_objects()) |not call in this file, depends on the file that calls this function, the initial value of contiobs_size, nof_objects is not define in this file|

 # Search of "cv::imencode()" #

 `cv::imencode()` ()
 Cv2.imencode () function is to convert (encode) the image format into streaming data and assign it to memory cache. It is mainly used for compressing image data format to facilitate network transmission.

| File (.cc)     | Line | Function Name | Usage | Flags involved |Potential for Privacy Leak |
| ----------- | ----------- |----------- |----------- |----------- |----------- |
| [compress_component.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/drivers/camera/compress_component.cc#L69) | 69 |if (!cv::imencode(".jpg", tmp_mat, compress_buffer, params)) |output image |No flags | memory cache will not leak privacy |


 # Search of "fprintf" #

 `fprintf` ()
frpint is to format the output into a stream/file

| File (.cc)     | Line | Function Name | Usage | Flags involved |Potential for Privacy Leak |
| ----------- | ----------- |----------- |----------- |----------- |----------- |
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L218) | 218-292 | output_laneline_to_json | output the lane line information to json file | No flag in the file, find flag in the file that use the function [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#214) FLAGS_lane_result_output |not call in this file, depends on the file that calls this function,use the function in [lane_denseline_eval.cc](https://github.com/ApolloAuto/apollo/blob/r3.5.0/modules/perception/camera/tools/lane_detection/lane_denseline_eval.cc#217) , output the information about lane line to json|
| [lane_common.cc](https://github.com/ApolloAuto/apollo/blob/a8f1259179067c5e0e7cc80f5aaafab495524f17/modules/perception/camera/tools/lane_detection/lane_common.cc#L294) | 294-335 | output_laneline_to_txt | output the lane line information to txt file | No flag in the file |not call in this file, depends on the file that calls this function, output the information about lane line to json, not find in program|



# VIN

An access to CAN bus for VIN (vehicle identification number)
See https://github.com/ApolloAuto/apollo/blob/fd8ffe3d0a4234cfa7fdb3d1da74d58ee0cb7002/modules/data/util/info_collector.cc#L80

More on VIN https://en.wikipedia.org/wiki/Vehicle_identification_number
