# Patient Knowledge Distillation for BERT Model Compression
## Paper Review

### **Abstract**
* Pretrained language models like BERT is highly effective for NLP, But high demand for computing resources in trianing models hinders application in proctice
* PDK approach to compress an original large model(teacher) into an equally effective lightweight shallow network(student)
* Student model *patiently* learns from multiple intermediate layers of the teacher model for incremental knowledge extraction
  - PKD_Last : learning from the last *k* layers
  - PKD_Skip : learning from every *k* layers
* these 2 ways of PKD enble the exploitation of rich information in the teacher's hidden layers, and encourage the student model to *patiently* learn from and imitate the teacher through a multilayer distillation process.
* Improved results without sacrificing model accuracy

 ### **1. Introduction**
 ### **2. Related Work**
 ### **3. Patient Knowledge Distillation**
 ### **4. Experiments**
 ### **5. Conclusion** 

* Post2
* Post3
