# Snapchat for PHP


This library is built to communicate with the Snapchat API. So far it supports
logging in/out, fetching snaps, downloading snaps, marking snaps viewed,
uploading snaps, and sending snaps.

It's similar to the [excellent Snaphax library](http://github.com/tlack/snaphax)
built by Thomas Lackner <[@tlack](http://twitter.com/tlack)>, but the approach
is different enough that I figured it deserved its own repo.


## Class Methods


```php
require 'snapchat.php';

$snapchat = new Snapchat('username', 'password');
$snapchat->logout();
```

- #### getSnaps()

    ```php
    echo $snapchat->getSnaps();
    ```

- #### getMedia($snap_id)

    ```php
    $data = $snapchat->getMedia('122FAST2FURIOUS334r');
    file_put_contents('/home/dan/snap.jpg', $data);
    ```

- #### markSnapViewed($snap_id)

    ```php
    echo $snapchat->markSnapViewed('122FAST2FURIOUS334r');
    ```

- #### uploadImage($image_path)

    ```php
    echo $snapchat->uploadImage('../test.jpg');
    ```

- #### uploadVideo($video_path)

    ```php
    echo $snapchat->uploadVideo('../test.mp4');
    ```

- #### send($snap_id, $friends_array, $seconds)

    ```php
    $id = $snapchat->uploadImage('../test.jpg');
    echo $snapchat->send($id, array('kartiktalwar'), 8);
    ```

- #### getFriends()

    ```php
    echo $snapchat->getFriends();
    ```

- #### addFriends($friends_array)

    ```php
    echo $snapchat->addFriends(array('bill', 'bob', 'bart'));
    ```

- #### getBests($friends_array)

    ```php
    echo $snapchat->getBests(array('bill', 'bob'));
    ```

- #### deleteFriends($friends_array)

    ```php
    echo $snapchat->deleteFriends(array('bart'));
    ```

- #### updatePrivacy($privacy)

    ```php
    echo $snapchat->updatePrivacy(Snapchat::PRIVACY_FRIENDS);
    ```


## Usage


Include src/snapchat.php via require_once or Composer or whatever, then:

```php
<?php

// Log in:
$snapchat = new Snapchat('username', 'password');


// Get your feed:
$snaps = $snapchat->getSnaps();

// Download a specific snap:
$data = $snapchat->getMedia('122FAST2FURIOUS334r');
file_put_contents('/home/dan/snap.jpg', $data);

// Mark the snap as viewed:
$snapchat->markSnapViewed('122FAST2FURIOUS334r');

// Upload a snap and send it to me for 8 seconds:
$id = $snapchat->upload(
	Snapchat::MEDIA_IMAGE,
	file_get_contents('/home/dan/whatever.jpg')
);
$snapchat->send($id, array('stelljes'), 8);

// Get a list of your friends:
$friends = $snapchat->getFriends();

// Add some people as friends:
$snapchat->addFriends(array('bill', 'bob', 'bart'));

// Get a list of the people you've added:
$added = $snapchat->getAddedFriends();

// Find out who Bill and Bob snap the most:
$bests = $snapchat->getBests(array('bill', 'bob'));

// You don't like Bart all that much:
$snapchat->deleteFriends(array('bart'));

// You don't want Bart to be able to send you photos:
$snapchat->updatePrivacy(Snapchat::PRIVACY_FRIENDS);

// Log out:
$snapchat->logout();

?>
```



## License

MIT
