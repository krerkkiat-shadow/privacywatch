# How many different ways are there to write image or video files to hard disks?

* `cv::imwrite()`
* `ofstream`
* `cv::imencode()`

# About FLAGS

* https://github.com/drchangliu/vital/blob/master/notes/perception_checking.md
 
 # Search of "cv::imwrite()" #
 
 `cv::imwrite()` (9 usages in 7 files) 
 
 
| File    | Line | Function Name | Usage | Flags Involved |
| ----------- | ----------- |----------- |----------- |----------- |
| [base_map_node.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_map/base_map/base_map_node.cc)      | [470](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_map/base_map/base_map_node.cc#L470)       | SaveIntenstiyImage(), called from Save(), called from BaseMapNode::Finalize() | Saves/resizes a map image (only if flag is set to be true; false by default).| is_changed_, set to false in Init(), Line 53 |
| [visualization_engine.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc)      |[627](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc#L627) [664](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/localization/msf/local_tool/local_visualization/engine/visualization_engine.cc#L664)| GenerateMultiResolutionImages() | Copies images. | First usage has no flags and is used upon initialization of the VisualizationEngine. Second usage is controlled by a local variable called "flag" and is true if a path exists. |
| [yolo_camera_detector_test.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/detector/yolo_camera_detector/yolo_camera_detector_test.cc) | [133](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/detector/yolo_camera_detector/yolo_camera_detector_test.cc#L133)| Test_F | Testing- not part of the final program. | N/A |
| [cc_lane_post_proccessor_test.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc) | [77](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc#L77) [176](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/camera/lane_post_process/cc_lane_post_processor/cc_lane_post_processor_test.cc#L176) | Test_F | Testing- not part of the final program. | N/A |
| [write_img.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/lidar/segmentation/cnnseg/write_img.cc) | [58](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/obstacle/lidar/segmentation/cnnseg/write_img.cc#L58)| (int) main() | Saves LiDAR images. | No flags. |
| [tl_preproccessor_subnode.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_preprocessor_subnode.cc) | [166](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_preprocessor_subnode.cc#L166)| SubCameraImage() | Saves image (only if flag is set to be true). | FLAGS_output_raw_img is set to false when initialized in [perception_gflags.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/common/perception_gflags.cc#L95), line 95. |
| [tl_proc_subnode.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_proc_subnode.cc) | [140](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/traffic_light/onboard/tl_proc_subnode.cc#L140) | OutputDebugImg() | Saves image (only if flag is set to be true). | FLAGS_output_debug_img is set to false when initialized in [perception_gflags.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/perception/common/perception_gflags.cc#L96), line 96. |


# Search of "ofstream" #
 
 `ofstream` (35 usages in 25 files) 
 
 
| File     | Line | Function Name | Usage | Flags Involved |
| ----------- | ----------- |----------- |----------- |----------- |
| [apollo_app.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/apollo_app.cc) | [43](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/apollo_app.cc#L43) | ExportFlags() | Exports flags to a file. | No flags. |
| [file.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/util/file.cc) | [115](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/common/util/file.cc#L115) | CopyFile() | Copies contents from one file to another. | No flags. |
| [lat_controller.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.cc) | [60](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.cc#L60) | WriteHeaders() | Writes headers, but only if flag is set to true. | FLAGS_enable_csv_debug is set to false by default. |
| [lat_controller.h](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.h) | [203](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/lat_controller.h#L203) | class LatController (protected) | Logging purposes for steering. | No flags. |
| [mpc_controller.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/mpc_controller.cc) | [59](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/control/controller/mpc_controller.cc#L59) | WriteHeaders() | Nothing. | No flags. |
| [event_collector_main.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc) | [82](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc#L82) [161](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/data/tools/event_collector_main.cc#L161)| Stop()     SaveEvent() | First usage: Saves event related bags. Second usage: adds new event to a file. | No flags. |
| [hmi_worker.cc](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/dreamview/backend/hmi/hmi_worker.cc) | [109](https://github.com/ApolloAuto/apollo/blob/r3.0.0/modules/dreamview/backend/hmi/hmi_worker.cc#L109) | SetGlobalFlag() | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
| []() | []() | | | |
