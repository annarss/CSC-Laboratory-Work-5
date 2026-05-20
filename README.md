#  Laboratory-Work-5-Activity
https://drive.google.com/drive/folders/1uPfU2OZytqSSNGZuxLYKyg4O3FLJqVr_?usp=drive_link

# .keras
https://drive.google.com/file/d/1B4RJ3LicycLfsLzXbIsPhsVAiwcsyFpW/view?usp=drive_link

##  PART 12: Performance Comparison Table

| Model | Train Acc | Train Loss | Val Acc | Val Loss | Precision | Recall | F1 | AUC |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **LW3 Baseline CNN** | 0.7545 | 0.7643 | 0.7699 | 0.7479 | 0.7985 | 0.7688 | 0.7696 | 0.9572 |
| **LW4 Improved CNN** | 0.5566 | 1.4283 | 0.7050 | 0.9974 | 0.7129 | 0.7016 | 0.7005 | 0.9051 |
| **Teachable Machine** | 0.9949 | 0.0056 | 0.9650 | 0.1710 | 0.0000 | 0.0000 | 0.0000 | 0.0000 |
| **MobileNetV2** | **0.9135** | **0.3544** | **0.9617** | **0.2182** | **0.9618** | **0.9620** | **0.9613** | **0.9953** |
| **EfficientNetB0** | 0.7294 | 1.1835 | 0.9017 | 0.7537 | 0.7731 | 0.7171 | 0.7182 | 0.9615 |
| **ResNet50** | 0.7938 | 0.7768 | 0.9263 | 0.4098 | 0.8095 | 0.7887 | 0.7870 | 0.9613 |

---

##  GUIDE QUESTIONS (FINAL REFLECTION) 

###  A. Model Performance 

**1. Which pre-trained model achieved the highest accuracy? Why?** > **Answer:** MobileNetV2 with an accuracy rate of 96.17%. It is designed to be highly efficient, meaning it can learn the most important features of an image very quickly without getting distracted by unnecessary details.

**2. Which model had the lowest performance? What could be the reason?** > **Answer:** EfficientNetB0 with an accuracy rate of 90.17%. While it is a very powerful model, it usually requires very specific image sizes and more training time to reach its full potential compared to the others.

**3. How did loss values compare across models?** > **Answer:** MobileNetV2 had the lowest final training loss at 0.3544 and validation loss of 0.2182, which means it learned the most. EfficientNetB0 stopped at training loss 1.1835 and val loss 0.7537 after just 3 epochs which is still pretty high. ResNet50 also stopped at 3 epochs with training loss 0.7768 and val loss 0.4098. Overall, MobileNetV2 had the best loss values by a big margin.

###  B. Evaluation Metrics

**4. Why is accuracy not enough to evaluate a model?** > **Answer:** Accuracy just tells you how many predictions were correct in total, but it doesn't tell you the full story. For example, if one class has very few images, the model could just ignore that class and still get high accuracy. That's why we also look at Precision, Recall, and F1-score — they show how the model performs on each individual class, not just overall.

**5. Which model had the best F1-score? What does it indicate?** > **Answer:** MobileNetV2 had the best F1-score at 0.96. F1-score is the balance between Precision and Recall, so a high F1 means the model is both accurate and consistent across all 20 plant classes. It means MobileNetV2 didn't just do well on easy classes — it did well on almost all of them.

**6. How did Precision and Recall differ across models?** > **Answer:** For MobileNetV2, both Precision and Recall were around 0.96, very balanced. For EfficientNetB0, Precision was 0.77 but Recall was 0.72 — some classes had very high precision but low recall, like areca_palm which had 88% precision but only 16% recall, meaning it rarely guessed that class. ResNet50 had Precision of 0.81 and Recall of 0.79, also decent but not as good as MobileNetV2.

###  C. Confusion Matrix Analysis 

**7. Which classes were frequently misclassified?** > **Answer:** Looking at the classification reports, the hardest classes were fiddle_leaf_fig, philodendron_xanadu, and areca_palm. For example, EfficientNetB0 got only 27% F1 on areca_palm and 46% on philodendron_xanadu. ResNet50 also struggled with fiddle_leaf_fig (50% F1) and philodendron_xanadu (49% F1). These plants look similar to others in my dataset. 

**8. What patterns did you observe in the confusion matrix?** > **Answer:** The diagonal of the confusion matrix was mostly bright (high numbers) for MobileNetV2, which means most classes were predicted correctly. For EfficientNetB0 and ResNet50, you could see more spread-out errors, especially for the plant classes that look visually similar like the different croton varieties or fern types. Plants that have similar leaf shapes and colors tended to confuse the models.

###  D. ROC and AUC 

**9. Which model had the highest AUC score?** > **Answer:** MobileNetV2 had the highest AUC score at 0.9953.

**10. What does AUC tell us about model performance?** > **Answer:** It tells us how well the model separates classes. A score of 0.99 means the model is almost 100% perfect at telling the difference between your different categories.

###  E. Explainability (Grad-CAM) 

**11. What did Grad-CAM reveal about model decision-making?** > **Answer:** It showed a heatmap of where the model "looked." It revealed if the model was looking at the actual object or just a random spot in the background.

**12. Did the model focus on relevant image regions?** > **Answer:** For MobileNetV2, yes — the heatmap mostly highlighted the leaves and the main plant features. This is the right behavior because that's what actually identifies the plant type. For the other two models, some heatmaps were a bit scattered, especially on images where the model was less confident. 

**13. Which model produced the most meaningful heatmaps?** > **Answer:** MobileNetV2 had the most meaningful heatmaps. Because it was the most accurate model, the red 'hotspots' in the Grad-CAM images were focused exactly on the object it was supposed to see. In the lower-performing models, the heatmaps were sometimes blurry or pointed at the background, showing that they weren't as focused on the right details as MobileNetV2 was.

###  F. Model Comparison & Improvement 

**14. Which model would you recommend for deployment? Why?** > **Answer:** I would recommend MobileNetV2. It got the best validation accuracy (96.17%), best F1-score (0.96), and highest AUC (0.9953). On top of that, MobileNetV2 is designed to be lightweight and fast, which means it can run on mobile phones and lower-end devices. Since my dataset is about plant classification, this could even work as a mobile plant identifier app.

**15. How can you further improve your best-performing model?** > **Answer:** I could use Data Augmentation (rotating or zooming into the photos) to help the model handle images taken from different angles or in different lighting.

###  G. Real-World Application

**16. How can your model be applied in real-world scenarios?** > **Answer:** Since my dataset about the ornamental plants, this model could be used as a plant identification app — someone takes a photo of a plant and the app tells them what type it is. It could also be used by nurseries or plant shops to help customers identify plants, or by students learning plant species.

**17. What are the risks of deploying an inaccurate model?** > **Answer:** The biggest risk is misidentification, which leads to the wrong care. For example, if the model confuses a Snake Plant (which needs very little water) with a Peace Lily (which loves moisture), the owner will overwater the Snake Plant and cause it to rot. Additionally, plants like the Peace Lily and Golden Pothos are toxic to pets. If the model incorrectly labels them as a "Safe" species, a cat or dog owner might put them in a dangerous spot, leading to a life-threatening emergency for their pet.

**18. How can this system be integrated into a mobile/web app?** > **Answer:** We convert the trained model into a small, fast file called TensorFlow Lite. This "mini-brain" is then put into a mobile app so it can run directly on a smartphone. A user simply points their camera at an ornamental plant, like a Snake Plant or Calathea, and the app instantly identifies it on the screen.
