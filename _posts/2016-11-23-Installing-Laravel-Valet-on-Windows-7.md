---
layout: post
title: Installing Laravel Valet on Windows 7
date: 2016-11-23
---
Laravel Valet is officially a Mac developer tool,  but it also works well on Windows.

<ol>
    <li>In the Terminal or <strong>Command Prompt</strong> run <code>git clone https://github.com/MehediDracula/valet</code>. You will of course already have <a href="https://git-for-windows.github.io/" target="_blank">Git</a> installed locally.</li>
    <li><code>cd</code> into the new <em>valet</em> directory.</li>
    <li>Run <code>git checkout windows</code></li>
    <li>Run <code>composer install</code>. You will of course already have <a href="https://getcomposer.org/doc/00-intro.md#installation-windows" target="_blank">Composer</a> installed locally, and you will also, of course, already have <a href="http://windows.php.net/" target="_blank">PHP</a> installed locally.</li>
    <li>If you are using <strong>GitBash</strong>, change to the <strong>Command Prompt</strong>, as an Administrator. (<strong>Start menu</strong> -> <strong>All Programs</strong> -> <strong>Accessories</strong> -> Right Click on <strong>Command Prompt</strong> -> Select <strong>Run as Administrator</strong>), then <code>cd</code> into the <code>valet</code> directory.</li>
    <li>Run <code>valet install</code></li>
</ol>

<img class="alignnone size-full wp-image-81" src="https://nisbeti.files.wordpress.com/2016/11/valet-install.png" alt="valet-install" width="673" height="339" />

<ol>
    <li>Ignore Acrylic error</li>
</ol>

<img class="alignnone size-full wp-image-85" src="https://nisbeti.files.wordpress.com/2016/11/acrylic-error.png" alt="acrylic-error" width="644" height="167" />

<ol>
    <li>Running <code>valet</code> command shows a list of options.</li>
    <li>You will now need to change the DNS settings on your machine, to ensure that it uses the local DNS first. At the <strong>Start Menu</strong> type <code>network</code> and open the <strong>Network and Sharing Center</strong>.</li>
    <li>Click on <strong>Change adapter settings</strong></li>
    <li>Right Click on <strong>Local Area Network Connection</strong> and select <strong>Properties</strong>.</li>
    <li>Click on the <strong>Internet Protocol Version 4</strong> and then click the <strong>Properties</strong> button below it.</li>
    <li>Click on <strong>Use the following DNS server addresses:</strong> and enter <code>127.0.0.1</code> in the <strong>Preferred DNS Server</strong> box, and <code>8.8.8.8</code> in the <strong>Alternate DNS Server</strong> (to use Google's DNS Server for other DNS lookups). Then Click OK.</li>
    <li>Click on the <strong>Internet Protocol Version 6</strong> and then click the <strong>Properties</strong> button below it.</li>
    <li>Click on <strong>Use the following DNS server addresses:</strong> and enter <code>::1</code> in the <strong>Preferred DNS Server box</strong>, then Click OK.</li>
    <li>Click OK again.</li>
    <li>Go back to the <strong>Command Prompt</strong> and remember the path to the <em>valet</em> folder.</li>
    <li>Add that path the <strong>PATH</strong> Environment Variable. Click on <strong>Start Menu</strong> -> Right click on <strong>Computer</strong> -> select <strong>Properties</strong> -> Click on <strong>Advanced system settings</strong> -> click on <strong>Environment Variables...</strong> button -> in the <strong>System Variable</strong> menu scroll until you see <strong>Path</strong> -> select <strong>Path</strong> -> click on <strong>Edit...</strong> button -> at the end of the list type <code>;&lt;path to the <em>valet</em> folder&gt;</code>, for example <code>;C:\Users\touch\valet</code> -> click OK a few times.</li>
    <li>Close the <strong>Command Prompt</strong> window and open a new one as an Administrator, or open a new <strong>GitBash</strong> terminal.</li>
    <li><code>cd</code> to the directory where your PHP projects are stored.</li>
    <li>Type <code>valet park</code></li>
    <li>You may be able to restart the Network Adapter now and jump to ste[ 18, or you may need to do step 16 and 17 below.</li>
    <li>You will need to add the name of each project into the local hosts file. <strong>Start menu</strong> -> <strong>All Programs</strong> -> <strong>Accessories</strong> -> Right Click on <strong>Notepad</strong> -> Select <strong>Run as Administrator</strong>.</li>
    <li>Open <code>C:\Windows\System32\drivers\etc\hosts</code> file in <strong>Notepad</strong>, and add <code>127.0.0.1 .dev</code> to the bottom of the list. For example <code>127.0.0.1 laravel.dev</code> if your project is called <em>laravel</em> and is stored in a directory called <em>laravel</em>.</li>
    <li>Open a browser and navigate to <code>http://laravel.dev</code></li>
    <li>Voila</li>
</ol>

You can watch the above (more or less) in action at <a href="https://www.youtube.com/watch?v=qy5BThVJBpU" target="_blank">https://www.youtube.com/watch?v=qy5BThVJBpU</a>
