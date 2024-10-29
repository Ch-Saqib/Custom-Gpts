# Custom GPTs vs Assistants

## GPTs vs Assistants: Key Differences

### Drawbacks of Using a Custom GPT System:

1. **Limited Access to User Interactions:**
   - **Lack of Chat Data:** We don’t have access to user chat data, which limits our ability to fine-tune the model based on actual user interactions and various user types.
   - **Impact on Accuracy:** Without user interaction data, it’s challenging to assess the model’s accuracy and effectiveness in practical settings.

2. **Challenges in Improving User Experience:**
   - **Data-Driven Enhancements:** The absence of user interaction data restricts our ability to improve and personalize the user experience.
   - **GUI Component Streaming:** For some use cases, our GUI component streaming solution via the Vercel SDK may be more effective than a custom GPT system.

3. **Message Limits for Free Users:**
   - **Daily Limits:** Free users are limited to approximately 10 messages per day, with fluctuations based on the time of day.
   - **Session Restrictions:** Users are further limited to 3-5 messages every 5-6 hours, which may impact the application's usability.
   - **Starter Prompt Requirement:** Each session begins with one message as a starter prompt, leaving around 4 messages every 5 hours for interaction.
