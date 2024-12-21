![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXclc23Ah4X-B_q9a_Amw3D-vxJF43Yp4Ms7_r4VJK8eIQs1pgIsYRFtTc0ZlKg9tqVW1Da2xNka1dB3zrGUlwRI9bzcM_3dCVkTxZ0C3_r-sFS9PfwQIEpzEnTCAiV6T2NgYOWg4Q?key=GgJlJs81vZ1Rn7pNNxesjX_J)

# What is ContextCore? 
ContextCore is the bridge between you and your tools, embedding your individuality into any system to make it feel personal, alive, and uniquely yours. It’s not just context—it’s a digital echo of your sentience, transforming AI from a generic mirror into a true extension of your mind.

A system (leveraging RAG for now) that is essentially a "context" database that I can maintain and manage over a long period of time. And it's localized and private, yet I can still plug it into any LLM models that are running globally. OR I could feed it to a local model if I'd like. The main advantage of what I'm building is the ability to build a database of information about yourself whose only capacity is how much memory YOU have, not the company providing the LLM, while also owning that information and keeping it private and local.And you can “turn on/off” different contexts depending on what kind of answer you want. For instance, if you want to know if you are blind to some relationship issues and can’t understand the problem, your AI answers may also be biased and blind to something. So you could disable all relationship context and then re-run your query. Additionally, you don’t have to stay loyal to any LLM provider, as your context will be interchangeable between many models.


> [!TIP] Components
> **ContextCore**
> Name of the company/organization. We are going to create an open source framework called ContextWeave, and a premium product called Akasha. 
> 
> **ContextWeave**
> This open source framework allows you to maintain and manage a context store of information that can be categorized and used via RAG to make a query to any LLM you plug it into (as long as that LLM has APIs for you to call it). It will also allow you to import/export your context store. The final step would be to expand the import functionality to translate imported contexts from other llm providers like chatgpt.  
> 
> **Akasha**
> Premium product that leverages ContextWeave and implements additional features. The premium product will be called something like Mentis, Cognis, Akasha, etc. 

> [!IMPORTANT] Core Pro Features
> **Integrations**: Allow you to seamlessly integrate different sources of data to ContextCore for automatic ingestion/categorization  
> 
> **Humors**: Think of these as emotional states / moods. They should map to Adjectives
> 
> **Mimics**: Think of these as Versions of people in terms of their history, thinking pattern, and style of speaking. These should map to Nouns
> 
> **Prisms (or Focus)**: Think of these as configuration profiles that contain different combinations of Elements, Humors, and Mimic settings. Kinda like "work focus" on iPhone or something.
