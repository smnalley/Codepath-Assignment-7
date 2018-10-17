# Codepath-Assignment-7
Procedures and proofs of concept for Assignment 7, Kali Linux vs. Wordpress

Exploit 1: Cross-site scripting via comment section
1) Go to the comment section of any post on version 4.2 of Wordpress or earlier.
2) Inject a malicious script into a comment. There appear to be no escaping requirements or other protections in place against XSS. We use the classic alert proof of concept.
3) The script will execute immediately after posting the comment. It will also load every time the post page reloads. Consecutive XSS injections can be spread across multiple comments.
GIF:
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress2_1.gif" width="800">

Exploit 2: Cross-site scripting via music metadata
1) Upload any audio file within file size constraints to the admin's media folder
2) As admin, start creating a post. Choose "Add Media," and choose "Create a playlist."
3) Add the audio file to the playlist, but insert an XSS script into the title. Again, we use the classic alert.
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress3_1.gif" width="800">
4) Create the playlist, ensure the playlist is inserted into the post, and publish the post. The post will trigger the XSS script when viewed.
5) Note: this does NOT work unless the media is part of a playlist. Putting the media in the playlist ensures that the title is displayed and thus ensures that the browser runs the script in the title.


Exploit 3: Cross-site scripting via image upload
1) Upload any image file within file size constraints to the admin's media folder
2) As admin, start creating a post. Choose "Add Media," but this time choose "Create an Image Gallery."
3) Add the image to the gallery. Insert an XSS script into the title, an alert in our case.
4) Create the gallery, ensure it's inserted into the post, and publish. 
5) Go to the post and click on the image to trigger the script.
6) Again, this will not work for images not part of an image gallery.
<img src="https://github.com/smnalley/Codepath-Assignment-7/blob/master/Wordpress4_1.gif" width="800">

