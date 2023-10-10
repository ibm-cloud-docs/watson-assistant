---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-10"

subcollection: watson-assistant
content-type: tutorial
account-plan: lite
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# Building a complex dialog
{: #tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="2h"}

In this tutorial, you create a dialog for an assistant that helps users with inquiries about a fictitious restaurant called *Truck Stop Gourmand*.
{: shortdesc}

## Learning objectives
{: #tutorial-objectives}

By the time you finish the tutorial, you learn how to:

- Plan a dialog.
- Define custom intents.
- Add dialog nodes that can handle your intents.
- Add entities to make your responses more specific.
- Add a pattern entity, and use it in the dialog to find patterns in user input.
- Set and reference context variables.

### Duration
{: #tutorial-duration}

This tutorial takes approximately 2 to 3 hours to complete.

### Prerequisite
{: #tutorial-prereqs}

Before you begin, complete the [Getting started with dialog tutorial](/docs/watson-assistant?topic=watson-assistant-gs-dialog).

You use the dialog that you created, and add nodes to the simple dialog that you built as part of the getting started exercise.

## Plan the dialog
{: #tutorial-plan}
{: step}

You are building an assistant for a restaurant that is named *Truck Stop Gourmand* that has one location and a thriving cake-baking business. You want the simple assistant to answer user questions about the restaurant, its menu, and to cancel customer cake orders. Therefore, you need to create intents that handle inquiries related to the following subjects:

- Restaurant information
- Menu details
- Order cancellations

You start by creating intents that represent these subjects, and then build a dialog that responds to user questions about them.

## Answer questions about the restaurant
{: #tutorial-add-about-intent}
{: step}

Add an intent that recognizes when customers ask for details about the restaurant itself. An intent is the purpose or goal that is expressed in user input. The `#General_About_You` intent that is provided with the *General* content catalog serves a similar function, but its user examples are designed to focus on queries about the assistant as opposed to the business that is using the assistant to help its customers. So, you add your own intent.

### Add the #about_restaurant intent
{: #tutorial-add-about-restaurant}

1. On the **Intents** page, click **Create intent**.

1. Add the following intent name, and then click **Create intent**:

   ```text
   about_restaurant
   ```
   {: screen}

   The #about_restaurant intent is added. A number sign (`#`) prefix is added to the intent name to label it as an intent. This naming convention helps you and others recognize the intent as an intent. It has no example user utterances that are associated with it yet.

1. In the **Add user examples** field, enter the following utterances:

   ```text
   Tell me about the restaurant
   i want to know about you
   who are the restaurant owners and what is their philosophy?
   What's your story?
   Where do you source your produce from?
   Who is your head chef and what is the chef's background?
   How many locations do you have?
   do you cater or host functions on site?
   Do you deliver?
   Are you open for breakfast?
   ```
   {: screen}

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) to finish adding the `#reservation` intent and its example utterances.

You added an intent and provided examples of utterances that real users might enter to trigger this intent.

### Add a dialog node that is triggered by the #about_restaurant intent
{: #tutorial-trigger-about-intent}

Add a dialog node that recognizes when the user input maps to the intent that you created in the previous step, meaning its condition checks whether your assistant recognized the `#about_restaurant` intent from the user input.

1. Click **Dialog** to open the dialog tree.

1. Find the **#General_Greetings** node in the dialog tree.

   You will add a node that checks for questions about the restaurant after this initial greeting node to reflect the flow you might expect to encounter in a normal conversation. For example, `Hello.` then `Tell me about yourself.`

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **Greet customers** node, and then select **Add node below**.

1. Start typing `#about_restaurant` in the **If assistant recognizes** field, and then select it from the list.
   
   This node is used if the user input matches the `#about_restaurant` intent.

1. In **Assistant responds**, enter the text response:

   ```text
   Truck Stop Gourmand is the brainchild of Gloria and Fred Smith. What started out as a food truck in 2004 has expanded into a thriving restaurant. We now have one brick-and-mortar restaurant in downtown Portland. The bigger kitchen brought with it new chefs, but each one is faithful to the philosophy that made the Smith food truck so popular to begin with: deliver fresh, local produce in inventive and delicious ways. Join us for lunch or dinner seven days a week. Or order a cake from our bakery.
   ```
   {: codeblock}

Add an image to the response also. 

1. Click **Add response type**.

1. Select **Image** from the drop-down list. In the **Image source** field, add `https://www.ibmlearningcenter.com/wp-content/uploads/2018/02/IBM-Learning-Center-Food4.jpg`.

1. Move up the image response type, so it is displayed in the response before the text is displayed. Click the **Move up** arrow ![Move up arrow](images/move-up-arrow.svg) to reorder the two response types.

   ![Shows the image response type listed before the text response type.](images/gs-ass-image-response-type.png){: caption="Image before text response and response" caption-side="bottom"}

1. Click the close icon ![Close](images/close-x.svg) to close the node edit view.

### Test the #about_restaurant dialog node
{: #tutorial-test-about-intent}

Test the intent by checking whether user utterances that are similar to, but not the same as, the examples you added have trained your assistant to recognize input with an `#about_restaurant` intent.

1. Click **Try it**.

1. Type `I want to learn more about your restaurant.`

   Your assistant indicates that the `#about_restaurant` intent is recognized, and returns a response with the image and text that you specified for the dialog node.

   ![Shows the Try it out pane recognizing the #about_restaurant intent and showing the image and text response.](images/gs-ass-test-about-restaurant.png){: caption="Try it out" caption-side="bottom"}

You added a custom intent, and a dialog node that knows how to handle it.

The `#about_restaurant` intent is designed to recognize various general questions about the restaurant. You added a single node to capture such questions. The response is long, but it is a single statement that can potentially answer questions about all of the following topics:

- Restaurant owners
- Restaurant history
- Philosophy
- Number of sites
- Days of operation
- Meals served
- The restaurant bakes cakes to order

For general questions, a single, general answer is suitable.

## Answer questions about the menu
{: #tutorial-menu}
{: step}

A key question from potential restaurant customers is about the menu. The Truck Stop Gourmand restaurant changes the menu daily. In addition to its standard menu, it has vegetarian and cake shop menus. When a user asks about the menu, the dialog needs to find out which menu to share, and then provide a link to the menu on the restaurant's website. You never want to hardcode information into a dialog node if that information changes regularly.

### Add a #menu intent
{: #tutorial-add-menu-intent}

1. On the **Intents** page, click **Create intent**.

1. Add the following intent name, and then click **Create intent**:

   ```text
   menu
   ```
   {: screen}

1. In the **Add user examples** field, enter the following utterances:

   ```text
   I want to see a menu
   What do you have for food?
   Are there any specials today?
   where can i find out about your cuisine?
   What dishes do you have?
   What are the choices for appetizers?
   do you serve desserts?
   What is the price range of your meals?
   How much does a typical dish cost?
   tell me the entree choices
   Do you offer a prix fixe option?
   ```
   {: screen}

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) icon to finish adding the `#menu` intent and its example utterances.

### Add a dialog node that is triggered by the #menu intent
{: #tutorial-trigger-menu-intent}

Add a dialog node that recognizes when the user input maps to the intent that you created in the previous step, meaning its condition checks whether your assistant recognized the `#menu` intent from the user input.

1. Click **Dialog** to open the dialog tree.

1. Find the **#about_restaurant** node in the dialog tree.

   You will add a node that checks for questions about the menu after this node.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#about_restaurant** node, and then select **Add node below**.

1. Start typing `#menu` in the **If assistant recognizes** field, and then select it from the list.
   
   This node is used if the user input matches the `#menu` intent.

1. In **Assistant responds**, enter the text response:

   ```text
   In keeping with our commitment to giving you only fresh local ingredients, our menu changes daily to accommodate the produce we pick up in the morning. You can find today's menu on our website.
   ```
   {: codeblock}

1. Add an *option* response type that provides a list of options for the user to choose from. In this case, the list of options includes the different versions of the menu that are available. Click **Add response type**. 

1. Select **Option** from the drop-down list.

1. In the **Title** field, add `Which menu do you want to see?`.

1. Click **Add option**.

1. In the **List label** field, add `Standard`. The text that you add as the label is displayed in the response to the user as a selectable option.

1. In the **Value** field, add `standard menu`. The text that you specify as the value is what gets sent to your assistant as new user input when a user chooses this option from the list, and clicks it.

1. Repeat the previous two steps to add label and value information for the remaining menu types:

   | List label | Value |
   | --- | --- |
   | Vegetarian | vegetarian menu | 
   | Cake shop | cake shop menu |
   {: caption="Menu options" caption-side="bottom"}

   ![Shows the options list filled in with menu types.](images/gs-ass-options-list.png){: caption="Options response" caption-side="bottom"}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

### Add a @menu entity
{: #tutorial-add-menu-entity}

To recognize the different types of menus that customers indicate they want to see, you add a `@menu` entity. Entities represent a class of object or a data type that is relevant to a user's purpose. By checking for the presence of specific entities in the user input, you can add more responses, each one tailored to address a distinct user request. In this case, you add a `@menu` entity that can distinguish among different menu types.

1. Click **My entities** to open the Entities page.

1. Click **Create entity**.

1. Enter `menu` into the entity name field.

1. Click **Create entity**.

1. Add `standard` to the **Value name** field, and then add `standard menu` to the **Synonyms** field, and press Enter.

1. Add the following additional synonyms:

   - `bill of fare`
   - `cuisine`
   - `carte du jour`

   ![Shows the standard value being added to the @menu entity.](images/gs-ass-add-standard-value.png){: caption="@menu entity" caption-side="bottom"}

1. Click **Add value** to add the `@menu:standard` value.

1. Add `vegetarian` to the **Value name** field, and then add `vegetarian menu` to the **Synonyms** field, and press Enter.

1. Add the following additional synonyms:

   - `vegan diet`
   - `vegan`
   - `plants-only`

1. Click **Add value** to add the `@menu:vegetarian` value.

1. Add `cake` to the **Value name** field, and then add `cake menu` to the **Synonyms** field, and press Enter.

1. Add the following additional synonyms:

   - `cake shop menu`
   - `dessert menu`
   - `bakery offerings`

1. Click **Add value** to add the `@menu:cake` value.

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) to finish adding the `@menu` entity.

### Add child nodes that are triggered by the @menu entity types
{: #tutorial-trigger-menu-entity}

In this step, you add child nodes to the dialog node that checks for the `#menu` intent. Each child node shows a different response depending on the `@menu` entity type that the user chooses from the options list.

1. Click **Dialog** to open the dialog tree.

1. Find the **#menu** node in the dialog tree.

   You add a child node to handle each menu type option that you added to the **#menu** node.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#menu** node, and then select **Add child node**.

1. Start typing `@menu:standard` in the **If assistant recognizes** field, and then select it from the list.

   This node is used if the user input matches the `@menu:standard` entity.

1. In **Assistant responds**, enter the text response:

   ```text
   To see our menu, go to the <a href="https://www.example.com/menu.html" target="blank">menu</a> page on our website.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **@menu:standard** node, and then select **Add node below**.
 
1. Start typing `@menu:vegetarian` into the **If assistant recognizes** field of this node, and then select it from the list.

1. In **Assistant responds**, enter the text response:

   ```text
   To see our vegetarian menu, go to the <a href="https://www.example.com/vegetarian-menu.html" target="blank">vegetarian menu</a> page on our website.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **@menu:vegetarian** node, and then select **Add node below**.

1. Start typing `@menu:cake` into the **If assistant recognizes** field of this node, and then select it from the list.

1. In **Assistant responds**, enter the text response:

   ```text
   To see our cake shop menu, go to the <a href="https://www.example.com/menu.html" target="blank">cake shop menu</a> page on our website.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

![Shows the child nodes after the #menu node](images/gs-ass-reordered-menu-nodes.png){: caption="@menu nodes" caption-side="bottom"}

You added nodes that recognize user requests for menu details. Your response informs the user that three types of menus available, and asks them to choose one. When the user chooses a menu type, a response is displayed that provides a hypertext link to a web page with the requested menu details.

### Test the menu options dialog nodes
{: #tutorial-test-menu-options-intent}

Test the dialog nodes that you added to recognize menu questions.

1. Click **Try it**.

1. Type `What type of food do you serve?`

   Your assistant indicates that the `#menu` intent is recognized, and displays the list of menu options for the user to choose from.

   ![Shows the Try it out pane when the user input triggers the #menu intent and the options response.](images/gs-ass-test-menu-intent.png){: caption="Try it out" caption-side="bottom"}

1. Click the `Cake shop` option.

   Your assistant recognizes the `#menu` intent and `@menu:cake` entity reference, and displays the response `To see our cake shop menu, go to the cake shop page on our website.`.

   A new web browser page opens and displays the example.com website.

1. Close the example.com web page.

You added an intent and entity that can recognize user requests for menu details, and can direct users to the appropriate menu.

The `#menu` intent represents a common, key need of potential restaurant customers. Due to its importance and popularity, you added a more complex section to the dialog to address it well.

## Manage cake orders
{: #tutorial-manage-orders}
{: step}

Customers can place orders in person, over the phone, or by using the order form on the website. After the order is placed, users can cancel the order through the virtual assistant. First, define an entity that can recognize order numbers. Then, add an intent that recognizes when users want to cancel a cake order.

### Adding an order number pattern entity
{: #tutorial-add-pattern-entity}

You want the assistant to recognize order numbers, so you create a pattern entity to recognize the unique format that the restaurant uses to identify its orders. The syntax of order numbers that are used by the restaurant's bakery is two uppercase letters followed by 5 numbers. For example, `YR34663`. Add an entity that can recognize this character pattern.

1. Click **My entities** to open the Entities page.

1. Click **Create entity**.

1. Enter `order_number` into the entity name field.

1. Click **Create entity**.

1. Add `order_syntax` to the **Value name** field.

1. Click the down arrow next to **Synonyms** to change the type to **Patterns**.

   ![Shows the user choosing to add a pattern for the entity.](images/gs-ass-add-pattern.png){: caption="Pattern" caption-side="bottom"}

1. Add the following regular expression to the Pattern field: 

   ```text
   [A-Z]{2}\d{5}
   ```
   {: codeblock}
   
1. Click **Add value**.

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) to finish adding the `@order_number` entity.

### Add a cancel order intent
{: #tutorial-cancel-order-intent}

1. On the **Intents** page, click **Create intent**.

1. Add the following intent name, and then click **Create intent**:

   ```text
   cancel_order
   ```
   {: screen}

1. In the **Add user examples** field, enter the following utterances:

   ```text
   I want to cancel my cake order
   I need to cancel an order I just placed
   Can I cancel my cake order?
   I'd like to cancel my order
   There's been a change. I need to cancel my bakery order.
   please cancel the birthday cake order I placed last week
   The party theme changed; we don't need a cake anymore
   that order i placed, i need to cancel it.
   ```
   {: screen}

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) to finish adding the `#cancel_order` entity.

### Add a yes intent
{: #tutorial-yes-intent}

Before you complete a task on the user's behalf, you must get confirmation that you are taking the proper action. Add a #yes intent to the dialog that can recognize when a user agrees with what your assistant is proposing.

1. On the **Intents** page, click **Create intent**.

1. Add the following intent name, and then click **Create intent**:

   ```text
   yes
   ```
   {: screen}

1. In the **Add user examples** field, enter the following utterances:

   ```text
   Yes
   Correct
   Please do.
   You've got it right.
   Please do that.
   that is correct.
   That's right
   yeah
   Yup
   Yes, I'd like to go ahead with that.
   ```
   {: screen}

1. Click the **Close** arrow ![Close arrow](images/arrow--left.svg) to finish adding the `#yes` intent.

### Add dialog nodes that can manage requests to cancel an order
{: #tutorial-cancel-order-dialog}

Now, add a dialog node that can handle requests to cancel a cake order.

1. Click **Dialog** to open the dialog tree.

1. Find the **#menu** node in the dialog tree.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#menu** node, and then select **Add node below**.

1. Start typing `#cancel_order` into the **If assistant recognizes** field of this node, then select it from the list.

1. In **Assistant responds**, enter the text response:

   ```text
   If the pickup time is more than 48 hours from now, you can cancel your order.
   ```
   {: codeblock}

Before you can cancel the order, you need to know the order number. The user might specify the order number in the original request. So, to avoid asking for the order number again, check for a number with the order number pattern in the original input. To do so, define a context variable that would save the order number if it is specified.

1. In **Assistant responds**, click the **Options** icon ![More options](images/overflow-menu--vertical.svg) icon, and then select **Open context editor**.

1. Set the context by using these values:

   | Variable | Value |
   | --- | --- |
   | `$ordernumber` | `<? @order_number.literal ?>` |
   {: caption="Order number context variable details" caption-side="bottom"}

   The context variable value (`<? @order_number.literal ?>`) is a SpEL expression that captures the number that the user specifies that matches the pattern that is defined by the @order_number pattern entity. It saves it to the `$ordernumber` variable.

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Now, add child nodes that either ask for the order number or get confirmation from the user that they want to cancel an order with the detected order number.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#cancel_order** node, and then select **Add child node**.

1. Add a label to the node to distinguish it from other child nodes you are adding. In the **Enter node name** field, add `Ask for order number`. 

1. In **If assistant recognizes**, enter `true` as the condition. 

1. In **Assistant responds**, enter the text response:

   ```text
   What is the order number?
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Now, add another child node that informs the user that you are canceling the order.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **Ask for order number** node, and then select **Add child node**.

1. In **If assistant recognizes**, enter `@order_number` as the condition. 

1. In **Assistant responds**, click the **Options** icon ![More options](images/overflow-menu--vertical.svg) icon, and then select **Open context editor**.

1. Set the context by using these values:

   | Variable | Value |
   | --- | --- |
   | `$ordernumber` | `<? @order_number.literal ?>` |
   {: caption="Order number context variable details" caption-side="bottom"}

1. In **Assistant responds**, enter the text response:

   ```text
   OK. The order $ordernumber is canceled. We hope we get the opportunity to bake a cake for you sometime soon.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Add another node to capture the case where a user provides a number, but it is not a valid order number. 

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **@order_number** node, and then select **Add node below**.

1. In **If assistant recognizes**, enter `true` as the condition. 

1. In **Assistant responds**, enter the text response:

   ```text
   I need the order number to cancel the order for you. If you don't know the order number, please call us to cancel over the phone.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Add a node after the initial order cancellation request node that responds in the case where the user provides the order number in the initial request, so you don't have to ask for it again. 

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#cancel_order** node, and then select **Add child node**.

1. Add a label to the node to distinguish it from other child nodes. In the **Enter node name** field, add `Number provided`. 

1. In **If assistant recognizes**, enter `@order_number` as the condition. 

1. In **Assistant responds**, enter the text response:

   ```text
   Just to confirm, you want to cancel order $ordernumber?
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

You must add child nodes that check for the user's response to your confirmation question.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **Number provided** node, and then select **Add child node**.

1. In **If assistant recognizes**, enter `#yes` as the condition. 

1. In **Assistant responds**, enter the text response:

   ```text
   OK. The order $ordernumber is canceled. We hope we get the opportunity to bake a cake for you sometime soon.
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#yes** node, and then select **Add node below**.

1. In **If assistant recognizes**, enter `true` as the condition. 

Don't add a response to **Assistant responds**. Instead, you redirect users to the branch that asks for the order number details that you created earlier.

1. In **Then assistant should** choose **Jump to**.

1. Select the **Ask for order number** node.

1. Choose **If assistant recognizes (condition)**.

   ![Shows choosing the Ask for order number node condition as the jump to target.](images/gs-ass-true-jump-to-destination.png){: caption="Jump to" caption-side="bottom"}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Force the conversation to evaluate the child nodes under the *#cancel_order* node at run time. 

1. Click to open the `#cancel_order` node in the edit view.

1. In **Then assistant should** select `Skip user input`.

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

### Test order cancellations
{: #tutorial-test-cancel-order}

Test whether your assistant can recognize character patterns that match the pattern that is used for product order numbers in user input.

1. Click **Try it**.

1. Type `i want to cancel my order number TW12345.`

   Your assistant recognizes both the `#cancel_order` intent and the `@order_number` entity. It responds with, `If the pickup time is more than 48 hours from now, you can cancel your order. Just to confirm, you want to cancel order TW12345?`.

1. Type `Yes`.

   Your assistant recognizes the `#yes` intent and responds with, `OK. The order TW12345 is canceled. We hope we get the opportunity to bake a cake for you sometime soon.`.

   ![Shows the Try it out pane test of the cancel order number node when the user provides the order number in the initial input.](images/gs-ass-test-cancel-order-number-provided.png){: caption="Try it out" caption-side="bottom"}

   Now, try it when you don't know the order number.

1. Click **Clear** in the "Try it out" pane to start over. 

1. Type `I want to cancel my order.`

   Your assistant recognizes the `#cancel_order` intent, and responds with, `If the pickup time is more than 48 hours from now, you can cancel your order. What is the order number?`.

1. Enter, `I don't know.`

   Your assistant responds with, `I need the order number to cancel the order for you. If you don't know the order number, please call us to cancel over the phone.`.

### Add nodes to clarify the order number format
{: #tutorial-clarify-order-number-format}

If you do more testing, you might find that the dialog isn't helpful in scenarios where the user does not remember the order number format. The user might include only the numbers or the letters too, but forget that they are meant to be uppercase. So, it would be a nice touch to give them a hint in such cases, correct? If you want to be kind, add another node to the dialog tree that checks for numbers in the user input.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **@order_number** node, and then select **Add node below**.

1. In **If assistant recognizes**, enter `input.text.find('\d')` as the condition. 

1. In the condition field, add `input.text.find('\d')`, which is a SpEL expression that says if you find one or more numbers in the user input, trigger this response.

1. In **Assistant responds**, enter the text response:

   ```text
   The correct format for our order numbers is AAnnnnn. The A's represents 2 uppercase letters, and the n's represent 5 numbers. Do you have an order number in that format?
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **input.text.find('\d')** node, and then select **Add child node**.

1. In **If assistant recognizes**, enter `true` as the condition. 

1. Click **Customize**, set the **Multiple conditioned responses** switch to **On**, and then click **Apply**.

1. In **Assistant responds, add responses with the following conditions:

   | If assistant recognizes | Assistant responds | Then assistant should |
   | --- | --- | --- |
   | `@order_number` | `OK. The order $ordernumber is canceled. We hope we get the opportunity to bake a cake for you sometime soon.` | Default to node settings |
   | `true` | `I need the order number to cancel the order for you. If you don't know the order number, please call us to cancel over the phone.` |
   {: caption="Condition details" caption-side="bottom"}

   ![Shows the addition of a node that checks for numbers in the user input and responds with a hint about the order number format.](images/gs-ass-give-hint.png){: caption="Condition details" caption-side="bottom"}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

Now, when you test, you can provide a set of numbers or a mix of numbers and text as input, and the dialog reminds you of the correct order number format. You tested your dialog, found a weakness in it, and corrected it.

Another way that you can address this type of scenario is to add a node with slots. See the [Adding a node with slots to a dialog](/docs/watson-assistant?topic=watson-assistant-tutorial-slots) tutorial to learn more about using slots.
{: tip}

## Add the personal touch
{: #tutorial-get-username}
{: step}

If the user shows interest in the bot itself, you want the virtual assistant to recognize that curiosity and engage with the user in a more personal way. You might remember the `#General_About_You` intent, which is provided with the *General* content catalog, that we considered using earlier before you added your own custom `#about_restaurant` intent. It is built to recognize such questions from the user. Add a node that conditions on this intent. In your response, you can ask for the user's name and save it to a $username variable that you can use elsewhere in the dialog, if available.

### Add a node that handles questions about the bot
{: #tutorial-add-about-you-node}

Add a dialog node that can recognize the user's interest in the bot, and respond.

1. Click **Dialog** to open the dialog tree.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **Welcome** node, and then select **Add node below**.

1. Start typing `#General_About_You` in the **If assistant recognizes** field, and then select it from the list.

1. In **Assistant responds**, enter the text response:

   ```text
   I am a virtual assistant that is designed to answer your questions about the Truck Stop Gourmand restaurant. What should I call you?
   ```
   {: codeblock}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

1. Click the Node options icon ![Node options](images/overflow-menu--vertical.svg) on the **#General_About_You** node, and then select **Add child node**.

1. In **If assistant recognizes**, enter `true` as the condition.

1. In **Assistant responds**, enter the text response:

   ```text
   Hello, <? input.text ?>! It's lovely to meet you. How can I help you today?
   ```
   {: codeblock}

To capture the name that the user provides, add a context variable to the node. 

1. In  **Assistant responds**, click the options menu ![Options](images/overflow-menu--vertical.svg) and select **Open context editor**.

1. Set the context by using these values:

   | Variable | Value |
   | --- | --- |
   | `$username` | `"<? input.text ?>"` |
      {: caption="Set context" caption-side="bottom"}

   The context variable value (`<? input.text ?>`) is a SpEL expression that captures the username as it is specified by the user, and then saves it to the `$username` context variable.

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

If at run time, the user triggers this node and provides a name, then you record the user's name. If you know it, you should use it! Add conditional responses to the greeting dialog node that you added previously to include a conditional response that uses the username, if it is known.

### Add the username to the greeting
{: #tutorial-add-username-to-greeting}

If you know the user's name, you should include it in your greeting message. To do so, add conditional responses, and include a variation of the greeting that includes the user's name.

1. Find the **Greet customers** node in the dialog tree, and click to open it in the edit view.

1. Click **Customize**, set the **Multiple conditioned responses** switch to **On**, and then click **Apply**.

1. Click **Add response**.

1. In  **If assistant recognizes**, enter `$username`.

1. In **Respond with**, enter a text response:

   ```text
   Good day to you, $username!
   ```
   {: codeblock}

1. Click the **Move up** arrow ![Move up arrow](images/move-up-arrow.svg) to reorder the two response types.

   ![Shows the existing response is now part of a table of responses.](images/gs-ass-mcr-response-added.png){: caption="Move up response" caption-side="bottom"}

1. Click the **Close** icon ![Close](images/close-x.svg) to close the node edit view.

### Test personalization
{: #tutorial-test-personalize}

Test whether your assistant can recognize and save a user's name, and then refer to the user by it later.

1. Click **Try it**.

1. Click **Clear** to restart the conversation session.

1. Enter `Who are you?`

   Your assistant recognizes the `#General_About_You` intent. Its response ends with the question, `What should I call you?`.

1. Enter `Jane`.

   Your assistant saves `Jane` in the `$username` variable and responds `Hello, Jane! It's lovely to meet you. How can I help you today?`.

1. To test the `Greet customers` node, enter `Hello.`.

   Your assistant recognizes the `Greet customers` intent and says, `Good day to you, Jane!`. It uses the conditional response that includes the user's name because the `$username` context variable contains a value at the time that the greeting node is triggered.

You can add a conditional response that conditions on and includes the user's name for any other responses where personalization would add value to the conversation.

## Summary
{: #tutorial-summary}

You created a more complex dialog that reacts to questions and requests from the customer.
