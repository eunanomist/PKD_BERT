# Patient Knowledge Distillation for BERT Model Compression(2019-EMNLP)
## Paper Review

### **Contents**

Abstract
Introduction
Related Work
Language Model Pre-training
Model Compression & Knowledge Distillation
3. Patient Knowledge Distillation
3.1 Distillation Objective
3.2 Patient Teacher for Model Compression
4. Experiments
4.1 Datasets
4.2 Baselines and Training Details
4.3 Experimental Results
4.4 Analysis of Model Efficiency
4.5 Does a Better Teacher Help?
5. Conclusion




### **Abstract**
 * Pretrained language models like BERT is highly effective for NLP, But high demand for computing resources in trianing models hinders application in proctice.
 * PDK approach to compress an original large model(teacher) into an equally effective lightweight shallow network(student).
 * Student model *patiently* learns from multiple intermediate layers of the teacher model for incremental knowledge extraction.
   - PKD_Last : learning from the last *k* layers
   - PKD_Skip : learning from every *k* layers
* these 2 ways of PKD enble the exploitation of rich information in the teacher's hidden layers, and encourage the student model to *patiently* learn from and imitate the teacher through a multilayer distillation process.
* Improved results without sacrificing model accuracy.

### **1. Introduction**
  *  Pre-training has proven to be highly effective, But, computational efficiency is a widely recognized issue because of its large number of parameters. training from scratch takes four days on 4 to 6 Cloud TPUss. Even fine-tuning may take several hours.
  * Reducing computational costs for such models is crucial for their apllication in practice, where computational resources are limited.
  * the teacher model outputs probability logits and predicts labels for the training samples, and the student model learns from the teacher network to mimic the teacher's prediction.
  * Instead of learning parameters from only the last layer of the teacher, they encourage the student model to extract knowlegde also from previous layers of the teacher network. this is PKD which has rich information through the deep structure of the teacher network for multi-layer knowledge distillation.
    - PKD_Last : the student learns form the last *k* layers of the teacher, under assumption that the top layers of the original network contain the most informatice knowledge to teach the student.
    - PKD_Skip : the student learns from every *k* layers of the teacher, suggesting that the lower layers of the teacher network also contain important information and should be passed along for incremental distillation.
    
### **2. Related Work**
   * Language Model Pre training
      - Feature based approach – Context independent word representation, Sentence level representation, contextualized word           representation
      - Fine tuning approach – GPT, BERT etc. training labeled data when downstream task 
   * Model Compression & Knowledge Distillation
      - Network pruning 
      - Weight quantization 
      - Knowledge Distillation (in 2015 by Hinton, to compress large parameters into a model that can be executed quickly. The compact model mimics the soft output of the existing model. Romero 2015 shows that learning a medium model representation of a small model is also a way to improve performance during the learning process)
      
      ***In this paper, effectively compress the teacher model into the student model using the method called Patient knowledge distillation.***
      
### **3. Patient Knowledge Distillation**
Problem Define : The student model to imitate outputs from the teacher model on the training dataset with a defined objective

![Picture1](https://user-images.githubusercontent.com/65929463/84465351-be4b0d80-acb1-11ea-9271-a5db165d8823.jpg)
![Picture2](https://user-images.githubusercontent.com/65929463/84465359-c1de9480-acb1-11ea-9ba1-727289fa70a4.jpg)
![Picture3](https://user-images.githubusercontent.com/65929463/84465372-c86d0c00-acb1-11ea-9dda-1b7c3a14672b.jpg)
![Picture4](https://user-images.githubusercontent.com/65929463/84465374-ca36cf80-acb1-11ea-9696-3a68a9afc0e6.jpg)
![Picture5](https://user-images.githubusercontent.com/65929463/84465381-ce62ed00-acb1-11ea-8e14-689c35ef1fff.jpg)
![Picture6](https://user-images.githubusercontent.com/65929463/84465385-d0c54700-acb1-11ea-9c96-44297b506a63.jpg)
![Picture7](https://user-images.githubusercontent.com/65929463/84465390-d3c03780-acb1-11ea-87c9-dd8d3af36f5a.jpg)
![Picture8](https://user-images.githubusercontent.com/65929463/84465393-d589fb00-acb1-11ea-941d-e7129a009e39.jpg)
![Picture9](https://user-images.githubusercontent.com/65929463/84465397-d884eb80-acb1-11ea-8049-6a2ee8890cb9.jpg)
![Picture10](https://user-images.githubusercontent.com/65929463/84465404-da4eaf00-acb1-11ea-9833-542587054040.jpg)
![Picture11](https://user-images.githubusercontent.com/65929463/84465407-dd499f80-acb1-11ea-8b3c-720b73a82a44.jpg)


### **4. Experiments**
### **5. Conclusion** 
   * They propose a novel approach to compressing a large BERT model into a shallow one via Patient Knowledge Distillation.
   * To fully utilize the rich information in deep structure of the teacher network, our Patient-KD approach encourages the student model to patiently learn from the teacher through a multi-layer distillation process.
   * Extensive experiments over four NLP tasks demonstrate the effectiveness of our proposed model.
   * For the Future work : plan to pre-train BERT from scratch to address the initialization mismatch issue, and potentially modify the proposed method such that it could also help during pre-training.
