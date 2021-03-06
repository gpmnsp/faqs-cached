<h1>rTorrent - troubleshooting common errors</h1>

        
<br>
rTorrent is a text-mode bittorrent client â€” you can watch how it works through any ssh client, web browser or even a cellphone. Wikipedia and the official website say that the very optimized code makes rTorrent faster than the official client.<br>
<br>
If editing the rTorrent configuration file please note you will need to <code>Show Hidden Files</code> or equivalent if using a Windows or Mac based client as files beginning with a period <code>.</code> are hidden by default - the file is called <code>.rtorrent.rc</code>.<br>
<br>
<h3>Getting Familiar with rTorrent</h3><br>
Use PuTTY to <a href="https://www.feralhosting.com/faq/view?question=12">log onto your server via secure shell (SSH)</a>.<br>
<br>
rTorrent runs in screen sessions, which could be compared to windows. To minimize a window with rTorrent in it, you <code>detach</code> a screen. To reopen a window, you <code>reattach</code> a screen.<br>
<br>
Try it. To join &#x2F; reattach an existing rTorrent screen:<br>
<br>
<strong>1:</strong> Find out your rTorrent screen session&#x27;s PID (process ID).<br>
&nbsp; <br>
Type to list all matching processes:<br>
<br>
<pre><code>ps x | grep rtorrent | grep -v grep</code></pre><br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/rtorrent1.png"><br>
<br>
Or for just the screen itself:<br>
<br>
<pre><code>screen -ls | grep rtorrent</code></pre><br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/rtorrent2.png"><br>
<br>
<strong>2:</strong> Reattach the screen session with rTorrent in it.<br>
&nbsp; <br>
Type:<br>
<br>
<pre><code>screen -r PID</code></pre><br>
Where <code>PID</code> is the process ID assigned by the system to your rTorrent screen session preceding <code>rtorrent</code> in the list shown above: The <code>PID</code> is <code>15057</code> in this example.&nbsp;  <br>
<br>
Based of the example image above:<br>
<br>
<pre><code>screen -r 15057</code></pre><br>
You should now see this if rtorrent is running.<br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/1.png"><br>
<br>
<h3>rTorrent Interface Overview</h3><br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/2.png"><br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/3.png"><br>
&nbsp; <br>
<h3>Controlling rTorrent</h3><br>
rTorrent is controlled entirely through keyboard shortcuts. Invest some time in learning them, and it will pay off greatly in no time.<br>
<br>
Try moving about â€” use the arrow keys, or press <code>0-9</code> to see rTorrent&#x27;s different <code>views</code>. If you can&#x27;t, rTorrent may be frozen, and you will need to restart it (see below).<br>
&nbsp; <br>
Here&#x27;s a <a href="http://tekguru.files.wordpress.com/2009/05/rtorrent_ref.pdf">handy reference card of all rTorrent shortcuts in a .pdf file</a>.<br>
<br>
<h3>Minimizing &#x2F; Detaching rTorrent Screen Session</h3><br>
If you close your PuTTY window at this point, it will effectively kill rTorrent. To exit PuTTY while leaving rTorrent running in the background, you will need to <code>detach</code> the screen session rTorrent is running in. This is similar to minimizing a window.<br>
<br>
Then press and hold <code>CTRL</code> and <code>a</code> then press <code>d</code> to detach from the screen. This leaves it running in the background.<br>
<br>
<h3>Restarting rTorrent (Properly)</h3><br>
If rTorrent is running OK, you can attach to it (see above) with:<br>
<br>
<pre><code>screen -r PID</code></pre><br>
Pressing and holding <code>Ctrl</code> and then pressing <code>q</code> exits (terminates) rTorrent and closes the screen session. When rTorrent starts again it will not re-hash all your torrents (but it will if you use kill, see below).<br>
<br>
There is a cron job running on the server that checks every 10 minutes if your rTorrent is running, and if it&#x27;s not, restarts it for you.<br>
<br>
<h3>Restarting rTorrent if it has frozen</h3><br>
However if rTorrent is frozen, you will need to kill it in order to restart it afterwards.<br>
<br>
<strong>1:</strong> Type:<br>
&nbsp; <br>
<pre><code>ps x | grep rtorrent | grep -v grep</code></pre><br>
(this will list all processes under your username).<br>
&nbsp; <br>
<strong>2:</strong> Type:<br>
&nbsp; <br>
<pre><code>kill -9 PID</code></pre><br>
(where PID is the process ID listed in the left column for rTorrent).<br>
<br>
<img src="https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/Installable%20software/rTorrent%20-%20troubleshooting%20common%20errors/4.png"><br>
<br>
Once killed run:<br>
<br>
<pre><code>ps x | grep rtorrent | grep -v grep</code></pre><br>
again to make sure it is dead. Repeat the kill command a few times if it doesn&#x27;t work the first time.<br>
<br>
Now you can start it back up by typing:<br>
<br>
<pre><code>screen rtorrent</code></pre><br>
It may take a few seconds to start up if you have a lot of torrents added.<br>
<br>
<h3>If rTorrent cannot be killed</h3><br>
Sometimes processes are not able to be killed, even with<br>
<br>
<pre><code>kill -9</code></pre><br>
In this event please open a support ticket informing us that you have already tried the <code>kill</code> command.<br>
<br>
<h3>rTorrent Preferences</h3><br>
rTorrent preferences are contained in the <code>.rtorrent.rc</code> file that is located in your home directory. Please be careful while changing these settings as doing so can have negative effect on the performance of the server which you are sharing with others.<br>
<br>
<h3>Enhancing rTorrent Interface</h3><br>
There are several things you can do to enhance your rTorrent interface. Consider adding the following lines to your default rTorrent config.<br>
<br>
By default rTorrent doesn&#x27;t delete the data associated with a .torrent, deleting just the .torrent file itself and leaving the data intact. This may not be what you want. To delete a .torrent file <code>and</code> the data (<code>ctrl + d</code> on a stopped torrent), add this to your <code>.rtorrent.rc</code> file (you will need to terminate rTorrent, edit the file, and restart rTorrent for the new settings to take effect):<br>
<br>
<strong>rTorrent 0.8.2</strong>:<br>
<br>
<pre><code># Delete data on torrent deletion
on_erase = on_erase,&quot;execute={rm,-rf,--,$d.get_base_path=}&quot;</code></pre><br>
<strong>rTorrent 0.8.4</strong>:<br>
<br>
<pre><code># Delete data on torrent deletion
system.method.set_key = event.download.erased,on_erase,&quot;execute={rm,-rf,--,$d.get_base_path=}&quot;</code></pre><br>
The following setting will enhance rTorrent&#x27;s active view (9) by making it what it really should be â€” a dynamically updated explicit list of what you&#x27;re uploading and downloading at the moment:<br>
<br>
<pre><code># Show jobs currently uploading or downloading in active view. Update every 10 seconds.
schedule = filter_active,10,10,&quot;view_filter = active,\&quot;or={d.get_up_rate=,d.get_down_rate=}\&quot;&quot;</code></pre><br>
If you wish to sort your main view (1) in reverse chronological order (newly added torrents first), add this to your config:<br>
<br>
<pre><code># Sort main view by last added
view_sort_current = main,greater=d.get_creation_date=</code></pre><br>
<h3>Configuring rTorrent to Use Several Watch and Data Directories</h3><br>
Pressing and holding <code>CTRL</code> and then pressing <code>q</code> to quit &#x2F; exit rTorrent.<br>
<br>
Locate the <code>.rtorrent.rc</code> file that resides in your home directory, and add the following lines to it:<br>
<br>
<pre><code># Watch directory 2 with a different destination.
schedule = watch_directory_2,60,60,&quot;load_start=&#x2F;PATH_TO_WATCH2&#x2F;*.torrent,d.set_directory=&#x2F;PATH_TO_DATA2&#x2F;&quot;</code></pre><br>
Restart rTorrent.<br>
<br>
Now when you put a <code>.torrent</code> into the WATCH2 dir, rTorrent will pick it up within 60 seconds and store the data in the DATA2 dir.<br>
<br>
You can have several more, if that suits your needs:<br>
<br>
<pre><code># Watch directory 3 with a different destination.
schedule = watch_directory_3,60,60,&quot;load_start=&#x2F;PATH_TO_WATCH3&#x2F;*.torrent,d.set_directory=&#x2F;PATH_TO_DATA3&#x2F;&quot;</code></pre><br>
... and so on.<br>
<br>
That&#x27;s the beauty of rTorrent â€” it&#x27;s highly configurable.<br>
<br>
<h3>Errors and Status Messages</h3><br>
<pre><code>FILE CHUNK ERROR &#x2F; STORAGE ERROR: CANNOT ALLOCATE MEMORY</code></pre><br>
When you get that error, it means rTorrent is running out of available RAM to download to, and is moving data out of RAM and onto the disk. It doesn&#x27;t usually happen with audio torrents since those are relatively small in size.<br>
<br>
If you just let it keep running, it will work fine, downloading data to the disk, which is a little slower. It will finish downloading, and then it will look like it&#x27;s hashing, but what it&#x27;s actually doing is putting the pieces back together.<br>
<br>
<pre><code>COULD NOT PARSE BENCODED DATA</code></pre><br>
This message is rTorrent&#x27;s way of saying that there is a communication problem with the tracker. (Like a 404 error for websites.) Just leave it be, and once the communication resumes, the error will go away. You can also go check with your tracker, to see if they are having issues: most trackers have a status in the IRC channel or website.<br>
<br>
<pre><code>TRIED ALL TRACKERS</code></pre><br>
From the developer himself: <br>
<br>
&quot;The message just means it was at the end of the list, or reached the end, not that it didn&#x27;t manage to connect to any trackers. This can happen when libtorrent automatically requests more peers.&quot;<br>
<br>
In other words, it&#x27;s harmless, just ignore it.<br>
<br>
<h3>PROBLEM: rTorrent will not start in shell</h3><br>
You try to start the rTorrent process with the command:<br>
<br>
<pre><code>screen rtorrent</code></pre><br>
but it just returns an error:<br>
<br>
<strong>Important note:</strong> This is not an rtorrent error, this is a screen command error.<br>
<br>
<pre><code>Screen is terminating</code></pre><br>
You can then start Screen with a command:<br>
<br>
<pre><code>screen</code></pre><br>
This will put you inside a Screen session. And once inside the Screen session, type: <br>
<br>
<pre><code>rtorrent</code></pre><br>
It will give you some kind of error telling you why it cannot start. <br>
<br>
If the error is:<br>
<br>
<pre><code>rtorrent: Could not lock session directory: &quot;&#x2F;home&#x2F;USERNAME&#x2F;private&#x2F;rtorrent&#x2F;work&#x2F;&quot;, held by &quot;&lt;error&gt;&quot;.</code></pre><br>
or the errors states:<br>
<br>
<pre><code>rtorrent: Invalid DHT cache</code></pre><br>
then here is what needs to be done:<br>
<br>
<strong>1:</strong> Close the Screen session you just opened, by typing:<br>
<br>
<pre><code>exit</code></pre><br>
<strong>2:</strong> Now you need to delete the <code>rtorrent.lock</code> file which is located in the <code>~&#x2F;private&#x2F;rtorrent&#x2F;work&#x2F;</code> folder with this command:<br>
<br>
<pre><code>rm -f ~&#x2F;private&#x2F;rtorrent&#x2F;work&#x2F;rtorrent.lock</code></pre><br>
Or delete the file <code>rtorrent.dht_cache</code>, which is in the same directory, with this command: <br>
<br>
<pre><code>rm -f ~&#x2F;private&#x2F;rtorrent&#x2F;work&#x2F;rtorrent.dht_cache</code></pre><br>
<strong>3:</strong> You can now start rTorrent with the normal command: <br>
<br>
<pre><code>screen rtorrent</code></pre><br>
It should now launch without an error. Log into your ruTorrent session to verify.<br>
<br>

