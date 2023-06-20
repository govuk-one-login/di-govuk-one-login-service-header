# A header for services using GOV.UK One Login

The GOV.UK One Login service header is a new navigation component for government services connected to GOV.UK One Login.

It provides a way for users to:

+ know they’re signed in
+ sign out
+ change their sign in credentials

The One Login header has been adapted from the [standard service header in the GOV.UK Design System](https://design-system.service.gov.uk/components/header/).

It's a 'beta' component and we're interested to hear from service teams about how it performs with your users.

The header works best if your service uses [GOV.UK Frontend](https://frontend.design-system.service.gov.uk/).

You can [preview the header in your browser](https://alphagov.github.io/di-govuk-one-login-service-header/dist/preview.html).

![A screenshot of the GOV.UK One Login header. It has 2 sections: a black section at the top showing the GOV.UK crown logo, a link saying "GOV.UK One Login", which takes you into your account, and a "Sign out" button. Below this section is a grey section, diplaying the name of a government service and internal links within that service. Those just have placeholder text, so read "Service name" and "Service link 1" and so on. The black and grey sections are divided by a blue bar, like on the GOV.UK homepage.](header_screenshot_larger_screen.png)

## What different parts of the header do

The header contains two distinct navigation menus - one for GOV.UK One Login links and another for internal service navigation.

On smaller screens, both menus collapse and can be shown and hidden using Javascript.

You’ll need to adapt the internal service navigation so that it includes content specific to your service. This includes adapting the accessibility markup in the internal service navigation.

### GOV.UK One Login links in the header

The header contains two links.

| Link text | Link destination | Function |
| - | - | - |
| GOV.UK One Login | `https://home.account.gov.uk/` | Takes the user to their One Login ‘home’ area, where they can manage their credentials and see and access the services they've used |
| Sign out | `https://home.account.gov.uk/sign-out` | Signs the user out of One Login, and ends their signed in session with your services

### Internal service navigation links in the header

The header has space to optionally add links to different parts of your service, just as the current ‘service header’ component from the Design System does. Follow the same patterns for internal service navigation links as you do with the Design System service header.

## How to start using the header in your service

This repository contains:

+ Nunjucks for the GOV.UK One Login service header component
+ plain HTML for the header - this is compiled from the Nunjucks into the `/dist` directory
+ Sass files for compiling CSS files to style the header
+ plain CSS, for services who are not using Sass
+ a Javascript file which enables 'drop down' behaviour for the header menu on small screens

This is all the code necessary to render the header, but you will need to make additional changes to your service and to the header code for it to function correctly.

You will need to:

+ write logic within your service so that the header is only shown to users who are signed in
+ adapt the header's HTML so that it works in the templating language your service uses
+ adapt the internal service navigation HTML so that it includes content specific to your service
+ include the styling and Javascript files in your service

### Write logic within your service so that the header is only shown to users who are signed in

The header should only be displayed when your users are signed in. There’s no ‘signed out state’ version of the header for the time being.

You’ll need to build the logic for only showing the header to signed in users within your service.

### Adapt the header's HTML so that it works in the templating language your service uses

The code for the header is currently available in HTML and the Nunjucks templating language. You will need to adapt the HTML or Nunjucks for the templating language your service uses.

The Nunjucks code will work with the [GOV.UK Prototype Kit](https://prototype-kit.service.gov.uk/docs/), which uses Nunjucks as its templating language.

[Contact the GOV.UK One Login team](#contact) if you would like to share your templating implementation in this repository for other teams to use.

### Adapt the internal service navigation HTML so that it includes content specific to your service

You'll need to modify the internal service navigation part of the header in order to:

+ visually highlight which page in the menu the user is currently on
+ ensure screen reader text and ARIA attributes are specific to your service

#### Visually highlight which page in the menu the user is currently on

You can visually highlight the page the user is currently on in the navigation menu by adding the `service-header__nav-list-item--active` modifier class to the relevant `li` element in the internal service navigation menu. You’ll need to implement this in the code you’re using to render your pages.

#### Edit screen reader text and ARIA attributes to be specific to your service

The header is designed to work for users of screen readers and contains some visually hidden text and [ARIA attributes](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) which you will need to edit to make it specific to your service.

You’ll need to edit the markup for the:

+ ‘menu’ button
+ service navigation
+ page the user is currently on in the service navigation

#### Edit accessibility markup for the ‘menu’ button

The menu button is used to show or hide the internal service navigation menu of the header on small devices.

You’ll need to adapt the screen reader text for the following attributes of the menu button element:

+ `aria-label`
+ `data-label-for-show`
+ `data-label-for-hide`

In this repository, the values for these attributes refer to the “service navigation menu”. You should adapt this text to describe your service’s navigation menu. For example, you could update `data-label-for-show` to have the value “Show Juggling Licence service navigation menu”.

This is to help users understand which navigation menu they are opening and closing.

#### Edit accessibility markup for the internal service navigation menu

The service navigation menu contains links to help users navigate your service. It’s distinct from the One Login navigation menu which lets users access One Login and sign out.

You’ll need to adapt the screen reader text for the `aria-label` attribute of the service navigation menu element.

In this repository, the value for this attribute refers to the “Service menu”. You should adapt this text to be specific to your service. For example, you could set the text to “Juggling Licence service navigation menu”.

This is to help users understand which navigation menu they are using. It also helps meet the WCAG requirement that navigation landmarks must be labelled when there is more than one `nav` element on the page, to describe the navigation to users who may be navigating the site using landmarks.

#### Edit accessibility markup for the navigation menu page the user is currently on

You can [visually highlight the page the user is currently on in the navigation menu](#visually-highlight-which-page-in-the-menu-the-user-is-currently-on).

In addition to this, set the `aria-current="page"` attribute on the relevant `<a>` element.

This is to indicate the user’s position in the navigation if they can’t perceive the visual highlight styling.

## Using the styles for the header in your service

How you use the styles for the header will be different depending on whether you:

+ use the GOV.UK Frontend npm package on your service
+ use the GOV.UK Frontend precompiled CSS files on your service
+ do not use GOV.UK Frontend

### If you use the GOV.UK Frontend npm package

Copy the Sass files from this repository into your service's Sass implementation.

Make sure you have added `node_modules/govuk-frontend` to your Sass loadpath. The header code uses this to [simplify its Sass import paths](https://frontend.design-system.service.gov.uk/importing-css-assets-and-javascript/#simplify-sass-import-paths).

Alternatively, you can edit the header’s Sass import paths to specify `node_modules/govuk-frontend` for each import.

### If you use the GOV.UK Frontend pre-compiled CSS files

Copy the pre-compiled CSS files from this repository into your service's pre-compiled CSS.

The pre-compiled CSS files in this repository duplicate some code from the GOV.UK Frontend CSS files. The header will still be styled correctly but your CSS files will be slightly larger than they need to be.

### If you do not use GOV.UK Frontend

Copy the pre-compiled CSS files from this repository into your service's CSS.

The pre-compiled CSS files contain all the CSS you need to style the header.

## Using the GDS Transport font

You must use the GDS Transport font with the header if your service is on the service.gov.uk subdomain.

However, this repository does not include the GDS Transport font. You’ll need to install it separately using GOV.UK Frontend.

There’s [more information about using GDS Transport](https://design-system.service.gov.uk/styles/typography/) in the GOV.UK Design System.

## Using the header's Javascript file

The GOV.UK One Login service header uses Javascript to enable 'drop down' behaviour for the header on small screen sizes. The header doesn't rely on Javascript to do anything else.

Copy the code in this repository's Javascript file into your service's Javascript implementation.

### Initialising the header

Copying the header’s Javascript file into your project does not initialise the drop down behaviour. This is so you can run other Javascript functions before initialisation of the header dropdown functionality if you need to.

You’ll need to initialise the Javascript in your code to make it work. To do this, you need to:

+ include [service-header.js](https://github.com/alphagov/di-govuk-one-login-service-header/blob/main/src/service-header.js) in your application Javascript - this attaches the function to the window object by default but you can namespace it if you need to
+ initialise the header by running `new window.CrossServiceHeader(document.querySelector("[data-module='one-login-header']")).init()`

### If you don’t use the header’s Javascript

The header degrades gracefully in the absence of Javascript (for example, if a user has turned Javascript off or the code does not load). Without Javascript:

+ both navigation menus will be in their ‘dropped down’ states
+ the menu toggle buttons will not display (they wouldn't be functional without Javascript)

## Translating the header content into other languages

The content for the header is currently only provided in English. A Welsh translation will be available soon.

If you need to translate the header into other languages, please consider sharing your translation with [the GOV.UK One Login team](#contact) so it can be used by other services.

## Contact

The best way to contact the maintainers of this repository is to use the [#govuk-one-login](https://ukgovernmentdigital.slack.com/archives/C02AQUJ6WTC) on Cross-Government Slack.
