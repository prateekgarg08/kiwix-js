# Kiwix JS

Kiwix is an offline browser for Wikipedia, Stackexchange, Project Gutenberg, and other Web resources packaged as highly compressed ZIM
archives. For full information about the open-source Kiwix project, see our main Web site: https://www.kiwix.org/.

Kiwix JS is an official HTML5/Javascript implementation of the Kiwix software, principally targeting browser extensions or add-ons. You
can get the extension, completely free, from the Mozilla, Chrome and Edge extension stores (see [Store links](#officially-supported-platforms) below).
There is also a version, primarily intended for use within extensions, implemented as an offline-first Progressive Web App (PWA)
at https://browser-extension.kiwix.org/current/. For the dedicated, fully featured PWA based on Kiwix JS, please see https://pwa.kiwix.org. 

To use Kiwix JS, you will need to obtain, completely free, a content archive (see [Usage](#usage)). Once you have this on your device, select it with the
file selector (Configuration page), or drag-and-drop it into the app, and start searching for article titles. No further Internet access is required to
read the archive's content. You can have the entire content of Wikipedia in your own language inside your device (including images and audiovisual content)
entirely offline. If your Internet access is expensive, intermittent, slow, unreliable, controlled or censored, you can still have offline access to this
amazing repository of knowledge, information and culture.

The Kiwix browser also works with other content in the [OpenZIM format](https://wiki.openzim.org/wiki/OpenZIM), but our main targets are Mediawiki-based
content (Wikipedia, Wikivoyage, Wikitionary, etc.), StackExchange, Project Gutenberg and TED Talks.

[![Build Status: Continuous Integration](https://github.com/kiwix/kiwix-js/workflows/CI/badge.svg?query=branch%3Amain)](https://github.com/kiwix/kiwix-js/actions?query=branch%3Amain)
[![Build Status: Release](https://github.com/kiwix/kiwix-js/workflows/Release/badge.svg?query=branch%3Amain)](https://github.com/kiwix/kiwix-js/actions?query=branch%3Amain)
[![CodeFactor](https://www.codefactor.io/repository/github/kiwix/kiwix-js/badge)](https://www.codefactor.io/repository/github/kiwix/kiwix-js)
[![Licence: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

[![Kiwix for Firefox](https://img.shields.io/amo/v/kiwix-offline?label=Kiwix%20for%20Firefox&logo=firefoxbrowser&logoColor=whitesmoke)](https://addons.mozilla.org/fr/firefox/addon/kiwix-offline/)
[![Kiwix for Chrome](https://img.shields.io/chrome-web-store/v/donaljnlmapmngakoipdmehbfcioahhk?label=Kiwix%20for%20Chrome&logo=googlechrome&logoColor=whitesmoke)](https://chrome.google.com/webstore/detail/kiwix/donaljnlmapmngakoipdmehbfcioahhk)
[![Kiwix for Edge](https://img.shields.io/badge/dynamic/json?label=Kiwix%20for%20Edge&logo=microsoftedge&logoColor=whitesmoke&prefix=v&query=%24.version&url=https%3A%2F%2Fmicrosoftedge.microsoft.com%2Faddons%2Fgetproductdetailsbycrxid%2Fjlepddlenlljlnnhjinfaciabanbnjbp)](https://microsoftedge.microsoft.com/addons/detail/kiwix/jlepddlenlljlnnhjinfaciabanbnjbp)

## Usage

Install "Kiwix JS" from your browser's add-on store. This is the best way to get the extension, because it will be kept up to date automatically. If
you would rather not use a store, you can get a file-based version of the extension from http://download.kiwix.org/release/browsers/ (and follow
[instructions below](#installing-signed-or-unsigned-extension-files-in-chromium)), but you will have to update this manually.

Alternatively, you can bookmark or install the PWA version from https://browser-extension.kiwix.org/current/ (it will auto-update), or try our dedicated
PWA version at https://pwa.kiwix.org. To install the PWA (in Chromium browsers), go to Settings -> Apps -> Install this site as an app.

As mentioned above, the app requires at least one ZIM archive of offline content. You can download one from https://library.kiwix.org (this has a nice,
graphical interface and a preview of each ZIM archive) or from https://download.kiwix.org/zim/ (a more basic list of archives). You have to download
these separately, store them in your filesystem, and manually select them after starting the application (or you can drag-and-drop one into the app).

Please note that certain "Zimit"-based archives (available from the "zimit" directory on https://download.kiwix.org/zim/) are not (yet) compatible
with this reader. There is experimental support for these in our sister app https://pwa.kiwix.org.

## Compatibility

Since the app is written in HTML/JavaScript, it should work in most recent browser engines and many older ones too, depending on the Content
Injection mode supported by the specific browser engine. Archives containing dynamic content (most non-Wikimedia archives) work much better
in ServiceWorker mode ([see below](#some-technical-details)), but unfortunately this is not available in many older browsers. If you wish to read such archives, we
would suggest that you upgrade to a browser that supports Service Workers (Chrome 58+, Firefox 61+ [not ESR versions], Edge 17+, Safari 11.3+).

### Officially supported platforms

- <img src="images/firefoxbrowser-color.svg" width="20" /> Mozilla Firefox >=56 (as an extension): [Mozilla Add-ons Store](https://addons.mozilla.org/fr/firefox/addon/kiwix-offline/)
    + Firefox 52-56 and ESR version 58: Limited support (jQuery mode only)
- Chromium / Chrome / Edge >= 88 (as a Manifest V3 extension):
    + <img src="images/googlechrome-color.svg" width="20" /> Google Chrome >=88: [Chrome Web Store](https://chrome.google.com/webstore/detail/kiwix/donaljnlmapmngakoipdmehbfcioahhk)
    + <img src="images/microsoftedge-color.svg" width="20" /> Microsoft Edge >=88: [Edge Add-ons Store](https://microsoftedge.microsoft.com/addons/detail/kiwix/jlepddlenlljlnnhjinfaciabanbnjbp)
- Chromium / Chrome / Edge 58-87 (as a Manifest V2 extension): use the MV2 zip from the `chrome` or `edge` directory in https://download.kiwix.org/release/browsers/, and follow [instructions below](#installing-signed-or-unsigned-extension-files-in-chromium)
- <img src="images/safari-color.svg" width="20" /> Safari >=11.3 on macOS or iOS: no extension available, but use https://browser-extension.kiwix.org and install to Home screen; for a more fully featured PWA, use https://pwa.kiwix.org
- <img src="images/electron-color.svg" width="27" /> Electron >=1.8.0 and NWJS >=0.14.7 (as an application for Linux and Windows): https://kiwix.github.io/kiwix-js-pwa/app
- <img src="images/microsoftwindows-color.svg" width="20" /> Universal Windows Platform (UWP) >=10.0.10240 (as an HTML/JS application): [Microsoft Store](https://www.microsoft.com/store/apps/9P8SLZ4J979J)
- <img src="images/ubuntu-color.png" width="20" /> Ubuntu Touch (as an application): [Ubuntu OpenStore](https://open-store.io/app/kiwix)

### Deprecated platforms

These platforms/browsers are deprecated. We still partially test against them, and we'll try to keep compatibility as long as it's not too complicated:

- Firefox OS >=1.2: needs to be installed manually on the device with WebIDE
- Microsoft Edge Legacy >=17: no extension available, but bookmark https://browser-extension.kiwix.org or https://pwa.kiwix.org
- Microsoft Edge Legacy 15-16: needs to run a bundled version of the source code in jQuery mode only
- Microsoft Internet Explorer 11: needs to run a bundled version of the source code in jQuery mode only

**_You can build a bundled version by running `npm install` and `npm run build` in the root directory of this repo._** Alternatively, a bundled version is served
as a web app for testing from https://kiwix.github.io/kiwix-js/dist/ (also available on the `gh-pages` branch of this repo, under `/dist`). 

### Installing signed or unsigned extension files in Chromium

If you need to install Chromium (Chrome or Edge) extension from a file instead of from a Store, e.g. if your browser doesn't support Manifest V3, then you will need to download a
signed or unsigned CRX or ZIP file from a relevant directory in https://download.kiwix.org/release/browsers/, or else a nightly version from https://download.kiwix.org/nightly/.
Files with `mv2` in their filename are in the legacy Manifest V2 format.

To install your CRX or ZIP, open the extension management page in your browser, e.g. chrome://extensions/ or edge://extensions/, and turn on Developer mode. Now, you should be
able to drag and drop the ZIP file into this page. Verify the extension is showing in the management page.

Files that we deliver with a `.crx` file extension are files that have been validated by the Edge or Chrome Stores, and you should be able to install these as "first-class" apps.
ZIP files provided in https://download.kiwix.org/release/browsers/, or the ones labelled `signed` in nightly, are actually signed CRX files that have been renamed with a `.zip`
extension to facilitate downloading and installing them in Chromium browsers. Although signed, you cannot install them as CRX files, because they have not been validated by the
Chrome or Edge Stores. **_For this reason, the browser will periodically ask you if you want to turn off developer-mode extensions. Just choose "ask again in two weeks"._**

If drag-and-drop is difficult, you can instead unzip the extension ZIP into a folder, and note the location. Then select "Load unpacked" and choose  the folder that contains the
unzipped extension. To unzip the MV2 files with a utility like 7Zip, you will need to change the extension name to `.crx`. On Linux, `unzip` can read them without changing the filename.

## Some technical details

Technically, after reading an article from a ZIM file, it is necessary to "inject" the dependencies (images, css, etc). For compatibility reasons,
there are two main ways of doing this:

- "ServiceWorker" mode (the default) uses a Service Worker to catch any HTTP request the page may send and reply with content read from
the ZIM file. It is a generic and clean way of serving content to the browser. It works in any recent browser, but not in older ones.
Service Workers are currently disabled by Mozilla in Firefox extensions, but we use a workaround (an offline-first PWA version) as a
substitute within the extension;
- "JQuery" mode (deprecated) parses the DOM to find the HTML tags of the dependencies and modifies them to point to content we extract
from the ZIM. This mode is compatible with any browser, but it cannot run JavaScript inside the ZIM file, so some ZIMs with dynamic
content do not work well (if at all). However, Mediawiki-based content (e.g. Wikipedia) works fine in this mode.

You can switch between these content injection modes in Configuration, but if your browser supports ServiceWorker mode, you are strongly
advised to remain in this mode.

### Limitations

It is unfortunately not yet technically possible to "remember" the selected ZIM file and open it automatically (browsers do not allow that for
security reasons). A handy alternative is to drag-and-drop a ZIM file into the app, which is a quick way to open an archive
and switch between several archives in a folder. There are
[versions of this app](https://kiwix.github.io/kiwix-js-pwa/app) that use frameworks like Electron, UWP or NWJS
which do have the capability of remembering the chosen archive between app launches. For desktop Chromium browsers, the
[File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) (see
[#656](https://github.com/kiwix/kiwix-js/issues/656)) is implemented in a PWA version at https://pwa.kiwix.org.

The app has fast title search, and slower full-text search for ZIM archives that have a full-text index, thanks to the
[openzim/javascript-libzim](https://github.com/openzim/javascript-libzim) project. Currently, full-text searching only works in browsers
that support [Atomic Operations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics), which means
recent desktop versions of Chromium and Firefox. There is also support in Safari on iOS 15+.

## Licence

This application is released under the GPL v3 licence. See http://www.gnu.org/licenses/ or the included LICENSE-GPLv3.txt file
The source code can be found at https://github.com/kiwix/kiwix-js.

## Contributing

Kiwix JS is an open-source project. We encourage individuals with experience of HTML and JavaScript development to contribute to the documentation and code in this repository.

To report a bug, read our [REPORT_BUG](REPORT_BUG.md) guide.

For code contributions, read our [CONTRIBUTING](CONTRIBUTING.md) guide.

To get to know the Kiwix project better, please familiarize yourself with the content on https://www.kiwix.org. There is also a Kiwix [Slack](https://join.slack.com/t/kiwixoffline/shared_invite/zt-19s7tsi68-xlgHdmDr5c6MJ7uFmJuBkg) group which you can join.

We also have a [CODE_OF_CONDUCT](CODE_OF_CONDUCT.md): everybody is expected to follow it.

## Public releases and nightly builds

The browser extensions are distributed through the stores of each vendor (see links above). But the packages are also saved in https://download.kiwix.org/release/browsers/ if necessary.

Some nightly builds are generated, and should only be used for testing purpose: https://download.kiwix.org/nightly/.

There is a test implementation of the latest code at https://kiwix.github.io/kiwix-js/ (unbundled: needs a modern browser that suppors native ES6 modules), and a bundled version for any
HTML5 browser (>=IE11) at https://kiwix.github.io/kiwix-js/dist/, but these implementations are used for development, and may be buggy, experimental or unstable. A stable PWA version for
use in the browser extensions is available from https://browser-extension.kiwix.org/current/.

## Previous versions

The first versions of this application were originally part of the Evopedia project: http://www.evopedia.info (discontinued). There was an "articles nearby" feature, that was able to find articles around your location. It has been deleted from the source code with everything related to Evopedia (but still in git history in versions<=2.0.0).

These first versions were targeting Firefox OS (discontinued too: we're not lucky ;-) ).

See [CHANGELOG.md](CHANGELOG.md) for details of previous versions.
