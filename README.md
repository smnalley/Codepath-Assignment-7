# Codepath-Assignment-7
Procedures and proofs of concept for Assignment 7, Kali Linux vs. Wordpress

Exploit 1: Cross-site scripting via comment section, CVE unknown, Ver. <=4.2
https://klikki.fi/adv/wordpress2.html
1) Go to the comment section of any post on version 4.2 of Wordpress or earlier.
2) Inject a malicious script into a comment. There appear to be no escaping requirements or other protections in place against XSS. We use the classic alert proof of concept.
3) The script will execute immediately after posting the comment. It will also load every time the post page reloads. Consecutive XSS injections can be spread across multiple comments.
GIF:
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress2_1.gif" width="800">

Exploit 2: Cross-site scripting via music metadata, CVE 2016-6814, Ver. <4.7.3
https://sumofpwn.nl/advisory/2016/wordpress_audio_playlist_functionality_is_affected_by_cross_site_scripting.html
1) Upload any audio file within file size constraints to the admin's media folder
2) As admin, start creating a post. Choose "Add Media," and choose "Create a playlist."
3) Add the audio file to the playlist, but insert an XSS script into the title. Again, we use the classic alert.
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress3_1.gif" width="800">
4) Create the playlist, ensure the playlist is inserted into the post, and publish the post. The post will trigger the XSS script when viewed.
5) Note: this does NOT work unless the media is part of a playlist. Putting the media in the playlist ensures that the title is displayed and thus ensures that the browser runs the script in the title.


Exploit 3: Cross-site scripting via image upload, CVE 2016-7168, Ver. 2.5-4.6
https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html
1) Upload any image file within file size constraints to the admin's media folder
2) As admin, start creating a post. Choose "Add Media," but this time choose "Create an Image Gallery."
3) Add the image to the gallery. Insert an XSS script into the title, an alert in our case.
4) Create the gallery, ensure it's inserted into the post, and publish. 
5) Go to the post and click on the image to trigger the script.
6) Again, this will not work for images not part of an image gallery.
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress4_1.gif" width="800">

Exploit 4: Cross-site scripting via fake video link, CVE-2017-6817, Ver 4.0-4.72
https://blog.sucuri.net/2017/03/stored-xss-in-wordpress-core.html
1) As an admin, start creating a post.
2) Embed a fake Youtube URL as shown. You can achieve this either by inputting the fake URL under the URL embed option under "Add Media", or you can type in the full HREF embed as shown. 
3) Publish the post and navigate to it. The XSS script should trigger.
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress5_1.gif" width="800">

