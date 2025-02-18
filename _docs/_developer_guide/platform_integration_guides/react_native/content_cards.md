---
nav_title: Content Cards
article_title: Content Cards for React Native
platform: React Native
page_order: 3
page_type: reference
description: "This article covers how to get started with Content Cards for React Native apps."
channel: content cards

---

# Content Card integration

> This article covers how to set up Content Cards for React Native.

The Braze SDKs include a default card feed to get you started with Content Cards. To show the card feed, you can use the `Braze.launchContentCards()` method. The default card feed included with the Braze SDK will handle all analytics tracking, dismissals, and rendering for a user's Content Cards.

## Customization

To build your own UI, you can get a list of available cards, and listen for updates to cards:

```javascript
// set initial cards
const [cards, setCards] = useState([]);

// listen for updates as a result of card refreshes
Braze.addListener(Braze.Events.CONTENT_CARDS_UPDATED, async (update) => {
    const updatedCards = await Braze.getContentCards();
    setCards(updatedCards);
});

// trigger a refresh of cards
Braze.requestContentCardsRefresh();
```

{% alert important %}
If you choose to build your own UI to display cards, you must call `logContentCardImpression` in order to receive analytics for those cards.
{% endalert %}

You can use these additional methods to build a custom Content Cards Feed within your app:

| Method                                         | Description                                                                                            |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `Braze.requestContentCardsRefresh()`     | Requests the latest Content Cards from the Braze SDK server.                                           |
| `Braze.getContentCards()`                | Retrieves Content Cards from the Braze SDK. This will return the latest list of cards from the server. |
| `Braze.logContentCardClicked(cardId)`    | Logs a click for the given Content Card ID.                                                            |
| `Braze.logContentCardImpression(cardId)` | Logs an impression for the given Content Card ID.                                                      |
| `Braze.logContentCardDismissed(cardId)`  | Logs a dismissal for the given Content Card ID.                                                        |
{: .reset-td-br-1 .reset-td-br-2}

## Test displaying sample Content Card

Follow these steps to test a sample Content Card.

1. Set an active user in the React application by calling the [`Braze.changeUser('your-user-id')`](https://js.appboycdn.com/web-sdk/latest/doc/modules/braze.html#changeuser) method.
2. Head to **Campaigns** and follow [this guide][4] to create a new Content Card campaign.
3. Compose your test Content Card campaign and head over to the **Test** tab. Add the same `user-id` as the test user and click **Send Test**. You should be able to launch a Content Card on your device shortly.

![A Braze Content Card campaign showing you can add your own user ID as a test recipient to test your Content Card.][5]

For more integrations, follow the [Android integration instructions][2] or the [iOS integration instructions][3], depending on your platform.

A sample implementation of this can be found in BrazeProject within the [React SDK][1].

[1]: https://github.com/braze-inc/braze-react-native-sdk
[2]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/content_cards/data_models/
[3]: https://braze-inc.github.io/braze-swift-sdk/tutorials/braze/c2-contentcardsui
[4]: {{site.baseurl}}/user_guide/message_building_by_channel/content_cards/create
[5]: {% image_buster /assets/img/react-native/content-card-test.png %} "Content Card Campaign Test"
