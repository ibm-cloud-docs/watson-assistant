---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-03"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the home screen
{: #web-chat-configure-home-screen}

On the **Home screen** tab, you can configure the contents of the home screen, which welcomes customers and helps them start the conversation with the assistant. The home screen replaces any greeting that would otherwise be sent by the *Greet customer* system action.

![An example of the home screen](images/home-screen.png){: caption="Home screen" caption-side="bottom"}

If you prefer to use a *Greet customer* system action instead of the home screen, you can disable it by clicking the toggle on the **Home screen** tab.

If you use the home screen, you must configure it to show content that is relevant to your customers:

- In the **Greeting message** field, type a greeting that is engaging and invites the user to interact with your assistant. This greeting is the first message that your customers see when they open the web chat window.

- In the **Conversation starters** section, specify the conversation starter messages that you want to be displayed on the home screen.

    These messages are displayed on the home screen as options that customers can click to start the conversation (for example, `I need to reset my password` or `What is my account balance?`). Specify conversation starters that are likely to be useful to your customers, and that your assistant knows how to handle. 

    Be sure to test each conversation starter. Use only messages that your assistant understands and knows how to answer well. Conversation starters cannot be longer than 35 characters.

    You can specify up to 5 conversation starters.

The messages that you specify are immediately reflected by the web chat preview that is shown on the page, and you can click the conversation starters to see how your assistant responds. However, no configuration changes are applied to the environment until you click **Save and exit**.
