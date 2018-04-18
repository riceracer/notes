## Who Let The Dogs Out? Modeling Dog Behavior From Visual Data

* https://arxiv.org/abs/1803.10827
* https://arxiv.org/pdf/1803.10827.pdf

Acting like a dog
* represent angular displacements via quanternions (4D complex number)
* quantize angular joint movements via K-means clusters so that action space is discrete
* Feed 2 successive image frames into CNN
* CNN feeds encoded features into an LSTM
* CNN is two towers of ResNet-18 (one for each frame)
* Decoder's job is predict the future joint movement for each step, prior state's predictions are passed forward on each step
* Loss = weighted class entropy loss

Planning like a dog
* Task: given non-consecutive image frames plan a series of actions to get from frame 1 to frame N
* Model: RNN containing an LSTM
* Each step the LSTM outputs planned actions as input to the next step
* Action probabilities are passed forward at each step, meaning low probably actions early can end up on high probability paths. This avoids early pruning to keep action possibilities open.

Learning from a dog
* Task: how does the representation learned from above generalizes to other tasks (walkable surfaces)?

Implementation details:
* GoPro captures video, Rasberry Pi captures motion from IMUs. The two are synced via audio captured in both systems to 5 FPS.
* This continuous value estimation problem formulated as classification because they get better results from this using CNNs than doing regression to continuous values.
 * Tuned the number of action classes for each joint (number of clusters) by visualing the action space -8 provided good separation of clusters, no false clusters and matches to natural movement of limbs.

Measurement:
* average per class accurancy
* perplexity: likelihood of ground-truth label (often used in sequence modeling)
