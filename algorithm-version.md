---

copyright:
  years: 2015, 2022
lastupdated: "2022-10-21"

subcollection: assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:preview: .preview}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:gif: data-image-type='gif'}

# Algorithm version
{: #algorithm-version}

The **Algorithm version** setting allows you to choose which {{site.data.keyword.conversationshort}} algorithm to apply to your future trainings.
{: shortdesc}

There are three choices:
- **Beta**: Use this to preview and test what is coming. The capability in the beta version at any given time is likely to become a supported version later on. It's not recommended to use the beta version in a production deployment.
- **Latest**: The current supported version that's recommended for your live production assistant. 
- **Previous**: The last supported before the latest version. Support for this version ends when the next version is released.

To choose an algorithm version for actions:

1. On the **Actions** page, click **Global settings** ![Gear icon](images/gear-icon-black.png).

1. Click the **Algorithm Version** tab.

1. Choose a version, then click **Save**.

To choose an algorithm version for dialog:

1. On the **Dialog** page, open the **Options** section.

1. Click **Algorithm Version**.

1. Choose a version.

The latest and previous versions have date labels such as **Latest (01-Jun-2022)** or **Previous (01-Jan-2022)**. See the [{{site.data.keyword.conversationshort}} release notes](/docs/watson-assistant?topic=watson-assistant-watson-assistant-release-notes) for details about each algorithm version release.

Algorithm version choices are currently available for Arabic, Chinese (Simplified), Chinese (Traditional), Czech, Dutch, English, French, German, Japanese, Korean, Italian, Portuguese, and Spanish. The universal language model uses a default algorithm.
