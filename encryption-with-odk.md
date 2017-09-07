Encrypted data collection using ODK Briefcase
===========================================

As part of our commitment to responsible data management, the American Red Cross uses encryption when collecting sensitive information using mobile data collection. We do this using ODK Briefcase. The online instructions are a little tricky to follow, so here's a guide to setting this up. We use omkserver on [POSM](www.posm.io) but these instructions will cover 90% of the content for a different server situation.

## Setup for Windows

Link is [here](http://support.kobotoolbox.org/customer/portal/articles/1948428-encrypting-forms)

## Setup for MacOS

1. Download [ODK Briefcase](https://opendatakit.org/use/briefcase/). The application is a `.jar` file. Put this somewhere handy.
2. Download dependencies. There are instructions for this on the [ODK encrypted forms page](https://opendatakit.org/help/encrypted-forms). Under Configuration, look for the Java Cryptography Extension package (currently available [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html)). Download this package.

<figure>
<img src="https://arcmaps.s3.amazonaws.com/share/blog-pictures/odk-encryption-pic1.jpg" alt="JCE package to download">
<p class="caption">JCE package to download</p>
</figure>

3. Unzip the JCE package that you just downloaded. Open the folder it creates. You should see three files, shown in the screenshot below. Copy these files. You will need to paste them to another location.

<figure>
<img src="https://arcmaps.s3.amazonaws.com/share/blog-pictures/odk-encryption-pic2.jpg" alt="Inside the JCE package download">
<p class="caption">(Copy these files to paste elsewhere)</p>
</figure>

4. Navigate to your internet plug-ins. On a Mac, this will generally be `Macintosh HD/Library/Internet Plug-ins/`. You should see a file called `JavaAppletPlugin.plugin`. Right-click this file and select `Show package contents`. In the new directory that appears, navigate to `Contents/home/lib/security`. Paste the JCE files (that you copied in Step 3) into this directory.

<figure>
<img src="https://arcmaps.s3.amazonaws.com/share/blog-pictures/odk-encryption-pic3.jpg" alt="Paste the JCE files here">
<p class="caption">(Paste the JCE files here)</p>
</figure>

## Creating public and private keys, creating encrypted ODK form

Now that you've got the right configuration, you can start to use ODK Briefcase.

Creating an encrypted form is just like creating a regular ODK form, except that you will add a public key into the `settings` tab in the XLS form. ODK will build the form with this public key and later on, you'll use your corresponding private key to decrypt the data.

To create a public and private key pair:

1. Open Terminal and navigate to the folder where you want the keys to live. I put these in the same directory as where my survey form and results will go.
2. Create a private key using the command `openssl genrsa -out NameOfKey_private.pem 2048`. You may get a note saying, `unable to write 'random state'` but the pem should still be created. If you get an error message, you may need to add `sudo` to the beginning of this command.
3. Use the private key you just created in order to create a public key. Use the command `openssl rsa -in NameOfKey_private.pem -inform PEM -out NameOfKey_public.pem -outform PEM -pubout`
4. Navigate to the public key you just created. Open it in a text editor and copy the text.
5. In your XLS form, go to the `Settings` tab. If you don't already have a Settings tab, then create one. You need to have a column titled `public_key`. Paste the text from your public key file into this column. You can then use the XLS form to create your ODK survey and load it onto mobile devices. In Excel, you'll need to make sure there are no line breaks in the text containing the key (it should be a continous stream of text, not split across 8 lines)

<figure>
<img src="https://arcmaps.s3.amazonaws.com/share/blog-pictures/odk-encryption-pic4.jpg" alt="Add public key to ODK XLS form">
</figure>

## Decrypting data

We upload data from mobile devices onto omkserver running on POSM servers.

On omkserver, encrypted data will be a random string of text. You have to download and decrypt the submissions in order to be able to use them. "Downloading" the data works in two steps: first ODK Briefcase fetches ("pulls") all the encrypted submissions and attachments. Then ODK Briefcase decrypts ("exports") them.

1. Open ODK Briefcase (the `.jar` file)
2. Under the "Pull" tab, select the type of server (ODK Aggregate 1.0) and the server url (http://posm.io). Connect to this server and select the forms to fetch.
3. Under the "Export" tab, select the form, the export type, the export directory, and the PEM private key file to use for decryption. This will give you a directory with results and attachments.

<figure>
<img src="https://arcmaps.s3.amazonaws.com/share/blog-pictures/odk-encryption-pic5.jpg"
</figure>
