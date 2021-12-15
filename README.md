# ML-Cyber-Security-Lab3 report
A repaired goodnet using the pruning defense

## Load Data and Test Model
We use four datasets to do this lab. They are test.h5, valid.h5, bd_test.h5, bd_valid.h5. you can find the link in the data file. Also, we have a backdoored neural network classifier with N classes. And using 'evl' function, we can get clean classification accuracy and the attack success rate of the base network on valid.h5 and bd_valid.h5.
## Prune Model
Using the pruning defense in class. That is, I will prune the last pooling layer of BadNet B (the layer just before the FC layers) by removing one channel at a time from that layer. Channels should be removed in decreasing order of average activation values over the entire validation set. Every time I prune a channel, I will measure the new validation accuracy of the new pruned badnet. I will save the new model into a file once the validation accuracy drops atleast X% below the original accuracy. This will be the new network B'.
## Good Net
Then we can design the repaired goodnet G. It works as follows. For every test input, we run it through both base network bd_model and new network B'. and if the predicted class outputs are the same, we output the same one classfication. However, if they are different, we output the class N+1. That's how we design the goodnet.
## Evaluation on new model
We design a new version of evaluation function named 'evl2', and use this to get the accuracy on clean test data and the attack success rate (on backdoored test 
data) on the goodnet G.
## Accuaracy of pruned channels 
Plot the accuracy on clean test data and the attack success rate (on backdoored test 
data) as a function of the fraction of channels pruned.
![image](https://user-images.githubusercontent.com/91434745/146216993-3f885e32-c120-4abc-8bb4-fd68ff81bbf3.png)
## Conclusion
From the first beginning, before the pruning defense, the accuracy is 98.65 and the Attack Success Rate is 100.0. And from the Evaluation part, we can see that if we prune the channel a little bit, The effect is not very obvious. As the number of channel pruned increase, the attack success rate decrease. And the attack success rate decrease a lot when we prune a lot of channels. However, the accuracy decrease a lot, too. Also, from the plot above, we can see that there is no big 'green space' like the space in the following picture. That is, backdoor diasabled with compromising clean set accuracy. So I think the pruning defense actually doen not works for this model. And this may because the attacker(this bd_model) adapts to this defense, that is, adaptive attacker introduces sacrificial neurons in the network to diable pruning defense. And that's why we didn't see obvious effect of our defense methods.

![image](https://user-images.githubusercontent.com/91434745/146217049-c2e6ccdf-b39f-4c3e-83a4-bcaa7642a633.png)
