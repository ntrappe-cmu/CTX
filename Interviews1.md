1. Researchers don't use branches properly - They work in a single branch and do "save-as" versioning (experiment_v1.py, experiment_v2.py, experiment_final_REALLY_FINAL.py) instead of using git's branching model
2. Git doesn't version the right things for research - Code changes are tracked, but what about: the dataset that changed, the random seed, the hyperparameters, the hardware it ran on, the failed experiments you didn't commit, the intellectual reasoning for trying approach B after A failed?
3. The real artifact isn't the code - Research "versions" should probably track complete experimental runs with their inputs, outputs, and provenance, not just code snapshots

4. - The problem isn't version control, it's provenance tracking
What researchers actually need isn't better branching - it's answers to questions like:
