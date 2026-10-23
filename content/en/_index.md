---
title: NOMM
description: A simple & easy way to mod on linux!
params:
  body_class: td-navbar-links-all-active
---

{{% blocks/cover
  title="NOMM: Native Open Mod Manager"
  height="med td-below-navbar"
  image_anchor="top"
%}}

<!-- prettier-ignore -->
{{% _param description %}}
{.display-6}

<!-- prettier-ignore -->
<div class="td-cta-buttons my-5">
  <a {{% _param btn-lg secondary %}} href="docs/">
    Read the docs
    <i class="fa fa-book-open"></i>
  </a>
  <a {{% _param btn-lg secondary %}}
    href="{{% param github_project_repo %}}"
    target="_blank" rel="noopener noreferrer">
    See the code
    {{% _param FA brands github "" %}}
  </a>
  <a {{% _param btn-lg primary button-green %}}
    href="https://flathub.org/en/apps/moe.nomm.Nomm"
    target="_blank" rel="noopener noreferrer">
    Get the app
    <i class="fa fa-download"></i>
  </a>
</div>

{{% blocks/link-down color="info" %}}

{{% /blocks/cover %}}

{{% blocks/lead color="white" %}}

NOMM provides a simple and modern solution for modding your games on Linux. It has support for over a dozen games, and adding support yourself is super easy (barely an inconvenience)!

No more faffing about trying to make vortex work on your distro, simply install the flatpak, follow the in-app setup and you're good to go!


{{% /blocks/lead %}}

{{% blocks/section color="primary" type="row" %}}

{{% blocks/feature
  title="Easy Game Support" icon="fa-gamepad"
  url="/docs/adding-your-game/"
  color="#56cc6d"
%}}

Support for a game is done via a simple yaml file.<br>Anyone can do it! No dev experience required.

{{% /blocks/feature %}}

{{% blocks/feature
  title="Multi-platform support" icon="fab fa-steam"
  url="/docs/about/game-platforms/"
  color="#c98848"
%}}

We have support for Steam,<br>but also GOG and Epic via Heroic!

{{% /blocks/feature %}}

{{% blocks/feature
  title="Full Nexus integration" icon="fa-cloud-arrow-down"
  url="/docs/about/mod-platforms/"
  color="#ea5792"
%}}

NOMM handles download links, update checking,<br>and even metadata updating!

{{% /blocks/feature %}}


{{% blocks/feature
  title="Super Secure" icon="fa-lock"
  url="/docs/about/flatpak-security/"
  color="#ead86e"
%}}

NOMM is distributed as a flatpak and is designed to only request the<br>minimal amount of access it needs to help you mod your games.

{{% /blocks/feature %}}

{{% blocks/feature
  title="Intuitive UI" icon="fa-window-maximize"
  url="/docs/nomm-guides"
  color="#ea5792"
%}}

We don't overwhelm our users with dozens of buttons.<br>
We prioritise a clean UI/UX so that you don't need a wiki to use the tool.

{{% /blocks/feature %}}

{{% blocks/feature
  title="Strong values" icon="fa-trophy"
  url="/docs/about/values"
  color="#56cc6d"
%}}

NOMM will always be open and free<br>
We also value transparency when it comes to AI use

{{% /blocks/feature %}}

{{% /blocks/section %}}
