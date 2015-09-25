---
layout: page
title: Tags on Web
permalink: /tag-web-sdk/tags/
---

Display PowaTag tags for your products or merchandise. In order to display a tag you will need a PowaTag API key, read the [Getting Started](/tag-web-sdk/start/) guide for more information.

<br />

# Displaying a Tag

1. Add the PowaTag JavaScript and CSS to your page:

    <pre>&lt;link id="powatag-css" rel="stylesheet" href="//assets.powatag.com/qr/css/powatag.css"&gt;
   &lt;script type="text/javascript" src="//assets.powatag.com/qr/js/powatag.js"&gt;&lt;/script&gt;</pre>

2. Add the HTML snippet wherever you want the tag to be displayed .

    <pre>&lt;div class="powatag" data-key="your-api-key" data-sku="your-product-sku"&gt;&lt;/div&gt;</pre>

<br />
Parameters

**data-key**<br />
Your PowaTag API key.

**data-sku**<br />
The product variant SKU. You should be able to inject the product SKU from your templating system.

<br />

# Try it Out

<link id="powatag-css" rel="stylesheet" href="https://assets.powatag.com/qr/css/powatag.css">
<script src="https://assets.powatag.com/qr/js/powatag.js"></script>

<div>
  <div class="tagbox">
    <div id="tag"></div>
  </div>
</div>

<div class="tag-generator-control">
  <strong>Preview On</strong>
  <div class="btn-group" role="group" aria-label="...">
    <button id="desktop" type="button" class="switch btn btn-default active"><span class="fa fa-laptop" aria-hidden="true"></span> Desktop</button>
    <button id="tablet" type="button" class="switch btn btn-default"><span class="fa fa-tablet" aria-hidden="true"></span> Tablet</button>
    <button id="mobile" type="button" class="switch btn btn-default"><span class="fa fa-mobile" aria-hidden="true"></span> Mobile</button>
  </div>
</div>

<div class="tag-generator-control">
  <strong>Options</strong>
  <div class="options">
    <div class="sections">
      <form class="tag-generator-form">
        <div class="section">
          <div class="form-group">
            <label for="endpoint">Endpoint</label> <input type="url" class="form-control" id="endpoint" placeholder="Endpoint">
          </div>
          <div class="form-group">
            <label for="key">API Key</label> <input type="text" class="form-control" id="key" placeholder="API Key">
          </div>
          <div class="form-group">
            <label for="sku">SKU</label> <input type="text" class="form-control" id="sku" placeholder="Product SKU">
          </div>
          <div class="form-group">
            <label for="redirect">Redirect (optional)</label> <input type="url" class="form-control" id="redirect" placeholder="Redirect URL (optional)">
          </div>
          <div class="form-group">
            <label for="offer-title">Promotion Title (optional)</label> <input type="text" class="form-control" id="offer-title" placeholder="Title">
          </div>
          <div class="form-group">
            <label for="offer-content">Promotion Content (optional)</label> <input type="text" class="form-control" id="offer-content" placeholder="Content">
          </div>
        </div>
        <div class="section">
          <div class="form-group">
            <label for="lang">Language</label><select id="lang" class="form-control">
              <option value="en_GB">en_GB</option>
              <option value="es_ES">es_ES</option>
              <option value="it_IT">it_IT</option>
              <option value="fr_FR">fr_FR</option>
            </select>
          </div>
          <div class="form-group">
            <label for="type">Type</label><select id="type" class="form-control">
              <option value="bag">bag</option>
              <option value="mobile-button">mobile-button</option>
              <option value="tablet-bag">tablet-bag</option>
            </select>
          </div>
          <div class="form-group">
            <label for="style">Style</label><select id="style" class="form-control">
              <option value="bg-act-left">bg-act-left</option>
              <option value="act-left">act-left</option>
              <option value="bg-act-right">bg-act-right</option>
              <option value="act-right">act-right</option>
              <option value="bg-buy-left">bg-buy-left</option>
              <option value="buy-left">buy-left</option>
              <option value="bg-buy-right">bg-buy-right</option>
              <option value="buy-right">buy-right</option>
              <option value="bg-give-left">bg-give-left</option>
              <option value="give-left">give-left</option>
              <option value="bg-give-right">bg-give-right</option>
              <option value="give-right">give-right</option>
              <option value="OLD STYLE">OLD STYLE</option>
            </select>
          </div>
          <div class="form-group">
            <label for="colorscheme">Button color scheme</label><select id="colorscheme" class="form-control">
              <option value="light">light</option>
              <option value="dark">dark</option>
              </select>
            </div>
            <div class="form-group"><label for="display">Display</label><select id="display" class="form-control">
              <option value="both">both</option>
              <option value="desktop-only">desktop-only</option>
              <option value="mobile-only">mobile-only</option>
            </select>
          </div>
          <div class="form-group">
            <label for="video">Video</label><select id="video" class="form-control">
              <option value="true">true</option>
              <option value="false">false</option>
            </select>
          </div>
        </div>
        <div class="section">
          <button id="reload" type="submit" class="btn btn-default">Refresh</button>
        </div>
      </form>
    </div>
  </div>
</div>

<div class="container">
  <div class="row">
    <div class="col-xs-12">
      <strong>Code</strong>
      <div id="code" class="code"></div>
    </div>
  </div>
</div>

<script>
var btn = document.getElementsByClassName('switch');
var scr = document.getElementById('script');

for (var i=0; i < btn.length; i++) {
    btn[i].addEventListener('click', function(){
        for (var j=0; j < btn.length; j++) {
            btn[j].className = btn[j].className.replace(' active', '')
        }
        this.className += ' active';

        PowaTags.setDevice(this.id);
        StaticPowaTags.setDevice(this.id);
    });
}
</script>

<script>
    var tagC = document.getElementById('tag');
    var tag = document.createElement('div');
    var code = document.getElementById('code');

    tagC.appendChild(tag);

    var endpoint = document.getElementById('endpoint'),
        key = document.getElementById('key'),
        sku = document.getElementById('sku'),
        redirect = document.getElementById('redirect'),
        offerTitle = document.getElementById('offer-title'),
        offerContent = document.getElementById('offer-content');

    var lang = document.getElementById('lang'),
        type = document.getElementById('type'),
        style = document.getElementById('style'),
        button = document.getElementById('colorscheme'),
        display = document.getElementById('display'),
        video = document.getElementById('video');

    var watch = [lang, type, style, button, display, video];

    endpoint.value = 'https://api-sb2.powatag.com';
    key.value = 'b3JvYmlhbmNvdGVzdDErYXBpOjEyMzQ1Njc4';
    sku.value = '519';

    tag.className += 'powatag';
    tag.setAttribute('data-endpoint', endpoint.value);
    tag.setAttribute('data-key', key.value);
    tag.setAttribute('data-sku', sku.value);

    tag.setAttribute('data-lang', lang.value);
    tag.setAttribute('data-type', type.value);
    tag.setAttribute('data-style', style.value);
    tag.setAttribute('data-colorscheme', button.value);

    var printCode = function(){
        code.textContent = tagC.innerHTML.replace(tag.innerHTML, '').replace(/ powatag-([A-z|-])*/g, '');
    };

    for (var i = 0; i < watch.length; i++) {
        watch[i].addEventListener('change', function(){
            tag.setAttribute('data-' + this.id, document.getElementById(this.id).value);
            printCode();
            PowaTags.reload();
        });
    }

    document.getElementById('reload').addEventListener('click', function(e) {
        e.preventDefault();
        tag.setAttribute('data-endpoint', endpoint.value);
        tag.setAttribute('data-key', key.value);
        tag.setAttribute('data-sku', sku.value);

        tag.setAttribute('data-lang', lang.value);
        tag.setAttribute('data-type', type.value);
        tag.setAttribute('data-style', style.value);
        tag.setAttribute('data-colorscheme', button.value);
        if (redirect.value) tag.setAttribute('data-redirect', redirect.value);
        if (offerTitle.value || offerContent.value) tag.setAttribute('data-offer', offerTitle.value + '#' + offerContent.value);


        PowaTags.reload();

        printCode();

    });

    printCode();
</script>

<br />

# Customizing the Tag

Options

**data-endpoint**<br />
The PowaTag server URL. If not specified will default to Production.

| Endpoint                 | Environment     |
| `//api.powatag.com/`     | Production      |
| `//api-sb1.powatag.com/` | Sandbox 1       |
| `//api-sb2.powatag.com/` | Sandbox 2       |
| `//custom-endpoint.com/` | Custom Endpoint |

<br />**data-redirect**<br />
Overrides the URL the browser is redirected to after a successful transaction.
Defaults to the redirect URL specified when creating the workflow.

**data-lang**<br />
The language of the tag text. Defaults to `en_GB`.

| Lang  	| Language        |
| `en_GB`	| English (UK)    |
| `es_ES`	| Spanish (Spain) |
| `fr_FR`	| French (France) |
| `it_IT`	| Italian (Italy) |

<br />**data-type**<br />
The type of PowaTag is displayed on each device. Defaults to `bag`.

| Type            | Desktop     | Tablet            | Mobile            |
| `bag`	          | Bag with QR | Touch to X bag    | Touch to X button |
| `tablet-bag`	  | bag with QR	| Touch to X bag	  | Touch to X button |

<br />**data-style**<br />
The style of PowaTag displayed on each device. Defaults to `buy-left`.

| Style           | Desktop Bag | Button |
| `act-left`      | <img src="{{ '/images/powatag_web_sdk_act_left.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_act_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_act_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `act-right`     | <img src="{{ '/images/powatag_web_sdk_act_right.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_act_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_act_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `buy-left`      | <img src="{{ '/images/powatag_web_sdk_buy_left.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_buy_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_buy_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `buy-right`     | <img src="{{ '/images/powatag_web_sdk_buy_right.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_buy_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_buy_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `give-left`     | <img src="{{ '/images/powatag_web_sdk_give_left.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_give_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_give_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `give-right`    | <img src="{{ '/images/powatag_web_sdk_give_right.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_give_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_give_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-act-left`   | <img src="{{ '/images/powatag_web_sdk_act_left_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_act_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_act_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-act-right`  | <img src="{{ '/images/powatag_web_sdk_act_right_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_act_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_act_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-buy-left`   | <img src="{{ '/images/powatag_web_sdk_buy_left_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_buy_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_buy_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-buy-right`  | <img src="{{ '/images/powatag_web_sdk_buy_right_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_buy_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_buy_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-give-left`  | <img src="{{ '/images/powatag_web_sdk_give_left_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_give_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_give_dark.png' | prepend: site.baseurl }}" width="200" /> |
| `bg-give-right` | <img src="{{ '/images/powatag_web_sdk_give_right_bg.png' | prepend: site.baseurl }}" /> | <img src="{{ '/images/powatag_web_sdk_button_give_light.png' | prepend: site.baseurl }}" width="200" /> <img src="{{ '/images/powatag_web_sdk_button_give_dark.png' | prepend: site.baseurl }}" width="200" /> |

<br />**data-offer**<br />
The offer text to be displayed alongside the tag.

The offer text only shows on the desktop PowaTag view and the PowaTag QR must have a branded background.

The promotion title must be specified first within the data-offer attribute. It should then be followed by a # (hash symbol) which separates the title from the Promotion Content, for example `data-offer="ENTER NOW!#For your chance to win!"`.

The placing of the area is dependent on which tag style variant has been chosen.
Currently there are 6 supported style variants for the promotional area: `bg-act-left`, `bg-act-right`, `bg-buy-left`, `bg-buy-right`, `bg-give-left`, `bg-give-right`.

|  Offer                                                 | Style          | Example |
| `SPECIAL OFFER!#Only £20.99 when you buy with PowaTag` | `bg-buy-left`  | <img src="{{ '/images/powatag_web_sdk_buy_promo.png' | prepend: site.baseurl }}"/> |
| `ENTER NOW!#For your chance to win!`                   | `bg-act-right` | <img src="{{ '/images/powatag_web_sdk_act_promo.png' | prepend: site.baseurl }}"/> |

<br />**data-colorscheme**<br />
Whether the light or dark version of the button is displayed. Defaults to `light`.

| Color Scheme  | Example |
| `light`       | <img src="{{ '/images/powatag_web_sdk_button_light.png' | prepend: site.baseurl }}" width="200" /> |
| `dark`        | <img src="{{ '/images/powatag_web_sdk_button_dark.png' | prepend: site.baseurl }}" width="200" /> |

<br />**data-display**<br />
Choose whether to show or hide the PowaTag on a particular form-factor. Defaults to `both`.

| Display        | Shown on Desktop? | Shown on Mobile? |
| `both`         | YES               | YES              |
| `desktop-only` | YES               | NO               |
| `mobile-only`	 | NO                | YES              |

<br />**data-video**<br />
Show or hide the video within the "What's This?" pop-out modal. Defaults to `true`.

| Video   |	Video Displayed?  |
| `true`  |	YES               |
| `false` |	NO                |

<br />**data-debug**<br />
Output to the browser's console detailed information about the PowaTag. Defaults to `false`.

FOR DEVELOPMENT USE ONLY. DO NOT USE IN PRODUCTION.

| Debug  	| Console messages printed? |
| `false`	| NO                        |
| `true`	| YES                       |
