# Tutorial - Create a digital business card with Flex Message Simulator

Flex Messages are messages that can be freely customized based on [CSS Flexible Box (CSS Flexbox)](https://www.w3.org/TR/css-flexbox-1/). Depending on your needs, you can adjust the size of the message, allocate text, images, and icons in specific locations, and add interactive buttons.

In this tutorial, you'll learn how to use [Flex Message Simulator](https://developers.line.biz/flex-simulator/) to create a digital business card. Flex Message Simulator is a tool to help you brainstorm, design, and prototype Flex Messages **without writing code**. If you are new to Flex Messages, see [Sending Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/) first.

## Goal 

The outcome of this tutorial is a digital business card as shown below. You can see the outcome defined in JSON from this [download link](https://developers.line.biz/media/code-samples/flex-message-simulator-example.json). But we recommend that you to go through this tutorial to become familiar with Flex Message Simulator. We guarantee, this tool will become quite handy to deal with a limitless number of use cases for Flex Messages.

![Final Output](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-final-output.png)

## Before you start 

To follow this tutorial, we recommend that you read [Messaging API overview](https://developers.line.biz/en/docs/messaging-api/overview/) and [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/), before you get started. Also, read on this section to learn about Flex Message Simulator if you are new to the simulator. If you're familiar with the simulator, [start with the tutorial](https://developers.line.biz/en/docs/messaging-api/using-flex-message-simulator/#select-flex-message) right now.

### Learn about Flex Message Simulator 

Flex Message Simulator is a tool with which you can compose and preview a Flex Message. You don't have to set up a development environment or write code to compose Flex Messages and send Flex Messages to preview.

First, open [Flex Message Simulator](https://developers.line.biz/flex-simulator/). If you aren't logged in to the [LINE Developers Console](https://developers.line.biz/console/), you're prompted to log in. If you have a LINE Developers account, log in with your account. If not, click **Create an account** and create one.

The UI of Flex Message Simulator has three areas:

- **Preview area**: Displays the Flex Message generated with the data specified in the tree view area and property area.
- **Tree view area**: Displays and lets you edit the data structure of the Flex Message.
- **Property area**: Lets you set the properties of the item selected in the tree view area. The simulator uses the data entered here to generate a Flex Message.

![Flex Message Areas](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-areas.png)

If you hover your mouse over an item in the tree view area, the corresponding area is highlighted in the preview area. See this in action from the video.

<video width="883" height="381" controls>
  <source src="https://vos.line-scdn.net/line-developers/docs/media/video/flex-message-simulator.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

#### You can use Flex Message layout presets 

Flex Message Simulator offers predefined Flex Message layouts.

To use a predefined layout, click **Showcase** at the top of the simulator. Once you make a choice, click **Create**.

<!-- note start -->

**About layout**

In this tutorial, we don't use a predefined layout. We'll create a Flex Message from scratch.

<!-- note end -->

![Flex Message Simulator Showcase](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/showcase.png)

#### You can copy the Flex Message in JSON 

To copy a Flex Message generated in JSON, click **</>View as JSON** and then the **Copy** button.

![View as JSON](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/view-as-json.png)

## Tutorial shortcut 

To skip reading through the instructions and jump right to preview the outcome, [download](https://developers.line.biz/media/code-samples/flex-message-simulator-example.json) the Flex Message object in JSON. To preview the outcome in Flex Message Simulator:

1. Click **</>View as JSON**. A modal with JSON data is displayed.
1. Remove the content in the modal.
1. Copy and paste the content of the downloaded JSON file into the modal.
1. Click **Apply** to save the change. The preview area shows the Flex Message we pasted in.

![Preview Flex Message created from sample JSON data](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-confirm-example-code-output.png)

## 1. Select container type 

Now that we learnt about Flex Message Simulator, let's get started to create a digital business card. We only need one bubble to create a business card, so we'll set our Flex Message container to the [bubble type](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#bubble).

To create a bubble container, click **New** and select **bubble** from the drop-down menu.

![Select Bubble Type Container](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/select-bubble-type.png)

<!-- tip start -->

**Tip**

When you select **bubble** from the drop-down menu, an "OK" message pops up at the bottom of the preview area. This means that your update is successfully reflected in the preview area.

![Select Message Type](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/type.png)

<!-- tip end -->

For more information about the types of containers, see [container](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#container).

## 2. Add a header 

In the container we created, let's add a header to show the company name. A header is a type of a [block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block) and so are hero, body, and footer. Header is mainly used to display the message subject or content heading.

![Block style example](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/elements.png)

1. To add a header, select the **header** node in the tree view area. Click **+** at the top and click **box**.
1. Set the background color of the header. In the property area, set the **backgroundColor** field with hexadecimal color code, `#00B900` in this tutorial, and hit the Enter key. Now the header is visually distinguishable from the body block.

   <!-- tip start -->

   **Hit the Enter key to apply your entry**

   Whenever you add or select a property in the property area, hit the Enter key to apply your entry in the preview area. Then you can see the result in the preview area. From this point onward in this tutorial, we'll omit this instruction to not overwhelm you.

   <!-- tip end -->

   ![Set Header Background Color](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/set-header-color.png)

1. Add a text in the header:
   1. From the tree view, click the **box [vertical]** node under **header**.

      <!-- tip}

      Vertical box is one of the box types for Flex Messages, that determines how the box's child components are placed within the box. For more information, see [Box component orientation](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#box-component-orientation).

      ::

   1. Click **+** in the tree view and then **text** from the drop-down menu. A **text** node is created under the **box [vertical]** node.
   1. Click the text node from the tree view.
   1. In the property area, replace "hello, world" in the **text** field with "Flex Message Corp".

We made the header distinguishable with the new background color, but the header text is a bit difficult to read. Let's make the text stand out with a new color and style. In the tree view, click the text node and set the **color** property to `#FFFFFF` and **weight** to `bold`.

Now you should see something like this. We have a distinguishable header with the text clearly visible.

![Add Header Final Output](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-header-final.png)

## 3. Add an image 

One way to supplement our a digital business card visually is to add an image. With Flex Message Simulator, adding or styling an image can't get easier. To add an image, we'll use the [hero block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block) which is mainly used to display image type content.

1. In the tree view, click the **hero** node.
2. Click **+** and then **image** from the drop-down list. A default image is displayed in the preview.
3. To change the image, click the **image** node from the tree view. In the property area, change the value of the **url** property to the location for your image. Your image must be in portrait mode. For the tutorial, you can use [this](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/mary.png) start -->

      **Image requirements**

   You can't upload image files to Flex Message Simulator. Specify a URL to an image that is uploaded on the web. The image and the image URL must satisfy these conditions:
   - Protocol: HTTPS (TLS 1.2 or later)
   - Image format: JPEG or PNG
   - Max image size: 1024 x 1024 px
   - Max file size: 10 MB

   <!-- tip}

      Vertical box is one of the box types for Flex Messages, that determines how the box's child components are placed within the box. For more information, see [Box component orientation](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#box-component-orientation).

      ::

   1. Click **+** in the tree view and then **text** from the drop-down menu. A **text** node is created under the **box [vertical]** node.
   1. Click the text node from the tree view.
   1. In the property area, replace "hello, world" in the **text** field with "Flex Message Corp".

We made the header distinguishable with the new background color, but the header text is a bit difficult to read. Let's make the text stand out with a new color and style. In the tree view, click the text node and set the **color** property to `#FFFFFF` and **weight** to `bold`.

Now you should see something like this. We have a distinguishable header with the text clearly visible.

![Add Header Final Output](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-header-final.png)

## 3. Add an image 

One way to supplement our a digital business card visually is to add an image. With Flex Message Simulator, adding or styling an image can't get easier. To add an image, we'll use the [hero block](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/#block) which is mainly used to display image type content.

1. In the tree view, click the **hero** node.
2. Click **+** and then **image** from the drop-down list. A default image is displayed in the preview.
3. To change the image, click the **image** node from the tree view. In the property area, change the value of the **url** property to the location for your image. Your image must be in portrait mode. For the tutorial, you can use [this](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/mary.png) end -->

   <!-- tip start -->

   **File size recommendation**

   To display a message without delay, we recommend that you keep the size of each image file to 1 MB or less.

   <!-- tip end -->

The image is changed successfully, but the image looks a little small compared to the background. Let's make the image bigger.

![Add Image](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-image.png)

To change the image size, click the **image** node from the tree view and set the maximum image width in the **size** property. For this tutorial, click the button next to the property's input field and the `xl` keyword from the drop-down list. You _can_ enter a value in pixels or %, instead. For more information, see the "size" property specification for [Image](https://developers.line.biz/en/reference/messaging-api/#f-image).

Now you have a business card with an enlarged image:

![Add Image Final Output](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/add-image-final.png)

## 4. Add a name 

A name in a business card is a must. Presenting key information such as a name in a noticeable style helps. To add a name under the image:

1. In the tree view, click the **box [vertical]** node under **body**.
1. Click **+** and then **text** from the drop-down menu. A text node is created under the box node.
1. Click the **text** node from the tree view.
1. In the property area, replace the "hello, world" in the **text** field with a name.

Like we did with the [header text](https://developers.line.biz/en/docs/messaging-api/using-flex-message-simulator/#add-header), let's style the name text. We want to increase the font size, make the font bold, and center align the text.

- **Size**: Set the **size** property to `xl`. (Default size is "md".)
- **Bold**: Set the **weight** property to `bold`.
- **Center align**: Set the **align** property to `center`.

Now your business card has a name under the image:

![Add Name Final Output](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-name-final.png)

## 5. Add a job title 

Another piece of information as important as a name in a business card is your job title. Let's add a job title under the name.

1. In the tree view, click the **box [vertical]** node under **body**.
1. Click **+** and then **text** from the drop-down menu. A new text node is created.
1. Click the new **text** node from the tree view.
1. In the property area, replace "hello, world" in the **text** field with a job title.

Since we aligned the name to the center, we want to align the job title also to the center. While the text node is selected, set the **align** property to `center`.

Now your business card has a job title:

![Add Job Title Final](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-job-title-final.png)

## 6. Add a separator 

Later on, we'll add buttons to make the business card interactive. Before we do that, let's add a [separator](https://developers.line.biz/en/reference/messaging-api/#separator) to visually separate the information section and interactive section.

1. In the tree view, click the **box [vertical]** node under **body**.
1. Click **+** and then **separator** from the drop-down menu. A separator is created right under the job title.

![Add Separator](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-separator.png)

The gap between the separator and the job title is almost none. Let's give a room between the two by giving a [margin](https://developers.line.biz/en/reference/messaging-api/#separator) to the separator. For more information about margins, see [Separator](https://developers.line.biz/en/reference/messaging-api/#separator) in the Messaging API reference.

1. In the tree view, click the **separator** node.
1. In the property area, set the **margin** property to `md`.

Now you have a separator in your business card with some room:

![Add Separator Final](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-separator-final.png)

## 7. Add buttons 

As mentioned in step 6, we want to add buttons to make our business card interactive. We want to add two buttons under the separator. First, we want a component to group the buttons.

1. Click the **box [vertical]** under **body**.
1. Click **+** and then **box** from the drop-down menu. A box node is created to add buttons to.

We want the buttons to execute an action when pressed. Available action types for buttons are [URI action](https://developers.line.biz/en/reference/messaging-api/#uri-action) and [postback action](https://developers.line.biz/en/reference/messaging-api/#postback-action). For this tutorial, we'll add buttons to:

1. [Jump to the company's website](https://developers.line.biz/en/docs/messaging-api/using-flex-message-simulator/#add-action-1)
1. [Open a registration form made with LIFF](https://developers.line.biz/en/docs/messaging-api/using-flex-message-simulator/#add-action-2)

### 7-1. Add a button to jump to the company's website 

To set a button to open the company's website:

1. In the tree view, click the **box [vertical]** created for the buttons.
1. Click **+** and then **button** from the drop-down menu.
1. Click the **button [action]** node.
1. In the property area, scroll down to the **Action** section. By default, the **type** property is set to `uri`. Since we want to open a website URL, let's keep the value as is.
1. From the **Action** section, set the **label** property to "Visit our website". This becomes the button label.
1. To open a website, set the **uri** property to the URL of your choice.

<!-- note start -->

**Apply percent encoding to the URI**

[Percent-encode](https://en.wikipedia.org/wiki/Percent-encoding) the domain name, path, query parameters, and fragments in the `uri` property, with the UTF-8 encoding. For example, the final URL becomes `https://example.com/path?q=Good%20morning#Good%20afternoon` with these settings:

| Scheme | Domain name | Path  | Query parameter | Fragment       |
| ------ | ----------- | ----- | --------------- | -------------- |
| https  | example.com | /path | q=Good morning  | Good afternoon |

<!-- note end -->

Now we have a button in the business card to open the company website.

![Add URI Action Button](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-uri-button.png)

Like we did in the header text, name, and job title, we want to style the button. To make the tappable area more visible, we can add a color to the button. You can choose from three preset button styles to add the color with:

- **Primary**: Style for dark colored buttons
- **Secondary**: Style for light colored buttons
- **Link**: Renders the button like an HTML text link

We recommend that you use the link style if you have multiple buttons stacked vertically, as in our tutorial. Instead of coloring the background, let's apply the link style to our button:

1. In the tree view, click the **button** node.
1. In the property area, set the **style** property to `link`.

Your button should look something like this:

![Change Button Color](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-change-button-color.png)

### 7-2. Add a button to open a registration form made with LIFF 

Let's continue to add the rest of the buttons. For the second button, we want to add a [LINE Front-end Framework (LIFF)](https://developers.line.biz/en/docs/liff/overview/) URL to the business' registration form. You can create registration forms with LIFF and later send a new message to the user with the information you retrieved from the form. For more information on LIFF, see [Developing a LIFF App](https://developers.line.biz/en/docs/liff/developing-liff-apps/) or [Trying the LIFF starter app](https://developers.line.biz/en/docs/liff/trying-liff-app/).

To create the second button:

1. In the tree view, click the **box [vertical]** node that you created for the first button.
1. Click **+** and then **button** from the drop-down menu. A button node is created.
1. In the property area:
   - Set the **style** property to `link`.
   - Set the **label** property to "Register with us".
   - Keep the **type** property to `uri`.
   - Set the **uri** property to a LIFF app URL.

Now we have the second button set with a LIFF URL:

![Add LIFF Button](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-add-liff-button.png)

### 7-3. Distribute the buttons 

The buttons are stacked very tight to each other. It doesn't look like so, but if you change the button style to primary or secondary, you can tell right away. To distribute the buttons with some room in between, you can use [margin](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#margin-property) or [padding](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/#padding-property) on the parent node, which is a box component for us. For this tutorial, we'll add padding:

1. In the tree view, click the **box [vertical]** that contains the two buttons you created.
1. In the property area, under the **Padding** section, set the **paddingTop** property to `10px`.

Now we have the buttons with more space in between:

![Style Buttons](https://developers.line.biz/media/messaging-api/using-flex-message-simulator/en-style-buttons.png)

This is it. You completed this tutorial to create a digital business card!

## Next steps 

When you compose a Flex Message, export the result in JSON as introduced at the [beginning of this tutorial](https://developers.line.biz/en/docs/messaging-api/using-flex-message-simulator/#copy-json). This is handy when you want to send a Flex Message with the Messaging API. For more information, see [Call the Messaging API to send the Flex Message](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/#sending-messages-with-the-messaging-api).

## Conclusion 

Flex Message Simulator is a simple tool to help you brainstorm, design, and prototype a Flex Message without writing code. Like this tutorial, there are a limitless number of use cases you can use Flex Messages for. Use Flex Message Simulator to conceptualize ideas, test prototypes, and speed up the creation of Flex Messages, without technical barriers. Create unique Flex Messages with Flex Message Simulator!

## Related pages 

- [Send Flex Messages](https://developers.line.biz/en/docs/messaging-api/using-flex-messages/)
- [Flex Message elements](https://developers.line.biz/en/docs/messaging-api/flex-message-elements/)
- [Flex Message layouts](https://developers.line.biz/en/docs/messaging-api/flex-message-layout/)
- [Flex Message](https://developers.line.biz/en/reference/messaging-api/#flex-message) (Messaging API reference)
