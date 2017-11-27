<div class="range range-xs-left">
<div class="cell-xs-10 cell-lg-6 text-md-left inset-md-right-80 cell-lg-push-1 offset-top-50 offset-lg-top-0">
<h2 id="content" class="h1">Testing with Web Browsers from outside ElasTest</h2>
<div class="offset-top-30 offset-md-top-50">
</div>
</div>
</div>

You can make use of ElastTest Web Browser services to run your local or CI end-to-end tests on any browser and version you want.

This is a deal breaker for developers: whatever platform you are coding in and whatever framework you are using, you can easily launch any browser in ElasTest dashboard and use it remotely to run your tests straight from your machine, as you would do in your favourite IDE. Do you want to test your web on Microsoft's Edge but you don't even have a Windows machine? No problem, just launch an Edge instance on ElasTest and run your test against it. Any other browser provided in ElasTest Web Browser services could serve as an example of this use case.

In order to run your test on ElasTest browsers, you just need to use the **URL shown on "Web Browsers" page**. There is no restriction on the environment your test is being executed: you can run it on your development machine from the command line or even directly from your favourite editor. Or you can run your test on ElasTest browsers as part of your CI platform, so that in the event of any failure you can check the window recording and browser's console. The advantages are considerable compared to other alternatives.

<div class="docs-gallery inline-block">
    <a data-fancybox="gallery-2" href="/docs/how-to/images/test.png"><img class="img-responsive img-wellcome" src="/docs/how-to/images/test.png"/></a>
</div>

To illustrate this scenarios, let's see how to start a Selenium Web Driver using different languages to remotely use ElasTest browsers. If the URL provided in "Web Browsers" page is `https://MY_REMOTE_WEB_BROWSER_URL.com`:

<div class="badges-menu">
    <span id="java-test-btn" class="badge badge-default my-badge">Java</span>
    <span id="js-test-btn" class="badge badge-default my-badge">JS</span>
    <span class="badge badge-default my-badge my-badge-disabled">. . .</span>
</div>

<div id="java-test">
<pre><code class="java">// Chrome

DesiredCapabilities caps = new DesiredCapabilities().chrome();
WebDriver driver = new RemoteWebDriver(new URL("https://MY_REMOTE_WEB_BROWSER_URL.com"), caps);

// Firefox

DesiredCapabilities caps = new DesiredCapabilities().firefox();
WebDriver driver = new RemoteWebDriver(new URL("https://MY_REMOTE_WEB_BROWSER_URL.com"), caps);</code></pre>
</div>

<div id="js-test">
<pre><code class="javascript">// Chrome

var browserBuilder = new webdriver.Builder().forBrowser("chrome");
browserBuilder.usingServer("https://MY_REMOTE_WEB_BROWSER_URL.com");
driver = browserBuilder.build();

// Firefox

var browserBuilder = new webdriver.Builder().forBrowser("firefox");
browserBuilder.usingServer("https://MY_REMOTE_WEB_BROWSER_URL.com");
driver = browserBuilder.build();</code></pre>
</div>

<p>
That's all the extra configuration needed. The rest of the code is exactly the same as in a regular Selenium test.
Whenever you run it, ElasTest will launch the requested browser on-demand and the test will be remotely executed against it.
</p>

<p>
You will have available the browser's window in real time to see your test in action. When it finishes, a <i>.mp4</i> file will be available for download.
</p>

<div class="docs-gallery inline-block">
    <a data-fancybox="gallery-2" href="/docs/how-to/images/test.png"><img class="img-responsive img-wellcome" src="/docs/how-to/images/test.png"/></a>
</div>

<script>
function navigateTo(subpage) {
    switch(subpage) {
        case 'java':
            $('#js-test').hide();
            $('#java-test').show();
            break;
        case 'js':
            $('#java-test').hide();
            $('#js-test').show();
            break;
        default:
            navigateTo('java');
            break;
    }
}

$('#java-test-btn').click(function() {
  navigateTo('java');
});
$('#js-test-btn').click(function() {
  navigateTo('js');
});

window.onload = function() {
  navigateTo(('java'));
};
</script>

<script src="//code.jquery.com/jquery-3.2.1.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.2.5/jquery.fancybox.min.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.2.5/jquery.fancybox.min.js"></script>

<script>
var galleries = $('div.docs-gallery');
for (var i = 1; i <= galleries.length; i++) {
    $().fancybox({
    selector : '[data-fancybox="gallery-' + i + '"]',
    infobar : true,
    arrows : false,
    loop: false,
    protect: true,
    transitionEffect: 'slide',
    buttons : [
        'close'
    ],
    clickOutside : 'close',
    clickSlide   : 'close',
  });
}
</script>