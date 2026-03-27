Owly plugin for `Tutor <https://docs.tutor.edly.io>`__
######################################################

Bring the power of AI to Open edX with Owly!

To know more about Owly and book a demo, visit `GetOwly.ai <https://getowly.ai>`__.

Note
****

You do not need this plugin to run Owly.
This Tutor plugin enhances Owly when used with Open edX by:

- Adding extra API endpoints in Open edX to enable advanced features (analytics, course management, content creation, staff management, roles, etc.).
- Injecting the Owly chat widget into LMS and MFE pages when the plugin is enabled.

Installation
************

This plugin supports Tutor 20.x.

.. code-block:: bash

    pip install git+https://github.com/aulasneo/tutor-contrib-owly

Usage
*****

.. code-block:: bash

    tutor plugins enable owly
    tutor images build openedx
    tutor images build mfe
    tutor local start

If you are enabling chat support, make sure the ``mfe`` plugin is enabled in Tutor as well.

Configuration
*************

When the plugin is enabled, it injects Owly into LMS and MFE pages.
You will need to build the MFE image and restart the environment.

Chat visibility is controlled in the LMS by the Django waffle flag ``owly_chat.enable``.
Like any regular waffle flag, it can be targeted by user, user group, user role, and other standard waffle criteria.

This plugin embeds Owly in all Open edX MFEs. Some Open edX pages are still rendered as HTML instead of MFEs.
If you want Owly to appear on those HTML pages as well, you need to edit your theme and add the script loader manually, usually in ``head-extra.html``:

.. code-block:: html

    <script type="text/javascript" async="" src="https://chat.owly.aulasneo.com/owly-chatbot-embed.js" data-owly-platform-type="openedx" data-owly-base-url="https://<your campus url>"></script>

Due to OAuth2 restrictions, Owly requires the LMS to be exposed to the public internet.
It will not work from local-only hosts such as ``localhost``, ``127.0.0.1``, ``local.edly.io``, or similar development domains.

How it works
************

This plugin integrates Owly with Open edX by:

- Exposing additional backend endpoints used by Owly for advanced capabilities.
- Embedding the Owly chat widget across the LMS/MFE whenever the plugin is enabled.

For a complete list of API endpoints, visit `Owly API Reference <https://github.com/aulasneo/openedx-owly-apis>`__.
