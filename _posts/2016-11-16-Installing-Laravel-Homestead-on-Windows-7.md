Just following the <a href="https://laravel.com/docs/5.3/homestead" target="_blank">Laravel Homestead Installation Instructions</a> will not be enough, if using a Windows machine. Below is a summary of a few issues that I have had, and then overcame, to get working system.
<ol>
	<li>Make sure that your machine has Virtualisation enabled in the BIOS. I found <a href="https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Virtualization/sect-Virtualization-Troubleshooting-Enabling_Intel_VT_and_AMD_V_virtualization_hardware_extensions_in_BIOS.html" target="_blank">this article</a> useful. Without this, your VirtualBox will probably not work. If you cannot enable this, then you probably won't be able to run VirtualBox successfully.</li>
	<li>If the command
<code>vagrant up</code>
does not work first time, then you should open the VirtualBox application to see what messages are being sent to the screen. It may be that it is waiting for some input, or that an error message is being displayed. Click on the <strong>Show</strong> arrow to display the terminal.<img class="alignnone size-full wp-image-23" src="https://nisbeti.files.wordpress.com/2016/11/virtualbox.png" alt="virtualbox" width="780" height="627" /></li>
	<li>If you get an error message that Homestead-7 already exists, then you will want to destroy the current attempt with
<code>vagrant destroy --force</code>
then delete the <em>homestead-7</em> directory from within <strong>C:\Users\\VirtualBox VMs\</strong> directory.</li>
	<li>I found that I needed to change the <strong>homestead.rb</strong> file settings a little. In a text editor open <strong>C:\Users\\Homestead\scripts\homestead.rb</strong> and change the reference of the repository from
<code>laravel/homestead</code>
to
<code>laravel/homestead-7</code>
and the version from
<code>">= 0.4.0"</code>
to
<code>">= 0.2.1"</code>
<img class="alignnone size-full wp-image-26" src="https://nisbeti.files.wordpress.com/2016/11/homestead-rb.png" alt="homestead-rb" width="786" height="481" /></li>
	<li>The final step to get it all working was to run the following command before <em>vagrant up</em>
<code>vagrant plugin install vagrant-vbguest</code>
as suggested in <a href="https://github.com/fideloper/Vaprobash/issues/92" target="_blank">this article</a></li>
	<li>Now the system worked fine.</li>
</ol>
