---

copyright:
  years: 2019, 2023
lastupdated: "2023-10-26"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}


# Controlling the web chat version
{: #web-chat-develop-versions}

The web chat JavaScript code follows semantic versioning practices. Starting with web chat version 2.0.0, you can set the version of the web chat that you want to use as a configuration option.

If you don't specify a version, the latest version is used automatically (`clientVersion: "latest"`). When you apply the latest version, you benefit from the continuous improvements, feature additions, and bug fixes that are made to the web chat regularly.

However, if you apply extensive customizations to your deployment, such as overriding the theme with your own custom theme, you might want to lock your deployment to a specific version. Locking on a version enables you to test new versions before you apply them to your live web chat.

To use a specific version (`clientVersion: "major.minor.patch"`), specify it as follows:

The following examples show what to specify when the current version is `2.3.1`.

- If you want to stay on a major version, but get the latest minor and patch releases, specify `clientVersion: "2"`.
- If you want to stay on a minor version, but get the latest patch releases, specify `clientVersion: "2.3"`. 
- If you want to lock on to a specific minor version and patch release, specify `clientVersion: "2.3.1"`.

To test the updates in a version release of the web chat before you apply the version to your live web chat, follow these steps:

1.  Lock the web chat that is running in your production environment to a specific version. 
1.  Embed your web chat deployment into a new page in a test environment, and then override the version lock setting. For example, specify `clientVersion: "latest"`.
1.  Test the web chat, and make adjustments to the configuration if necessary.
1.  Update your production deployment to use the latest version and apply any other configuration changes that you determined to be necessary after testing.

For more information about features that were introduced in previous web chat versions, see the [Web chat release notes](/docs/watson-assistant?topic=watson-assistant-release-notes-chat).

