# MapGeneralization
Make generalized maps from technical drawings 

## Pipeline
**DWG(optional) -> DXF:** Can be done online at https://anyconv.com/dwg-to-dxf-converter/  
**DXF -> Line data -> Graph:** Use DxfReader.extract_data() to create line data and DxfReader.convert_data_to_graph() to convert it to a graph  
**Train Graph node classifiation:** Use train.py for sliding window <br/> Use train_gcn.py for batched graphs of different sizes + DeepWalk embedding  
**Test graph node classifiation:** Use test.py for sliding window <br/>
Use testgcn.py for batched graphs of different sizes + DeepWalk embedding

### Notes about graphs
We've added some example floorplans that we found online for training/testing. In order to train with the graphs you must
 first annotate them (which examples have also been provided under data/graph_annotations). If you want to annotate some 
 new data then under our src folder there is the script annotation_tool.py

### Notes when running train_gcn.py
The graphs you want to train with should be under data/graph_annotations. To let train_gcn.py know which graphs you want
 to train with, edit the train_file_list.txt under the data folder
<br/>
<br/>
DeepWalk (node embeddings) takes time to run for the graphs provided. Therefore when the embedding is done, it is 
saved in a '.embeddings' file under data/embeddings. That way when you want to test different parameters with the 
GCN model, you don't have to wait for the same embedding. If you change some paramters within the execute_deepwalk() 
function, then it is recommended to delete these previously stored embeddings.