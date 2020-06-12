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
   * 3.1 Distillation Objective
      - Teacher = deep bidirectional encoder, Student = lightweight model with fewer layers
      - BERT-Base = BERT(12), BERT-Large = BERT(24), BERT-K layers = BERT(k)
      - Final object for knowledge distillation 
      
![Picture1](https://user-images.githubusercontent.com/65929463/84465351-be4b0d80-acb1-11ea-9271-a5db165d8823.jpg)

   * 3.2 Patient Teacher for Model Compression
      - Student network can achieve comparable performance to the teacher model on the Training Set. But, Learned with Vanilla KD can reach Saturation on Test Set. 
      - One hypothesis = Overfitting during knowledge distillation may lead to poor generalization
      
![Picture2](https://user-images.githubusercontent.com/65929463/84465359-c1de9480-acb1-11ea-9ba1-727289fa70a4.jpg)

   - Propose Two Patient Distillation Strategies
       - PKD-Skip: the student learns from every k layers of the teacher
       - PKD-Last: the student learns from the last k layers of the teacher
      - Because of Expensive and Introduce noise
       - BERT : the output from the last layer’s [CLS] token.
       - SDNet : a weighted average of all layers’ [CLS] embeddings is applied.
      - When model compression is performed, learning the expression of the middle layer of [CLS] will likely increase the generalization ability.

![Picture3](https://user-images.githubusercontent.com/65929463/84465372-c86d0c00-acb1-11ea-9dda-1b7c3a14672b.jpg)

Middle layer for Knowledge distillation                                          

![Picture4](https://user-images.githubusercontent.com/65929463/84465374-ca36cf80-acb1-11ea-9696-3a68a9afc0e6.jpg)

PKD loss is defined as MSE (M = # of student layers)


![Picture5](https://user-images.githubusercontent.com/65929463/84465381-ce62ed00-acb1-11ea-8e14-689c35ef1fff.jpg)

The final objective function can be formulated

![Picture6](https://user-images.githubusercontent.com/65929463/84465385-d0c54700-acb1-11ea-9c96-44297b506a63.jpg)

### **4. Experiments**
   * 4.1 Datasets
      - SST-2, MRPC, QQP, MNLI, QNLI, RTE, etc. were used
      - Machine Reading Comprehension Task – RACE (1 question , 4 candidates answers, one is correct) 
   * 4.2 Baselines and Training Details
      - Use the same architecture in the original BERT, and fine-tune each task independently.
      - BERT12 = BERT-Base, and Use 3 and 6 layers of Transformers as the Student models. 
      - # of hidden units in the final softmax layer = 768
      - Batch Size = 32
      - Number of Epoch = 4 
      - Learning rate = (5e-5, 2e-5, 1e-5)
      - On Vanilla KD, T = (5, 10, 20), alpha = (0.2, 0.5, 0.7)
      - On Patient-KD, Beta = (10, 100, 500, 1000)
   * 4.3 Experimental Results

![Picture7](https://user-images.githubusercontent.com/65929463/84465390-d3c03780-acb1-11ea-87c9-dd8d3af36f5a.jpg)

![Picture8](https://user-images.githubusercontent.com/65929463/84465393-d589fb00-acb1-11ea-941d-e7129a009e39.jpg)

![Picture9](https://user-images.githubusercontent.com/65929463/84465397-d884eb80-acb1-11ea-8049-6a2ee8890cb9.jpg)

![Picture10](https://user-images.githubusercontent.com/65929463/84465404-da4eaf00-acb1-11ea-9833-542587054040.jpg)

![Picture11](https://user-images.githubusercontent.com/65929463/84465407-dd499f80-acb1-11ea-8b3c-720b73a82a44.jpg)

### **5. Conclusion** 
   * This paper introduced a novel approach to compressing large BERTs (PKD).
   * In order to capture the rich information of the teacher model, it is better for the student to distill the multilayer.
   * Their model proved to be effective in four NLP tasks.
   * In the future, They will try to solve the BERT initialization mismatch issue when pre-training.
   * Designing a more sophisticated distance metric is one direction.
   * PKD to help with complex settings like multi-task and meta-learning.

