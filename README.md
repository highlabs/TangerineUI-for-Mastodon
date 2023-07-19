# Tangerine UI for Mastodon 🍊🐘

A Tangerine redesign for Mastodon's Web UI, using just CSS.
Tangerine UI features a bubblier look, a more compact timeline, round avatars, and a soft color palette.

* [**Live demo** at nileane.fr](https://nileane.fr)
* [**Announcement** post on Mastodon](https://nileane.fr/@nileane/110691663040709608)

* [**Installation** for instance admins](#installation-for-instance-admins)
  * [Install as the only theme](#install-tangerine-ui-as-the-only-theme-on-your-instance)
  * [Install as an optional theme [Recommended]](#install-tangerine-ui-as-an-optional-theme-on-your-instance-recommended)
* [**Installation** for regular users](#installation-for-regular-users)
* [**Things to know**](#things-to-know)
* [**Credits**](#credits)

## Variants

* **Tangerine 🍊**  
  Default variant for Tangerine UI, featuring a soft orange palette.

![Tangerine UI's orange palette, both in dark and light modes.](https://github.com/nileane/TangerineUI-for-Mastodon/assets/914451/5048329b-9d95-4b11-a859-48c1f37d54e6)

* **Purple 🪻**  
  For those of you who like Tangerine UI but want to stick to Mastodon's purple palette.

![Tangerine UI's purple variant, both in dark and light modes.](https://github.com/nileane/TangerineUI-for-Mastodon/assets/914451/c01c7a54-d2db-4fe5-a0f6-dc6e77cfe128)

## Installation for instance admins

### Install Tangerine UI as the only theme on your instance:
* Copy & paste the contents of [`TangerineUI.css`](https://github.com/nileane/TangerineUI-for-Mastodon/blob/main/TangerineUI.css) to the **Custom CSS** field in the administration panel on your Mastodon instance (Navigate to https://*domain*/admin/settings/appearance).
   * 🪻 For the purple variant, copy the contents of [`TangerineUI-purple.css`](https://github.com/nileane/TangerineUI-for-Mastodon/blob/main/TangerineUI-purple.css) instead.
   * ⚠️ **Caution: Using the 'Custom CSS' field to apply Tangerine UI will prevent all users on your instance from being able to choose another theme in their settings.** Please make sure there is a consensus among your users for doing so. Otherwise, see below how to install Tangerine UI as an optional site theme for your users.

### Install Tangerine UI as an optional theme on your instance [Recommended]:
Follow these instructions if you wish to add Tangerine UI as an available theme for your users on your instance. This will also allow you to set Tangerine UI as the default theme for your instance, while still letting users change back to Mastodon's default themes in their appearance settings.

1. Add the files from the [`mastodon`](https://github.com/nileane/TangerineUI-for-Mastodon/tree/main/mastodon/app/javascript/styles) folder in this repository to your Mastodon themes directory:

```
app/
  javascript/
    styles/
    tangerineui.scss                                  | **new**
    tangerineui-purple.scss                           | **new**
      contrast/
        ...
      fonts/
        ...
      tangerineui/                                    | **new**
        layout-single-column.scss                     | **new**
      tangerineui-purple/                             | **new**
        layout-single-column.scss                     | **new**
```


2. **Add Tangerine UI to the config.** To make Tangerine UI available in your users's settings, you need to add a new line to [`config/themes.yml`](https://github.com/tootsuite/mastodon/blob/master/config/themes.yml). Here we're adding 2 new lines, one for Tangerine UI, another for Tangerine UI's purple variant:

```yml
default: styles/application.scss
contrast: styles/contrast.scss
mastodon-light: styles/mastodon-light.scss
tangerineui: styles/tangerineui.scss                  | **new**
tangerineui-purple: styles/tangerineui-purple.scss    | **new**
```

3. **Add a human-friendly name (optional).** You can edit each desired language's locale file in `config/locales/[lang].yml` to add a localized string name for Tangerine UI. You need to do this for every language you expect your users to use. Otherwise, in their themes list, they will see the unlocalized `themeName` ("tangerineui"), instead of a human-friendly theme name ("Tangerine UI").

```yml
themes:
  contrast: Mastodon (High contrast)
  default: Mastodon (Dark)
  mastodon-light: Mastodon (Light)
  tangerineui: Tangerine UI                           | **new**
  tangerineui-purple: Tangerine UI (Purple)           | **new**
```

4. **Compile theme assets and restart.** Run `RAILS_ENV=production bundle exec rails assets:precompile` and restart your Mastodon instance for the changes to take effect.

Your users should now be able to choose '*Tangerine UI*' and '*Tangerine UI (Purple)*' as their site theme:

![Screenshot : select Tangerine UI as a theme in appearance settings on Mastodon.](https://github.com/nileane/TangerineUI-for-Mastodon/assets/914451/8cce803c-099b-4f25-8e39-e1c0da3aa6dc)

As an admin, you should also now be able to set Tangerine UI as the default theme for your instance (navigate to https://*domain*/admin/settings/appearance):

![Screenshot : select Tangerine UI as the default theme for your Mastodon instance in the administration panel.](https://github.com/nileane/TangerineUI-for-Mastodon/assets/914451/05fcbb53-54de-40e4-89bd-199107116dfc)




## Installation for regular users:
Even if you are not the admin of your instance, you can still use Tangerine UI using a browser extension.

* Install any browser extension that allows you to inject CSS on a webpage, such as [Stylus](https://add0n.com/stylus.html), or [Live CSS Editor](https://github.com/webextensions/live-css-editor)
* Copy & paste the contents of [`TangerineUI.css`](https://github.com/nileane/TangerineUI-for-Mastodon/blob/main/TangerineUI.css) to the extension's editor
   * 🪻 For the purple variant, copy the contents of [`TangerineUI-purple.css`](https://github.com/nileane/TangerineUI-for-Mastodon/blob/main/TangerineUI-purple.css) instead.

## Things to know
* **Tangerine UI currently only supports Mastodon's single column layout**. The advanced view (multiple columns) will not be affected.
* **Tangerine UI auto-switches from light to dark mode based on your OS preference**, whether you set your Mastodon theme to *Mastodon (Dark)* or *Mastodon (Light*).
* Check your Mastodon instance version before using. The latest Mastodon release checked to be compatible is indicated in the CSS file header.
* **Glitch-soc** and **Hometown** instance admins beware: Tangerine UI is currently only meant to be applied to Mastodon's vanilla Dark and Light themes.
    * If you are a user on a Glitch-soc instance using a browser extension, first switch your instance to the vanilla flavour before applying Tangerine UI.

## Accessibility
* I have not yet adapted Tangerine to Mastodon's *High Contrast* theme setting. Please consider that some of your users may depend on it before setting Tangerine UI as the only theme on your instance.

## Credits
Huge thanks to [Roni Laukkarinen](https://mementomori.social/@rolle) whose work on [Mastodon Bird UI](https://github.com/ronilaukkarinen/mastodon-bird-ui) I adapted for multiple parts of the redesign. The icon replacement implementations I have also adapted from Bird UI.

## <3
If you enjoy Tangerine UI, jobless me would really appreciate a [tip 💛](https://ko-fi.com/nileane)!
