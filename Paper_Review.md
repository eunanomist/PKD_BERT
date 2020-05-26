# Patient Knowledge Distillation for BERT Model Compression(2019-EMNLP)
## Paper Review

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
### **3. Patient Knowledge Distillation**
### **4. Experiments**
### **5. Conclusion** 
   * They propose a novel approach to compressing a large BERT model into a shallow one via Patient Knowledge Distillation.
   * To fully utilize the rich information in deep structure of the teacher network, our Patient-KD approach encourages the student model to patiently learn from the teacher through a multi-layer distillation process.
   * Extensive experiments over four NLP tasks demonstrate the effectiveness of our proposed model.
   * For the Future work : plan to pre-train BERT from scratch to address the initialization mismatch issue, and potentially modify the proposed method such that it could also help during pre-training.
