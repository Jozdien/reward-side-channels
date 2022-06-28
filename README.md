# Reward Side-Channels

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Jozdien/reward-side-channels/blob/main/Reward_Side_Channels.ipynb)

## To-Do List

Before even beginning with this, read [Risks from Learned Optimization](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB) (specifically the section linked in [[2]](#ref-2)).

1. ~~Set up all the dependencies for running SpinningUp on Colab.  [[3]](#ref-3).~~ - Amrita
2. Test setting up model checkpoints and storing data to Drive automatically to account for runtime errors or pauses (run some small model with a lot of steps).  [[5]](#ref-5) [[6]](#ref-6).- Amrita
3. These two steps should be independent enough of the other to do parallelly (I'm not sure about this, if it starts to seem otherwise stop trying to do them separately __immediately__).
    1. Create modified lunarlander environment.  I think we can do better than the changes we made earlier - at the very least, we'll need to discuss properly what both rewards are, and whether they're different enough.  It might also be possible to implement the changes we need in the same env class, with flags passed as parameters at call time to decide what reward.
    2. Building the RL agent
        1. Figure out the architecture of the model, especially with needing these many parameters including the decision transformer. [[4]](#ref-4).
            1. Get the Colab paid tier.
            2. Figure out how many parameters are actually feasible, even on the highest paid tier (we can settle for the long runs taking a few days, but not more than that).
        2. For the love of everything good and holy, iteratively test with tiny runs after adding each component (eg, after making the model slightly bigger) so we don't have to figure out what's going wrong after adding everything together.
4. Test, test, test, before running everything on large runs.
5. Do a proper run.  This involves training the model on the first environment and then __testing__ it on the second (this could mean setting epsilon for exploration to very low in this second phase).
6. If the result seems to imply that the reward is learned internally, try designing more environments with different rewards and train the model on them successively, to increase the inductive bias of the training procedure toward corrigible alignment.

## References

1. [Primary Reference](https://www.alignmentforum.org/posts/uSdPa9nrSgmXCtdKN/concrete-experiments-in-inner-alignment) - Evan's original experiment description. <span id="ref-1"></span>

2. [Reference for understanding motivation better](https://www.alignmentforum.org/s/r9tYkB2a8Fp4DN8yB/p/zthDPAjh9w6Ytbeks#4_4__Internalization_or_deception_after_extensive_training) - Some additional info on the motivation behind understanding the likelihood of corrigible vs robust alignment. <span id="ref-2"></span>

3. [Colab reference for SpinningUp dependencies](https://colab.research.google.com/github/lcipolina/gymAI/blob/master/0-Gym_Envs_3_spinup_ExperimentGrid.ipynb) <span id="ref-3"></span>

4. [Code for Decision Transformer in RL](https://github.com/nikhilbarhate99/min-decision-transformer) <span id="ref-4"></span>

5. [Colab reference for saving and loading checkpoints - TensorFlow](https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/keras/save_and_load.ipynb) <span id="ref-5"></span>

6. [Colab reference for saving and loading checkpoints - PyTorch](https://colab.research.google.com/github/pytorch/tutorials/blob/gh-pages/_downloads/9e9be5fea5bc1cdd5fd8f2305b475f16/saving_and_loading_a_general_checkpoint.ipynb)<span id="ref-6"></span>
