# Sentence Constructor

We explore three different LLMs for our english-japanese sentence constructor.

Their performance on this activity would rank as follows:
1. Claude Sonnet 3.5 v2
2. ChatGPT
3. MetaAI

This outcome was as expected due to the model size and differences. 

MetaAI required more tuning to create a better response (as well as removing the invisible japanese characters). 

ChatGPT did better but still needed very specific instructions as well as reafirming them for it to provide a reasonable answer.

Claude Sonnet 3.5v2 (aws bedrock) performed the best and required little tuning. 

The biggest challenge for me was the agent states. Before the "Architecting States" video, my approach was to try and steer the model behaviour throughout the whole chat from the beginning, which stops working after a couple messages. This was overcome through different states/phases that the LLM would assume.