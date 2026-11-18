# Related Work and Research Notes

## TENT

**Paper:** Tent: Fully Test-Time Adaptation by Entropy Minimization

### What it does
TENT adapts a pretrained model at test time using unlabeled target data. It minimizes prediction entropy so that the model becomes more confident on shifted test examples.

### Why it matters for PatchStop
TENT shows that test-time adaptation can be performed without access to ground-truth test labels.

### How PatchStop differs
TENT uses entropy as its unsupervised signal. PatchStop instead studies whether agreement across masked views can indicate when adaptation should stop.

---

## TTT-MIM

**Paper:** Test-Time Training with Masked Image Modeling for Denoising Distribution Shifts

### What it does
TTT-MIM uses masked image reconstruction as a self-supervised task during test-time training.

### Why it matters for PatchStop
It provides motivation for using masked visual information during test-time adaptation.

### How PatchStop differs
TTT-MIM uses reconstruction loss for adaptation. PatchStop uses classification agreement across masked views as a stopping signal.

---

## AdaContrast

**Paper:** Contrastive Test-Time Adaptation

### What it does
AdaContrast combines test-time pseudo-labeling with contrastive learning. It improves pseudo-label quality through online refinement and soft voting among nearby target examples.

### Why it matters for PatchStop
The paper shows that raw pseudo-labels can be noisy and that aggregating multiple predictions can provide more reliable pseudo-label supervision.

It also identifies compounding pseudo-label errors as an important failure mode during adaptation.

### How PatchStop differs
AdaContrast votes across neighboring target examples in feature space. PatchStop votes across masked views of the same test image.

---

## Teacher-Student Test-Time Adaptation

### What it does
Teacher-student methods use a teacher model to produce pseudo-labels while a student model adapts.

Recent work shows that continuously updating the teacher can still allow errors to accumulate, while a fixed teacher can provide a more stable pseudo-label source.

### Why it matters for PatchStop
This supports evaluating whether repeated self-adaptation can reinforce incorrect pseudo-labels.

### How PatchStop differs
PatchStop attempts to control error accumulation by deciding when adaptation should stop rather than relying only on a separate teacher model.

---

## CIFAR-100-C

CIFAR-100-C is used to evaluate model robustness under common image corruptions at different severity levels.

Our initial PatchStop experiments focus on Gaussian noise, particularly severities 4 and 5.

Existing frozen ViT results:

- Severity 4: 51.34%
- Severity 5: 44.99%

Supervised Gaussian-noise reference:

- Severity 4: 78.65%
- Severity 5: 76.00%

Ground-truth labels are used for evaluation only in the unsupervised PatchStop experiments.