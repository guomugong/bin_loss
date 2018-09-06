## Bin loss for hard exudates segmentation in fundus images

## Introduction
Diabetic retinopathy is one of the leading reasons that causes blindness. And the segmentation of hard exudates in color fundus images is crucial for early diagnosis of diabetic retinopathy, which is a difficult task due to its uncertainty in size, shape and contrast. Class-balanced cross entropy (CBCE) loss is the most popular objective function for image segmentation task to solve the class-unbalance problem. However, we show that background pixels tend to be misclassified to hard exudates in CBCE since the loss for a misclassified background pixels is much smaller than that for a misclassified hard exudate pixel, which is called loss-unbalance problem here. A top-k loss is proposed in this paper, which considers the cases of both class-unbalance and loss-unbalance by focusing more over the hard-to-classify pixels. Moreover, a fast version of the top-k loss, named bin loss, is implemented for efficiency, which reduces the time complexity from O(nlogn) of top-k loss to O(n), where n is the number of background pixels. We evaluated the proposed bin loss over two public datasets for hard exudates segmentation task, including e-ophtha EX and IDRID. Furthermore, three popular models for image segmentation, HED, DeepLab v2, and FCRN, were used to evaluate the versatility of bin loss. Extensive experiments show that each model with the proposed bin loss performs better than that with CBCE loss, which demonstrates bin loss is versatile so that it can be applied to different models for performance improvement.

## Usage:
```
layer {
  name: "loss"
  type: "BinLoss"
  bottom: "pred"
  bottom: "label"
  top: "loss"
  bin_loss_param {
    key: 20
	lambda: 1
  }
}
```
The usage is the same as `SigmoidCrossEntropyLoss` layer.
